# ADR-0002 · Estado de propiedad en tiempo real vía polling corto
**Estado:** aceptado
**Fecha:** 2026-07-05

## Contexto y fuerza

`requisitos.md` R-05 exige que el portal público muestre el estado de cada
propiedad (disponible/reservada/vendida) "en tiempo real"; R-14 acota ese
requisito con un número concreto: **latencia máxima de 60 segundos** entre el
cambio interno y su reflejo en el portal. US-05 (`stories.md`, 5 pts, Sprint
1) traduce esto en un criterio de aceptación verificable: "el estado
actualizado aparece en menos de 60 segundos".

`personas.md` describe el dolor origen —un cliente hizo una visita de 40
minutos a una propiedad ya reservada— pero no describe volumen de tráfico
alto ni concurrencia masiva; es una inmobiliaria de Cuenca con 4 asesores.

## Decisión

El estado de propiedad se refresca en el portal del cliente mediante
**polling corto** (consulta periódica del frontend al backend, cada ~20-30
segundos) sobre el endpoint de estado de la propiedad. Esto cumple con
holgura el límite de 60 segundos de R-14 sin introducir un canal de
comunicación persistente.

## Alternativas consideradas

- **WebSockets** — descartado por ahora: exige gestión de conexiones
  persistentes, reconexión ante caídas de red del cliente, y afinidad de
  sesión si se escala horizontalmente; ninguna de estas necesidades está
  respaldada por el inbox para el volumen actual de la inmobiliaria.
- **Server-Sent Events (SSE)** — descartado por la misma razón que
  WebSockets: resuelve un problema de latencia sub-segundo que R-14 no exige
  (el requisito es 60 s, no "instantáneo").

## Consecuencias

Se cumple el requisito medible (R-14) con el mecanismo más simple de operar,
compatible con el monolito modular sin estado de conexión (ADR-0001). El
costo aceptado es tráfico de polling redundante y una latencia "hasta" el
intervalo de polling (peor caso dentro del margen de 60 s exigido). Esta
decisión se debe revisar si aparece evidencia futura de que el requisito de
latencia se endurece, o si el volumen de usuarios concurrentes crece de forma
que el polling se vuelva costoso — ninguna de esas condiciones está
evidenciada en el inbox hoy.
