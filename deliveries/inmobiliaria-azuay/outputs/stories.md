# Historias refinadas — Delivery `inmobiliaria-azuay`

> Generado por el Developer a partir de `outputs/backlog.json` (PO) y `inbox/`
> (mvp-canvas.md, user-stories.md, requisitos.md, personas.md, evidence-map.json).
> Las 13 historias candidatas pasaron por refinamiento INVEST. Ninguna superó los
> 8 pts (`DELIVERY_MAX_POINTS`), por lo que no fue necesario partir historias.
> Las 6 que tenían `open_questions` se cerraron con evidencia indirecta del inbox
> (ver "Decisión de refinamiento" en cada una); no se inventó ningún requisito nuevo.

**Total del backlog:** 13 historias · **63 puntos** · todas en Definition of Ready.

| Épica | Historias | Puntos |
|---|---|---|
| E-01 · Menos visitas en vano | US-05, US-07, US-08 | 13 |
| E-02 · Agendamiento sin teléfono | US-06 | 8 |
| E-03 · Asesor preparado a tiempo | US-04 | 5 |
| E-04 · Historial unificado del cliente | US-03 | 5 |
| E-05 · Publicación rápida al recibir fotos | US-01 | 3 |
| E-06 · Rechazo automático de ofertas | US-02 | 3 |
| E-07 · Alertas de precio y propiedades | US-09 | 8 |
| E-08 · Visibilidad operativa para la gerencia | US-10, US-11, US-12, US-13 | 18 |

---

### US-05 · Estado en tiempo real de propiedades   ·   épica E-01   ·   5 pts
**Como** cliente comprador, **quiero** ver en el portal si una propiedad está
disponible, reservada o vendida en tiempo real, **para** no hacer una visita
innecesaria a una propiedad que ya no está libre.

Criterios de aceptación (Gherkin):
- Dado que un asesor cambia el estado de una propiedad en el sistema interno, cuando el cliente visualiza la ficha en el portal, entonces el estado actualizado aparece en menos de 60 segundos.
- Dado que la propiedad pasa a "reservada", cuando el cliente intenta agendar una visita, entonces el sistema lo informa y no permite avanzar.
- Dado que la propiedad está marcada como "vendida", cuando el cliente la busca, entonces aparece con ese estado claramente visible y sin opción de contacto.

Dependencias: ninguna.

Origen: `user-stories:US-05` · `requisitos:R-05, R-14` · `personas:estado-propiedad-no-real-time`

---

### US-07 · Notificación proactiva de cambio de estado al cliente   ·   épica E-01   ·   3 pts
**Como** cliente comprador, **quiero** recibir un aviso si el estado de una
propiedad cambia después de que agendé una visita, **para** no llegar a una
propiedad que ya no está disponible.

Criterios de aceptación (Gherkin):
- Dado que el cliente tiene una visita agendada, cuando la propiedad pasa a "reservada" o "vendida", entonces el cliente recibe una notificación proactiva antes de la fecha de la visita.
- Dado que se envió la notificación, cuando el cliente la recibe, entonces puede cancelar la visita o contactar al asesor desde la misma notificación.
- Dado que la reserva se cancela y la propiedad vuelve a estar disponible, cuando eso ocurre, entonces el cliente también es notificado.

Dependencias: US-06 (requiere que exista una visita agendada desde el portal).

Origen: `user-stories:US-07` · `requisitos:R-06` · `personas:visita-sin-aviso-de-reserva`

---

### US-08 · Ficha con mínimos obligatorios (metraje, servicios, fotos)   ·   épica E-01   ·   5 pts
**Como** cliente comprador, **quiero** que todas las fichas de propiedades
incluyan metraje real, servicios disponibles y al menos tres fotos de calidad,
**para** tomar decisiones informadas sin visitar propiedades que no cumplen mis
criterios básicos.

Criterios de aceptación (Gherkin):
- Dado que un asesor intenta publicar una propiedad, cuando no ha cargado metraje, servicios básicos (agua, luz, tipo de calle) o menos de tres fotos, entonces el sistema bloquea la publicación e indica exactamente qué falta.
- Dado que la ficha está completa con los mínimos, cuando el cliente la ve en el portal, entonces todos los campos obligatorios son visibles sin necesidad de clics adicionales.
- Dado que el asesor carga tres fotos de resolución aceptable (≥ 800×600 px), cuando las sube, entonces el sistema las acepta y permite publicar.
- Dado que las tres fotos cumplen la resolución mínima (≥ 800×600 px), cuando el sistema las valida, entonces la aprobación es automática y no requiere revisión manual.

Dependencias: ninguna.

**Decisión de refinamiento:** el inbox (user-stories.md, requisitos R-08/R-15) no
menciona ningún proceso de revisión manual de fotos; la única validación de
calidad especificada es la resolución mínima. Se define la validación como
100 % automática por resolución para el alcance de este MVP; una revisión
manual sería un requisito nuevo, no una ampliación de esta historia.

Origen: `user-stories:US-08` · `requisitos:R-08, R-15` · `personas:informacion-incompleta-y-engañosa`

---

### US-06 · Agendamiento online de visitas   ·   épica E-02   ·   8 pts
**Como** cliente comprador, **quiero** elegir fecha y hora de visita
directamente desde el portal, **para** no depender de llamadas ni esperar
confirmaciones que tardan hasta un día.

Criterios de aceptación (Gherkin):
- Dado que el cliente selecciona una propiedad disponible, cuando accede a "Agendar visita", entonces ve los horarios disponibles del asesor asignado y puede reservar uno sin hacer ninguna llamada.
- Dado que el cliente selecciona un horario y confirma, cuando el sistema lo registra, entonces recibe un comprobante en pantalla y el asesor recibe la notificación (US-04).
- Dado que todos los horarios de un día están ocupados, cuando el cliente lo ve, entonces el sistema le ofrece el siguiente día disponible.
- Dado que cada propiedad tiene un único asesor responsable de su publicación, cuando el cliente agenda una visita, entonces el sistema muestra únicamente los horarios de ese asesor.

Dependencias: US-05 (el cliente solo puede agendar sobre una propiedad cuyo estado en tiempo real esté disponible).

**Decisión de refinamiento:** se resolvió con evidencia indirecta si el cliente
elige el asesor o el sistema lo asigna cuando hay varios asesores para la
misma propiedad. `personas.md` describe que cada asesor gestiona su propia
cartera de 15-20 propiedades activas, y el criterio original de
`user-stories.md` ya habla de "el asesor asignado" en singular. No hay
evidencia en el inbox de que una propiedad pueda tener más de un asesor
simultáneamente, por lo que el escenario de selección entre varios asesores
no aplica al alcance descrito.

Nota de tamaño: 8 pts es el máximo permitido (`DELIVERY_MAX_POINTS`); no se
divide porque las 4 ramas (ver horarios, confirmar, reofertar día siguiente,
resolución de asesor único) son parte indivisible del mismo flujo de reserva
y ya están cubiertas por criterios verificables independientes.

Origen: `user-stories:US-06` · `requisitos:R-07` · `personas:agendamiento-visita-por-telefono`

---

### US-04 · Notificación push al asesor   ·   épica E-03   ·   5 pts
**Como** asesor inmobiliario, **quiero** recibir una notificación en mi
celular cuando se confirme o cancele una visita en mi agenda, **para**
enterarme a tiempo y llegar preparado a cada cita.

Criterios de aceptación (Gherkin):
- Dado que un cliente confirma una visita desde el portal, cuando el sistema la registra, entonces el asesor asignado recibe una notificación push en menos de 60 segundos.
- Dado que el cliente cancela una visita, cuando el sistema actualiza el estado, entonces el asesor recibe notificación con el detalle de la propiedad y el horario cancelado.
- Dado que el asesor no tiene habilitadas las notificaciones push, cuando se confirma una visita, entonces el evento queda registrado igualmente y visible en su calendario.

Dependencias: US-06 (no hay visita que notificar sin agendamiento online).

Origen: `user-stories:US-04` · `requisitos:R-04` · `personas:notificaciones-visitas-tardias`

---

### US-03 · Historial unificado del cliente para el asesor   ·   épica E-04   ·   5 pts
**Como** asesor inmobiliario, **quiero** ver en una sola vista el historial de
visitas, ofertas y consultas de cada cliente asignado, **para** entrar a cada
reunión ya informado y no hacerle repetir lo mismo dos veces.

Criterios de aceptación (Gherkin):
- Dado que el asesor accede al perfil de un cliente asignado, cuando lo abre, entonces ve el historial cronológico de visitas, ofertas enviadas y consultas previas.
- Dado que hay una nueva actividad del cliente, cuando ocurre, entonces aparece reflejada en el historial sin necesidad de recargar la vista.

Dependencias: ninguna.

**Decisión de refinamiento:** se resolvió si el historial debe actualizarse en
tiempo real (push) o basta con recargar la vista. El propio criterio de
aceptación original ("aparece reflejada en el historial sin necesidad de
recargar") ya exige actualización automática sin refresco manual del
usuario. No se especifica el mecanismo técnico exacto (push vs. polling en
el backend), pero el comportamiento observable requerido queda definido y
es testeable con ese criterio.

Origen: `user-stories:US-03` · `requisitos:R-03` · `personas:historial-cliente-disperso`

---

### US-01 · Publicación rápida al recibir fotos   ·   épica E-05   ·   3 pts
**Como** asesor inmobiliario, **quiero** tener una propiedad pre-configurada
lista para publicarse en un clic al cargar la primera foto, **para** no
perder oportunidades cuando el dueño demora en enviar las imágenes.

Criterios de aceptación (Gherkin):
- Dado que la propiedad tiene todos los datos obligatorios excepto fotos, cuando el asesor carga las imágenes mínimas, entonces puede publicarla con un solo clic sin reingresar datos.
- Dado que la propiedad está en estado "pendiente de foto", cuando el asesor o el dueño carga las imágenes, entonces el sistema notifica al asesor que ya puede publicar.

Dependencias: ninguna.

Origen: `user-stories:US-01` · `requisitos:R-01` · `personas:fotos-pendientes-bloquean-publicacion`

---

### US-02 · Rechazo automático de ofertas bajo el mínimo   ·   épica E-06   ·   3 pts
**Como** asesor inmobiliario, **quiero** que el sistema rechace
automáticamente las ofertas que no superen el precio mínimo pactado, **para**
evitar conversaciones incómodas cuando la oferta no es viable.

Criterios de aceptación (Gherkin):
- Dado que el cliente envía una oferta menor al precio mínimo de la propiedad, cuando el sistema la recibe, entonces la rechaza automáticamente e informa al cliente el motivo sin intervención del asesor.
- Dado que la oferta supera el mínimo, cuando el sistema la recibe, entonces la notifica al asesor para que decida.
- Dado que el precio mínimo pactado es un campo obligatorio del registro de la propiedad, cuando el asesor intenta publicar la propiedad sin ese campo, entonces el sistema no permite publicarla.

Dependencias: ninguna.

**Decisión de refinamiento:** se resolvió si el precio mínimo pactado es un
campo de la ficha o un módulo aparte. `mvp-canvas.md` enumera exactamente 5
funcionalidades mínimas del MVP y ninguna es un módulo de precios; R-02
menciona el "precio mínimo pactado con el propietario" en el mismo contexto
que los demás campos obligatorios de la ficha (R-08). Se define como campo
obligatorio del registro de la propiedad, por ausencia de evidencia de un
módulo separado.

Origen: `user-stories:US-02` · `requisitos:R-02` · `personas:ofertas-bajo-minimo-sin-filtro`

---

### US-09 · Alertas de precio y nuevas propiedades   ·   épica E-07   ·   8 pts
**Como** cliente comprador, **quiero** configurar alertas para recibir
notificaciones cuando bajen precios o ingresen propiedades que se ajusten a
mis criterios, **para** actuar rápido sin revisar el portal constantemente.

Criterios de aceptación (Gherkin):
- Dado que el cliente define criterios de búsqueda (zona, tipo, rango de precio), cuando ingresa una propiedad que los cumple, entonces el cliente recibe una notificación.
- Dado que el precio de una propiedad marcada como favorita baja, cuando ocurre el cambio, entonces el cliente recibe alerta con el precio anterior y el nuevo.

Dependencias: ninguna (funcionalmente se apoya en la adopción de E-02, pero no depende técnicamente de ninguna historia del backlog).

Origen: `user-stories:US-09` · `requisitos:R-09` · `mvp-canvas:fuera-de-alcance:alertas-precio`

---

### US-10 · Resumen de rendimiento por asesor   ·   épica E-08   ·   5 pts
**Como** gerente / propietaria, **quiero** ver un resumen del rendimiento de
cada asesor (visitas realizadas, clientes activos, propiedades sin
movimiento), **para** saber quién necesita apoyo sin tener que preguntarles
uno por uno.

Criterios de aceptación (Gherkin):
- Dado que la gerente accede al panel de gerencia, cuando lo abre, entonces ve una tabla con cada asesor y sus métricas de la semana y el mes.
- Dado que un asesor tiene propiedades sin movimiento en más de cuatro semanas, cuando la gerente ve su resumen, entonces esas propiedades están resaltadas.

Dependencias: ninguna.

Origen: `user-stories:US-10` · `requisitos:R-10` · `personas:visibilidad-rendimiento-asesores`

---

### US-11 · Vista de carga de asesores para asignación   ·   épica E-08   ·   3 pts
**Como** gerente / propietaria, **quiero** ver cuántos clientes activos tiene
cada asesor antes de asignar uno nuevo, **para** distribuir la carga de
manera equitativa y que ningún cliente quede sin atención.

Criterios de aceptación (Gherkin):
- Dado que la gerente va a asignar un cliente nuevo, cuando abre el formulario de asignación, entonces ve el número de clientes activos de cada asesor en ese momento.
- Dado que un asesor tiene más del doble de clientes que el de menor carga, cuando se le va a asignar otro, entonces el sistema muestra una advertencia de sobrecarga.

Dependencias: ninguna.

Origen: `user-stories:US-11` · `requisitos:R-11` · `personas:asignacion-clientes-sin-vista-de-carga`

---

### US-12 · Alerta de propiedades sin actividad   ·   épica E-08   ·   5 pts
**Como** gerente / propietaria, **quiero** recibir una alerta automática
cuando una propiedad activa lleve más de cuatro semanas sin visitas ni
ofertas, **para** actuar antes de que el dueño se moleste por la
inactividad.

Criterios de aceptación (Gherkin):
- Dado que una propiedad activa no registra visitas ni ofertas en cuatro semanas, cuando se cumple ese plazo, entonces la gerente recibe una alerta con el nombre de la propiedad y el asesor asignado.
- Dado que el umbral es configurable, cuando la gerente lo modifica desde la configuración, entonces las alertas futuras respetan el nuevo valor.
- Dado que el umbral de semanas sin actividad es un valor único para toda la inmobiliaria, cuando la gerente lo configura, entonces aplica por igual a todas las propiedades y asesores.

Dependencias: ninguna.

**Decisión de refinamiento:** se resolvió si el umbral configurable es global
o segmentable por tipo de propiedad/asesor. Ni `requisitos.md` (R-12) ni
`user-stories.md` mencionan segmentación; la redacción siempre usa "un
umbral configurable" en singular. Se define como configuración global única,
por ausencia de evidencia de segmentación.

Origen: `user-stories:US-12` · `requisitos:R-12` · `personas:propiedades-inactivas-sin-alerta`

---

### US-13 · Consolidado de ofertas rechazadas   ·   épica E-08   ·   5 pts
**Como** gerente / propietaria, **quiero** acceder al historial consolidado
de ofertas rechazadas por propiedad, **para** detectar cuándo el precio
publicado está lejos del mercado y decidir si ajustarlo.

Criterios de aceptación (Gherkin):
- Dado que la gerente accede al módulo de análisis de precios, cuando lo abre, entonces ve el listado de propiedades con el número de ofertas rechazadas y los montos ofrecidos.
- Dado que una propiedad acumula tres o más rechazos bajo el mínimo, cuando la gerente la ve, entonces puede comparar el precio mínimo vs. el promedio ofertado.

Dependencias: US-02 (solo hay ofertas rechazadas que consolidar si existe el rechazo automático bajo el mínimo).

**Decisión de refinamiento:** se resolvió si el umbral de "tres o más
rechazos" es una regla de negocio fija o solo ilustrativa. El valor aparece
de forma idéntica en `user-stories.md` y fue trasladado sin cambios al
backlog; se toma como el umbral operativo por defecto del criterio de
resaltado del MVP, ajustable en el futuro por la gerencia si la operación
real lo amerita.

Origen: `user-stories:US-13` · `requisitos:R-13` · `personas:ofertas-rechazadas-sin-consolidar`
