# ADR-0003 · Prevención de doble reserva con restricción única en base de datos relacional
**Estado:** aceptado
**Fecha:** 2026-07-05

## Contexto y fuerza

US-06 (`stories.md`, 8 pts, Sprint 1, la historia de mayor tamaño del sprint)
exige que el cliente reserve una visita "sin hacer ninguna llamada" y que,
si un horario ya está ocupado, el sistema "le ofrece el siguiente día
disponible". El refinamiento de la historia (nota de tamaño y decisión de
refinamiento en `stories.md`) confirma, con evidencia de `personas.md` (cada
asesor gestiona su propia cartera de 15-20 propiedades activas) y del
criterio de aceptación original, que **cada propiedad tiene un único asesor
asignado** — no hay arbitraje entre varios asesores para el mismo slot.

La fuerza real detrás de esta decisión: si dos clientes intentan reservar el
mismo horario del mismo asesor casi al mismo tiempo, y el sistema no lo
impide con una garantía fuerte, el propio sistema reproduciría el dolor que
motivó el MVP (visita en vano, `mvp-canvas.md`) — solo que causado por una
falla del sistema, no por falta de información.

## Decisión

El módulo de Agendamiento persiste las reservas en **PostgreSQL** con una
**restricción única** sobre la combinación `(asesor_id, fecha_hora_slot)`. La
confirmación de una reserva se ejecuta dentro de una **transacción atómica**:
si dos solicitudes concurrentes intentan reservar el mismo slot, la base de
datos garantiza que solo una tenga éxito; la segunda recibe un error de
conflicto y el frontend le ofrece el siguiente horario disponible (ya exigido
por el propio criterio de aceptación de US-06).

## Alternativas consideradas

- **Lock optimista solo a nivel de aplicación (sin restricción en BD)** —
  descartado: bajo una condición de carrera real (dos clientes reservando el
  mismo slot en una ventana de milisegundos), la garantía dependería
  enteramente de la lógica de aplicación sin respaldo del motor de datos,
  dejando una ventana de doble reserva posible.
- **Cola de mensajes que serialice las reservas (ej. RabbitMQ)** —
  descartado por sobre-ingeniería: agrega un componente de infraestructura
  nuevo para un volumen de reservas bajo (4 asesores, 15-20 propiedades cada
  uno); no hay evidencia en el inbox de picos de tráfico que justifiquen esa
  complejidad operativa adicional.

## Consecuencias

Se obtiene la garantía de "no doble reserva" —el requisito no-negociable de
esta historia— con el mecanismo más simple disponible dentro de la misma
base de datos que ya usa el resto del monolito (ADR-0001). El costo aceptado
es acoplar esta garantía de consistencia al motor relacional elegido: migrar
en el futuro a un almacén eventualmente consistente exigiría rediseñar esta
regla de negocio.
