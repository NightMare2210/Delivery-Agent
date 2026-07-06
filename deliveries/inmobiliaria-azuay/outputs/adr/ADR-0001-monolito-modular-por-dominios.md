# ADR-0001 · Monolito modular por dominios en vez de microservicios
**Estado:** aceptado
**Fecha:** 2026-07-05

## Contexto y fuerza

El Sprint 1 (`sprint-plan.md`) compromete 19 pts en cuatro historias que
cruzan tres épicas distintas: US-05 (E-01, estado en tiempo real), US-06
(E-02, agendamiento), US-07 (E-01, notificación al cliente, dependiente de
US-06) y US-01 (E-05, publicación rápida). El propio backlog ya anticipa,
como próximas prioridades, E-03 (US-04, notificación push al asesor,
dependiente de US-06) y E-04 (US-03, historial unificado del cliente), ambas
fuera del Sprint 1 solo por capacidad, no por dependencia técnica pendiente
(`sprint-plan.md`, sección "Historias de mayor prioridad que quedaron
afuera").

`personas.md` describe una inmobiliaria de 4 asesores. No hay evidencia en el
inbox de necesidad de escalar componentes de forma independiente, de equipos
distribuidos trabajando en paralelo sobre distintos servicios, ni de
requisitos de despliegue independiente.

## Decisión

Se construye un **monolito modular**: un único proceso desplegable, separado
internamente por límites de dominio (módulos): `Propiedades`, `Agendamiento`,
`Notificaciones`, `Identidad`. Cada módulo posee sus propias tablas y expone
su propia API de aplicación; la comunicación entre módulos es en memoria
(llamadas de función y eventos de dominio in-process, ver ADR-0004), no vía
red.

## Alternativas consideradas

- **Microservicios desde el día 1** — descartado: no hay fuerza en el inbox
  (escala, equipos distribuidos, despliegue independiente) que lo justifique;
  agregaría orquestación, versionado de contratos entre servicios y
  observabilidad distribuida que el equipo no necesita para un sprint de 19
  pts con 4 asesores como usuarios internos.
- **Monolito sin separación interna de módulos** (todo en una sola capa) —
  descartado: acoplaría directamente el flujo de agendamiento con el de
  notificaciones, obligando a modificar el código de Agendamiento cuando
  entre US-04 (E-03) o US-03 (E-04), que ya se conocen como próximas
  prioridades.

## Consecuencias

Ganamos la capacidad de evolucionar cada módulo de forma relativamente
independiente y, si en el futuro aparece evidencia real de necesidad de
escalamiento o despliegue independiente, extraer un módulo a servicio propio
sin rediseñar el dominio. El costo aceptado es la disciplina del equipo para
no filtrar dependencias directas entre módulos (requiere convención de
código/estructura de carpetas que respete los límites, no un enforcement de
infraestructura).
