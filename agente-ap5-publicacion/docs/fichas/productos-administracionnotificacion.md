# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `AdministracionNotificacion`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / Notificaciones`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.AdministracionNotificacion` se llena mediante `Parametros_NotificacionAdministracion.dtsx`. La evidencia es un `OpenRowset` directo al destino, aunque el paquete use prefijo `Parametros`.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Parametros_NotificacionAdministracion.dtsx` | carga principal | recurrente | paquete transversal que tambien toca otras tablas de notificacion |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de administracion de notificaciones
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[AdministracionNotificacion]`
- Tablas relacionadas: `Productos.NotificacionProductos`, `Productos.NotificacionCanales`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Parametros_NotificacionAdministracion.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El paquete es transversal y no estrictamente del esquema `Productos`.
- Tambien actualiza otras tablas del mismo subdominio de notificaciones.

## Inferencias

- La administracion de notificaciones se modela como configuracion publicada compartida.

## Dudas abiertas

- Si el nombre del paquete refleja un dominio historico o una dependencia de catalogos parametrizados.

## Clasificacion final

- Motivo de clasificacion: destino explicito en paquete funcionalmente coherente.
- Riesgo de error: bajo.
- Proxima validacion sugerida: reconstruir la relacion entre las tres tablas de notificacion.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Parametros_NotificacionAdministracion.dtsx`
- Fecha de analisis: `2026-08-11`
