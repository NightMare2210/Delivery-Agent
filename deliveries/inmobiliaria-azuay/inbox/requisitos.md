# Requisitos candidatos — inmobiliaria-azuay

> Generado por `/discovery:analyze`. Fuente única: entrevistas en `interviews/`.

---

## Funcionales

- **[R-01]** El sistema debe permitir preparar una propiedad para publicación inmediata, de modo que al cargar la primera imagen se active con un solo clic sin reingreso de datos.
  - Tipo: funcional
  - Origen: `asesor-inmobiliario.md` · Asesor Inmobiliario

- **[R-02]** El sistema debe rechazar automáticamente las ofertas que no superen el precio mínimo pactado con el propietario, sin intervención manual del asesor.
  - Tipo: funcional
  - Origen: `asesor-inmobiliario.md` · Asesor Inmobiliario

- **[R-03]** El sistema debe mostrar un historial unificado de cada cliente (visitas, ofertas, consultas) accesible al asesor asignado en una sola vista.
  - Tipo: funcional
  - Origen: `asesor-inmobiliario.md` · Asesor Inmobiliario

- **[R-04]** El sistema debe enviar una notificación push al celular del asesor cuando se confirme o cancele una visita en su agenda.
  - Tipo: funcional
  - Origen: `asesor-inmobiliario.md` · Asesor Inmobiliario

- **[R-05]** El sistema debe mostrar en tiempo real el estado de cada propiedad (disponible / reservada / vendida) en el portal público.
  - Tipo: funcional
  - Origen: `cliente-comprador.md` · Cliente Comprador

- **[R-06]** El sistema debe notificar proactivamente al cliente si el estado de una propiedad cambia después de que agendó una visita.
  - Tipo: funcional
  - Origen: `cliente-comprador.md` · Cliente Comprador

- **[R-07]** El sistema debe permitir al cliente seleccionar fecha y hora de visita directamente desde el portal, sin necesidad de llamar a la inmobiliaria.
  - Tipo: funcional
  - Origen: `cliente-comprador.md` · Cliente Comprador

- **[R-08]** La ficha de propiedad debe exigir campos mínimos obligatorios para publicarse: metraje real, servicios disponibles (agua, luz, tipo de calle) y al menos tres fotos de calidad.
  - Tipo: funcional
  - Origen: `cliente-comprador.md` · Cliente Comprador

- **[R-09]** El sistema debe permitir al cliente configurar alertas para recibir notificaciones cuando baje el precio o ingresen nuevas propiedades que coincidan con sus criterios de búsqueda.
  - Tipo: funcional
  - Origen: `cliente-comprador.md` · Cliente Comprador

- **[R-10]** El sistema debe proveer a la gerente un resumen del rendimiento de cada asesor: visitas realizadas, clientes activos y propiedades sin movimiento reciente.
  - Tipo: funcional
  - Origen: `gerente-propietaria.md` · Gerente / Propietaria

- **[R-11]** El sistema debe mostrar el número de clientes activos por asesor para facilitar la distribución de carga al asignar un cliente nuevo.
  - Tipo: funcional
  - Origen: `gerente-propietaria.md` · Gerente / Propietaria

- **[R-12]** El sistema debe generar una alerta automática cuando una propiedad activa supere un umbral configurable de semanas sin visitas ni ofertas.
  - Tipo: funcional
  - Origen: `gerente-propietaria.md` · Gerente / Propietaria

- **[R-13]** El sistema debe consolidar el historial de ofertas rechazadas por propiedad y hacerlo accesible para análisis de precios fuera de mercado.
  - Tipo: funcional
  - Origen: `gerente-propietaria.md` · Gerente / Propietaria

---

## No funcionales

- **[R-14]** El estado de una propiedad debe reflejarse en el portal público con una latencia máxima de 60 segundos tras el cambio en el sistema interno.
  - Tipo: no funcional (rendimiento)
  - Origen: `cliente-comprador.md` · Cliente Comprador

- **[R-15]** La plataforma pública debe presentar fichas con información completa y fotos de calidad, proyectando imagen profesional de la inmobiliaria ante el cliente.
  - Tipo: no funcional (usabilidad / imagen de marca)
  - Origen: `gerente-propietaria.md` · Gerente / Propietaria
