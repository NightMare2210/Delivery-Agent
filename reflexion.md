# Reflexión — Agile Delivery Team (`inmobiliaria-azuay`)

## ¿Qué cambió en el plan al separar el trabajo en cuatro roles en vez de pensarlo "todo junto"?

Pensar "todo junto" tiende a resolver primero lo que es técnicamente cómodo,
no lo que aporta más valor. Separar en cuatro roles obligó a pasar por cuatro
preguntas distintas antes de llegar al código: el Product Owner priorizó las
épicas por impacto en el negocio (menos visitas en vano, agendamiento sin
teléfono) antes de que existiera una sola línea de arquitectura; el Developer
recién después tradujo esas épicas a historias con criterios verificables; el
Architect decidió la estructura (monolito modular por dominios, polling en vez
de WebSockets para el estado en tiempo real, eventos de dominio para
notificaciones) una vez que ya había un backlog priorizado que sostener, no
antes; y el Scrum Master cerró el ciclo verificando que el compromiso del
sprint no superara la capacidad real del equipo. Cada rol actúa como un check
sobre el anterior — el PO no puede inflar valor sin evidencia del `inbox/`, el
Developer no puede declarar "lista" una historia sin criterios, el Architect
no puede diseñar sin épicas que lo justifiquen. Sin esa separación, es fácil
que una sola persona (o un solo prompt) mezcle "qué construir" con "cómo
construirlo" y termine optimizando la solución más fácil de programar en vez
de la que resuelve el problema real del cliente o del asesor.

## ¿Qué historia costó más dejar lista según INVEST, y por qué?

**US-06 · Agendamiento online de visitas** (8 puntos, el máximo permitido por
`DELIVERY_MAX_POINTS`). Costó por dos razones distintas. Primero, tamaño: la
historia original del `inbox/` mezclaba cuatro comportamientos en uno —ver
horarios disponibles, confirmar una reserva, reofertar el siguiente día si no
hay cupo, y resolver a qué asesor pertenecen los horarios mostrados—. Partirla
hubiera sido la salida fácil, pero las cuatro ramas son parte indivisible del
mismo flujo de reserva y cada una ya tenía un criterio de aceptación propio y
verificable, así que dividir habría sido trocear por trocear, no por valor
independiente. Segundo, tenía una pregunta abierta real: si el cliente elige
el asesor o el sistema lo asigna cuando hay más de uno para la misma
propiedad. No estaba en ningún documento del `inbox/` de forma explícita, y
la regla de cero invención impide inventar una respuesta. Se resolvió con
evidencia indirecta (`personas.md` describe que cada asesor gestiona su
propia cartera, y `user-stories.md` ya habla de "el asesor asignado" en
singular), lo que permitió cerrar la Definition of Ready sin agregar un
requisito que el descubrimiento no respaldaba. Ese fue el patrón más
incómodo del ejercicio: distinguir entre una historia grande pero cohesiva
(no se parte) y una historia con una laguna real de información (se cierra
con evidencia, no con invención).

## ¿Para qué te serviría un gate de Definition of Ready en tu equipo real?

Para lo mismo que resolvió acá: dejar de confiar en que alguien *diga* que
una historia está lista y verificarlo contra datos estructurados antes de que
entre al sprint. En un equipo real, la presión de cerrar la planificación a
tiempo empuja a aceptar historias con criterios vagos ("mejorar el
rendimiento", "una UI más amigable") o con estimaciones puestas al voleo
porque "ya se sabrá en el sprint". Un gate automatizado como
`dor-invest-gate.py` no reemplaza el criterio humano del Scrum Master, pero
le saca el trabajo mecánico y "silencioso" de encima: bloquea antes de que la
historia llegue al compromiso del sprint, señala exactamente qué falta (no
"está incompleta", sino "sin criterios", "depende de un ID que no existe",
"término vago sin criterio medible"), y no se puede evadir escribiendo el
archivo con otro nombre porque el hook vigila el contenido, no la ceremonia.
La demo de este ejercicio lo mostró en la práctica: una historia con cinco
fallas distintas fue rechazada con las cinco señaladas una por una, y la
misma historia corregida pasó sin fricción. Esa es la diferencia entre
"la Definition of Ready es un documento que leemos" y "la Definition of
Ready es una puerta que el sistema hace cumplir".
