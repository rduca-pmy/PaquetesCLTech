# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `NotificacionProductos`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / Notificaciones`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.NotificacionProductos` se llena mediante `Parametros_NotificacionAdministracion.dtsx`. La evidencia observada es un `OpenRowset` directo a la tabla.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Parametros_NotificacionAdministracion.dtsx` | carga principal | recurrente | paquete transversal del circuito de notificaciones |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de productos asociados a notificaciones
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[NotificacionProductos]`
- Tablas relacionadas: `Productos.AdministracionNotificacion`, `Productos.NotificacionCanales`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Parametros_NotificacionAdministracion.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla se actualiza junto con otras estructuras de notificacion.
- No se detectaron paquetes alternativos.

## Inferencias

- Modela la vinculacion entre configuraciones de notificacion y productos afectados.

## Dudas abiertas

- Si la tabla guarda solo asociaciones activas o tambien historico.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita en paquete transversal.
- Riesgo de error: bajo.
- Proxima validacion sugerida: validar cardinalidad con `AdministracionNotificacion`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Parametros_NotificacionAdministracion.dtsx`
- Fecha de analisis: `2026-08-11`
