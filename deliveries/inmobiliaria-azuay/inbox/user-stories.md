# User Stories — inmobiliaria-azuay

> Generado por `/discovery:generate-mvp`. Fuente única: personas y requisitos de `outputs/`.
> Las historias marcadas **[MVP]** entran en el alcance mínimo del producto.
> El orden refleja prioridad: núcleo de valor primero.

---

## En el MVP

### [US-05] Estado en tiempo real de propiedades — [MVP]

- **Como** cliente comprador, **quiero** ver en el portal si una propiedad está disponible, reservada o vendida en tiempo real, **para** no hacer una visita innecesaria a una propiedad que ya no está libre.
  - Criterios de aceptación:
    - Dado que un asesor cambia el estado de una propiedad en el sistema interno, cuando el cliente visualiza la ficha en el portal, entonces el estado actualizado aparece en menos de 60 segundos.
    - Dado que la propiedad pasa a "reservada", cuando el cliente intenta agendar una visita, entonces el sistema lo informa y no permite avanzar.
    - Dado que la propiedad está marcada como "vendida", cuando el cliente la busca, entonces aparece con ese estado claramente visible y sin opción de contacto.
  - Fuente: `cliente-comprador.md` · R-05, R-14

### [US-06] Agendamiento online de visitas — [MVP]

- **Como** cliente comprador, **quiero** elegir fecha y hora de visita directamente desde el portal, **para** no depender de llamadas ni esperar confirmaciones que tardan hasta un día.
  - Criterios de aceptación:
    - Dado que el cliente selecciona una propiedad disponible, cuando accede a "Agendar visita", entonces ve los horarios disponibles del asesor asignado y puede reservar uno sin hacer ninguna llamada.
    - Dado que el cliente selecciona un horario y confirma, cuando el sistema lo registra, entonces recibe un comprobante en pantalla y el asesor recibe la notificación (US-04).
    - Dado que todos los horarios de un día están ocupados, cuando el cliente lo ve, entonces el sistema le ofrece el siguiente día disponible.
  - Fuente: `cliente-comprador.md` · R-07

### [US-07] Notificación proactiva al cliente — [MVP]

- **Como** cliente comprador, **quiero** recibir un aviso si el estado de una propiedad cambia después de que agendé una visita, **para** no llegar a una propiedad que ya no está disponible.
  - Criterios de aceptación:
    - Dado que el cliente tiene una visita agendada, cuando la propiedad pasa a "reservada" o "vendida", entonces el cliente recibe una notificación proactiva antes de la fecha de la visita.
    - Dado que se envió la notificación, cuando el cliente la recibe, entonces puede cancelar la visita o contactar al asesor desde la misma notificación.
    - Dado que la reserva se cancela y la propiedad vuelve a estar disponible, cuando eso ocurre, entonces el cliente también es notificado.
  - Fuente: `cliente-comprador.md` · R-06

### [US-04] Notificación push al asesor — [MVP]

- **Como** asesor inmobiliario, **quiero** recibir una notificación en mi celular cuando se confirme o cancele una visita en mi agenda, **para** enterarme a tiempo y llegar preparado a cada cita.
  - Criterios de aceptación:
    - Dado que un cliente confirma una visita desde el portal, cuando el sistema la registra, entonces el asesor asignado recibe una notificación push en menos de 60 segundos.
    - Dado que el cliente cancela una visita, cuando el sistema actualiza el estado, entonces el asesor recibe notificación con el detalle de la propiedad y el horario cancelado.
    - Dado que el asesor no tiene habilitadas las notificaciones push, cuando se confirma una visita, entonces el evento queda registrado igualmente y visible en su calendario.
  - Fuente: `asesor-inmobiliario.md` · R-04

### [US-08] Ficha con información mínima obligatoria — [MVP]

- **Como** cliente comprador, **quiero** que todas las fichas de propiedades incluyan metraje real, servicios disponibles y al menos tres fotos de calidad, **para** tomar decisiones informadas sin visitar propiedades que no cumplen mis criterios básicos.
  - Criterios de aceptación:
    - Dado que un asesor intenta publicar una propiedad, cuando no ha cargado metraje, servicios básicos (agua, luz, tipo de calle) o menos de tres fotos, entonces el sistema bloquea la publicación e indica exactamente qué falta.
    - Dado que la ficha está completa con los mínimos, cuando el cliente la ve en el portal, entonces todos los campos obligatorios son visibles sin necesidad de clics adicionales.
    - Dado que el asesor carga tres fotos de resolución aceptable (≥ 800×600 px), cuando las sube, entonces el sistema las acepta y permite publicar.
  - Fuente: `cliente-comprador.md` · R-08

---

## Fuera del MVP — próximas iteraciones

### [US-01] Publicación rápida al recibir fotos

- **Como** asesor inmobiliario, **quiero** tener una propiedad pre-configurada lista para publicarse en un clic al cargar la primera foto, **para** no perder oportunidades cuando el dueño demora en enviar las imágenes.
  - Criterios de aceptación:
    - Dado que la propiedad tiene todos los datos obligatorios excepto fotos, cuando el asesor carga las imágenes mínimas, entonces puede publicarla con un solo clic sin reingresar datos.
    - Dado que la propiedad está en estado "pendiente de foto", cuando el asesor o el dueño carga las imágenes, entonces el sistema notifica al asesor que ya puede publicar.
  - Fuente: `asesor-inmobiliario.md` · R-01

### [US-02] Rechazo automático de ofertas bajo el mínimo

- **Como** asesor inmobiliario, **quiero** que el sistema rechace automáticamente las ofertas que no superen el precio mínimo pactado, **para** evitar conversaciones incómodas cuando la oferta no es viable.
  - Criterios de aceptación:
    - Dado que el cliente envía una oferta menor al precio mínimo de la propiedad, cuando el sistema la recibe, entonces la rechaza automáticamente e informa al cliente el motivo sin intervención del asesor.
    - Dado que la oferta supera el mínimo, cuando el sistema la recibe, entonces la notifica al asesor para que decida.
  - Fuente: `asesor-inmobiliario.md` · R-02

### [US-03] Historial unificado del cliente

- **Como** asesor inmobiliario, **quiero** ver en una sola vista el historial de visitas, ofertas y consultas de cada cliente asignado, **para** entrar a cada reunión ya informado y no hacerle repetir lo mismo dos veces.
  - Criterios de aceptación:
    - Dado que el asesor accede al perfil de un cliente asignado, cuando lo abre, entonces ve el historial cronológico de visitas, ofertas enviadas y consultas previas.
    - Dado que hay una nueva actividad del cliente, cuando ocurre, entonces aparece reflejada en el historial sin necesidad de recargar.
  - Fuente: `asesor-inmobiliario.md` · R-03

### [US-09] Alertas de precio y propiedades nuevas

- **Como** cliente comprador, **quiero** configurar alertas para recibir notificaciones cuando bajen precios o ingresen propiedades que se ajusten a mis criterios, **para** actuar rápido sin revisar el portal constantemente.
  - Criterios de aceptación:
    - Dado que el cliente define criterios de búsqueda (zona, tipo, rango de precio), cuando ingresa una propiedad que los cumple, entonces el cliente recibe una notificación.
    - Dado que el precio de una propiedad marcada como favorita baja, cuando ocurre el cambio, entonces el cliente recibe alerta con el precio anterior y el nuevo.
  - Fuente: `cliente-comprador.md` · R-09

### [US-10] Resumen de rendimiento por asesor

- **Como** gerente / propietaria, **quiero** ver un resumen del rendimiento de cada asesor (visitas realizadas, clientes activos, propiedades sin movimiento), **para** saber quién necesita apoyo sin tener que preguntarles uno por uno.
  - Criterios de aceptación:
    - Dado que la gerente accede al panel de gerencia, cuando lo abre, entonces ve una tabla con cada asesor y sus métricas de la semana y el mes.
    - Dado que un asesor tiene propiedades sin movimiento en más de cuatro semanas, cuando la gerente ve su resumen, entonces esas propiedades están resaltadas.
  - Fuente: `gerente-propietaria.md` · R-10

### [US-11] Vista de carga de asesores para asignación

- **Como** gerente / propietaria, **quiero** ver cuántos clientes activos tiene cada asesor antes de asignar uno nuevo, **para** distribuir la carga de manera equitativa y que ningún cliente quede sin atención.
  - Criterios de aceptación:
    - Dado que la gerente va a asignar un cliente nuevo, cuando abre el formulario de asignación, entonces ve el número de clientes activos de cada asesor en ese momento.
    - Dado que un asesor tiene más del doble de clientes que el de menor carga, cuando se le va a asignar otro, entonces el sistema muestra una advertencia de sobrecarga.
  - Fuente: `gerente-propietaria.md` · R-11

### [US-12] Alerta de propiedades sin actividad

- **Como** gerente / propietaria, **quiero** recibir una alerta automática cuando una propiedad activa lleve más de cuatro semanas sin visitas ni ofertas, **para** actuar antes de que el dueño se moleste por la inactividad.
  - Criterios de aceptación:
    - Dado que una propiedad activa no registra visitas ni ofertas en cuatro semanas, cuando se cumple ese plazo, entonces la gerente recibe una alerta con el nombre de la propiedad y el asesor asignado.
    - Dado que el umbral es configurable, cuando la gerente lo modifica desde la configuración, entonces las alertas futuras respetan el nuevo valor.
  - Fuente: `gerente-propietaria.md` · R-12

### [US-13] Consolidado de ofertas rechazadas

- **Como** gerente / propietaria, **quiero** acceder al historial consolidado de ofertas rechazadas por propiedad, **para** detectar cuándo el precio publicado está lejos del mercado y decidir si ajustarlo.
  - Criterios de aceptación:
    - Dado que la gerente accede al módulo de análisis de precios, cuando lo abre, entonces ve el listado de propiedades con el número de ofertas rechazadas y los montos ofrecidos.
    - Dado que una propiedad acumula tres o más rechazos bajo el mínimo, cuando la gerente la ve, entonces puede comparar el precio mínimo vs. el promedio ofertado.
  - Fuente: `gerente-propietaria.md` · R-13
