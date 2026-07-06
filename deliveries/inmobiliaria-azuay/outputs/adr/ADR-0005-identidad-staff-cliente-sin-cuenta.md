# ADR-0005 · Identidad y autorización: cuentas para staff, cliente sin cuenta persistente
**Estado:** aceptado
**Fecha:** 2026-07-05

## Contexto y fuerza

Ninguna de las historias comprometidas en Sprint 1 (US-05, US-06, US-07,
US-01) menciona que el cliente deba registrarse o iniciar sesión. R-07
(`requisitos.md`) exige que el cliente "seleccione fecha y hora de visita
directamente desde el portal, **sin necesidad de llamar** a la
inmobiliaria" — el foco es eliminar la fricción telefónica, no describe ni
exige una cuenta de cliente.

En cambio, el asesor y la gerente sí operan sobre datos sensibles y acciones
que requieren distinguir rol: cambiar el estado de una propiedad (US-05),
gestionar su propia agenda de horarios (US-06), y —en épicas futuras— ver el
historial de sus clientes (US-03/E-04) o el panel gerencial (E-08).

La única historia del backlog que sí requeriría identidad persistente de
cliente es **US-09** (E-07, "configurar alertas", "propiedad marcada como
favorita"), y el propio `mvp-canvas.md` la deja fuera de alcance
explícitamente: *"se construye sobre la adopción del agendamiento, no
antes"*.

## Decisión

- **Staff (asesor, gerente):** cuenta con autenticación (sesión o JWT) y
  autorización basada en rol. Rutas de cambio de estado de propiedad,
  calendario del asesor y (a futuro) panel gerencial quedan protegidas por
  rol.
- **Cliente:** sin cuenta persistente en Sprint 1. Se identifica con nombre y
  un dato de contacto (teléfono o email) al momento de agendar la visita
  (US-06); ese contacto es suficiente para registrar la reserva y para que
  US-07 le envíe la notificación proactiva si cambia el estado de la
  propiedad.

## Alternativas consideradas

- **Cuenta obligatoria para el cliente desde Sprint 1 (registro + login)** —
  descartado: no hay evidencia en el inbox de que agendar una visita
  requiera una cuenta; exigirlo introduciría fricción nueva en el mismo
  flujo que el MVP busca simplificar (cambiar la llamada telefónica por un
  formulario de registro no es "sin depender del teléfono", es reemplazar
  una fricción por otra).

## Consecuencias

Se resuelve el Sprint 1 sin construir un sistema de cuentas de cliente que
ninguna historia comprometida exige todavía, manteniendo el flujo de
agendamiento tan simple como lo pide R-07. El costo/riesgo aceptado: cuando
E-07 (US-09, alertas y favoritos) se priorice, habrá que introducir identidad
persistente de cliente (registro, sesión, almacenamiento de criterios de
búsqueda) — se declara explícitamente como **open question** para ese
momento, no como algo pendiente de este sprint.
