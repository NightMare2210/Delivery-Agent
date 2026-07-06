# Sprint 1 — El cliente ve el estado real de las propiedades y agenda su visita 100% desde el portal, sin depender del teléfono

**Capacidad:** 20 · **Comprometido:** 19

| Historia | Pts | Épica | Prioridad |
|----------|-----|-------|-----------|
| US-05    | 5   | E-01  | 1         |
| US-07    | 3   | E-01  | 2         |
| US-06    | 8   | E-02  | 1         |
| US-01    | 3   | E-05  | 1         |

## Notas de selección

- **US-05** (estado en tiempo real) y **US-06** (agendamiento online) son las dos
  historias mejor priorizadas del backlog (E-01 prioridad 1, E-02 prioridad 2) y
  forman el núcleo del Sprint Goal.
- **US-07** depende de **US-06**; como ambas caben dentro de la capacidad, se
  incluyen juntas (US-06 se adelanta en el orden de entrada solo para satisfacer
  esa dependencia, no cambia su prioridad real de backlog).
- **US-01** (E-05, sin dependencias) se agrega para aprovechar la capacidad
  restante (1 pt libre no alcanza para ninguna historia; con 4 pts libres antes
  de sumarla, entra ella en lugar de dejar la capacidad ociosa).

## Historias de mayor prioridad que quedaron afuera (y por qué)

| Historia | Pts | Épica | Motivo |
|----------|-----|-------|--------|
| US-08    | 5   | E-01 (prioridad 3) | No entra por capacidad: 16 pts comprometidos (US-05+US-07+US-06) + 5 = 21 > 20. |
| US-04    | 5   | E-03 | Dependencia (US-06) sí está resuelta, pero no entra por capacidad. |
| US-03    | 5   | E-04 | No entra por capacidad. |
| US-02    | 3   | E-06 | No entra por capacidad (19 + 3 = 22 > 20). |
| US-09    | 8   | E-07 | No entra por capacidad. |
| US-10, US-11, US-12, US-13 | 5, 3, 5, 5 | E-08 | No entran por capacidad. |

Ninguna historia quedó afuera por dependencias sin resolver: todas las
dependencias de las historias comprometidas (US-06 para US-07) están dentro del
mismo sprint.
