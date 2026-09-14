# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `NotificacionCanales`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / Notificaciones`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.NotificacionCanales` se llena mediante `Parametros_NotificacionAdministracion.dtsx`. La evidencia hallada es un `OpenRowset` directo al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Parametros_NotificacionAdministracion.dtsx` | carga principal | recurrente | paquete transversal del circuito de notificaciones |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de canales de notificacion
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[NotificacionCanales]`
- Tablas relacionadas: `Productos.AdministracionNotificacion`, `Productos.NotificacionProductos`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Parametros_NotificacionAdministracion.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El mismo paquete puebla las tres tablas de notificaciones.
- No se observaron operaciones de mantenimiento extra en la matriz resumida.

## Inferencias

- La tabla representa los canales disponibles o vinculados a cada regla de notificacion.

## Dudas abiertas

- Si existe un catalogo maestro de canales fuera del esquema `Productos`.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita y coherencia funcional con el paquete.
- Riesgo de error: bajo.
- Proxima validacion sugerida: relevar claves y dependencias con las otras tablas de notificacion.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Parametros_NotificacionAdministracion.dtsx`
- Fecha de analisis: `2026-08-11`
