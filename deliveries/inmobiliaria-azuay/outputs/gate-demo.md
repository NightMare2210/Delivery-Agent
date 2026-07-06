# Demo del gate `dor-invest-gate.py` — delivery `inmobiliaria-azuay`

Captura: [`gate-demo-screenshot.png`](./gate-demo-screenshot.png) · mockup fuente: [`gate-demo.html`](./gate-demo.html)
(mismo formato usado en la Unidad 1 para el `readiness-gate` del Discovery Agent).

## Qué se hizo

Se coló deliberadamente una historia floja en `backlog.json` (`US-99`, ficticia,
no proviene del `inbox/`) que viola varias reglas de INVEST / Definition of Ready
al mismo tiempo:

```json
{
  "id": "US-99",
  "epic": "E-08",
  "as_a": "gerente / propietaria",
  "want": "un panel moderno y rapido con todo lo importante del negocio",
  "so_that": "tomar mejores decisiones",
  "acceptance_criteria": [],
  "estimate": null,
  "dependencies": ["US-77"],
  "open_questions": ["¿que metricas exactas debe mostrar el panel?"],
  "priority": 5,
  "origin": ["user-stories:US-13"]
}
```

Luego se intentó escribir `outputs/stories.md` (el archivo custodiado por el hook).

## Nota sobre el entorno de esta demo

En esta sesión de trabajo (Claude Code vía chat), las llamadas directas a las
herramientas `Edit`/`Write` no dispararon el hook `PreToolUse` de forma visible
(probablemente por resolución de `$CLAUDE_PROJECT_DIR` en ese contexto de
ejecución). Para no fabricar evidencia, la demo se hizo invocando el propio
hook con el mismo evento JSON que Claude Code le pasa por stdin al escribir
`stories.md` — es el mismo script, la misma verificación contra `backlog.json`,
ejecutado tal cual. En una sesión de terminal local con `claude`, el mismo
bloqueo ocurre automáticamente al correr `/delivery:generate-stories`.

## 1) Bloqueo (backlog con US-99 floja)

Comando:

```bash
echo '{"tool_input":{"file_path":"deliveries/inmobiliaria-azuay/outputs/stories.md"},"cwd":"'"$PWD"'"}' \
  | python3 .claude/hooks/dor-invest-gate.py
echo "exit code: $?"
```

Salida real:

```
dor-invest-gate: BLOQUEADO — el backlog no está listo para el sprint.

  ✗ US-99: sin criterios de aceptación (no es testeable).
  ✗ US-99: sin estimación válida en puntos (no es estimable).
  ✗ US-99: depende de 'US-77', que no existe en el backlog.
  ✗ US-99: tiene preguntas abiertas sin resolver (no está 'ready').
  ✗ US-99: usa un término vago ('un panel moderno y rapido con todo lo importante del negocio') sin criterio medible (no es testeable).

Corrige las historias señaladas (no evadas el gate):
  · formato Como/Quiero/Para completo
  · al menos un criterio de aceptación verificable (testeable)
  · una estimación en puntos > 0 (estimable)
  · tamaño <= 8 pts; si es mayor, divídela (pequeña)
  · sin preguntas abiertas bloqueantes (Definition of Ready)
exit code: 2
```

El gate identificó **las 5 fallas exactas** que se sembraron: sin criterios,
sin estimación, dependencia inexistente, pregunta abierta sin resolver y
término vago sin criterio que lo aterrice. `stories.md` **no se escribió**.

## 2) Resolución (US-99 corregida)

Se corrigió la misma historia para que cumpla INVEST + DoR:

```json
{
  "id": "US-99",
  "epic": "E-08",
  "as_a": "gerente / propietaria",
  "want": "ver en un panel las 3 metricas clave (ventas del mes, visitas agendadas y ofertas rechazadas)",
  "so_that": "tomar decisiones sin pedirle el dato a cada asesor",
  "acceptance_criteria": [
    "Dado que la gerente abre el panel principal, cuando carga, entonces ve ventas del mes, visitas agendadas y ofertas rechazadas actualizadas al dia."
  ],
  "estimate": 3,
  "dependencies": [],
  "open_questions": [],
  "priority": 5,
  "origin": ["user-stories:US-13"]
}
```

Mismo comando, mismo archivo. Salida real:

```
exit code: 0
```

(El hook no escribe nada en `stdout` cuando pasa — es el comportamiento
documentado. `stories.md` habría podido escribirse normalmente.)

## 3) Cierre

`US-99` era una historia sintética solo para esta demo — no proviene del
`inbox/` del caso `inmobiliaria-azuay` (violaría la regla de cero invención
del `CLAUDE.md`), así que se removió de `backlog.json` una vez capturada la
evidencia. El backlog real del delivery quedó intacto: 13 historias, 63
puntos, todas en Definition of Ready.
