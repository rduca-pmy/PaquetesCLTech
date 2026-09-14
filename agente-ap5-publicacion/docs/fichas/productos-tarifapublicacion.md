# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `TarifaPublicacion`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / Tarifas`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.TarifaPublicacion` se llena mediante `Productos_TarifaPublicacion.dtsx`. La evidencia observada es un `OpenRowset` directo a la tabla destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Productos_TarifaPublicacion.dtsx` | carga principal | recurrente | paquete especifico para la publicacion de tarifas |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: publicacion de tarifas
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[TarifaPublicacion]`
- Tablas relacionadas: `Productos.TarifaDevengada`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Productos_TarifaPublicacion.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla tiene un job dedicado y simple.
- No se observaron operaciones de mantenimiento adicionales en la evidencia resumida.

## Inferencias

- AP5 expone una tabla final de tarifas separada del circuito de devengamiento.

## Dudas abiertas

- Como se integra esta publicacion con `TarifaDevengada`.

## Clasificacion final

- Motivo de clasificacion: paquete especializado con destino explicito.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar si consume directamente una stage o una vista consolidada.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Productos_TarifaPublicacion.dtsx`
- Fecha de analisis: `2026-08-11`
