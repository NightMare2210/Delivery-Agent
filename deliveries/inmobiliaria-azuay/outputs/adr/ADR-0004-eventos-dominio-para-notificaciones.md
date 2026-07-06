# ADR-0004 · Eventos de dominio in-process para desacoplar notificaciones del agendamiento
**Estado:** aceptado
**Fecha:** 2026-07-05

## Contexto y fuerza

Dos historias comparten el mismo hecho de negocio ("una visita se confirmó o
se canceló") pero con destinatarios y momentos distintos:

- **US-07** (E-01, 3 pts, Sprint 1, depende de US-06): notificar al
  **cliente** si el estado de la propiedad cambia después de agendar.
- **US-04** (E-03, 5 pts, prioridad 3, **no comprometida en Sprint 1 por
  capacidad**, `sprint-plan.md`): notificar al **asesor** cuando se confirma o
  cancela una visita en su agenda.

La fuerza explícita está en el propio criterio de aceptación de US-06
(`stories.md`, `user-stories.md`): *"el sistema lo registra, entonces recibe
un comprobante en pantalla y **el asesor recibe la notificación (US-04)**"*.
Es decir, el flujo de agendamiento ya está escrito asumiendo que la
notificación al asesor existe, aunque US-04 no entre a este sprint. Si el
módulo de Agendamiento llama directamente a la lógica de notificación push,
cuando US-04 entre al backlog (próxima prioridad conocida, E-03) habría que
volver a tocar el código de agendamiento ya probado.

## Decisión

El módulo de Agendamiento (y el de Propiedades) publican **eventos de
dominio** (`VisitaConfirmada`, `VisitaCancelada`, `EstadoPropiedadCambiado`)
a un **bus de eventos in-process** (dentro del mismo monolito, sin broker
externo). El módulo de Notificaciones se suscribe a esos eventos y decide el
canal de entrega. En Sprint 1 se implementa **solo** el suscriptor necesario
para US-07 (notificación al cliente). Cuando US-04 entre al sprint, se agrega
un nuevo suscriptor (canal push al asesor) sin modificar el módulo de
Agendamiento.

## Alternativas consideradas

- **Acoplar el envío de notificación directamente en el flujo de
  confirmación de visita** (ej. una llamada explícita a
  `enviarNotificacionAsesor()` desde el código de Agendamiento) —
  descartado: mezclaría la regla de negocio de agendamiento con el detalle de
  canales de entrega; cada canal nuevo (US-04 ahora, alertas de US-09
  después) obligaría a modificar Agendamiento otra vez.
- **Cola de mensajes externa (Kafka/RabbitMQ/SQS) para los eventos** —
  descartado por ahora: agrega infraestructura y operación (broker, dead
  letter queue, monitoreo) que un monolito de 19 pts/sprint con 4 asesores no
  necesita todavía; se reconsiderará si aparecen más consumidores async de
  alto volumen o necesidad de desplegar Notificaciones como servicio propio.

## Consecuencias

Se gana la capacidad de sumar US-04 —la siguiente prioridad conocida del
backlog (E-03)— sin retrabajar el módulo de Agendamiento ya construido y
probado en Sprint 1. El costo aceptado: el bus in-process no persiste
eventos no entregados si el proceso se reinicia; esto es aceptable porque el
propio criterio de aceptación de US-04 ya contempla ese caso ("el evento
queda registrado igualmente y visible en su calendario" — el estado
persistido en base de datos, no el evento en tránsito, es la fuente de
verdad).

**Supuesto explícito:** el inbox no especifica el canal exacto de la
notificación al cliente en US-07 (push, email o in-app). Se asume
notificación in-app + email como la opción más simple sin infraestructura de
push móvil adicional; esto no está confirmado por ninguna evidencia del
inbox y debe validarse con el PO/discovery si se requiere otro canal.
