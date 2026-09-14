# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ActivoPublicacionMoneda`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.ActivoPublicacionMoneda` se llena mediante `Activos_ActivoPublicacionMoneda.dtsx`. La evidencia observada es un `OpenRowset` directo al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Activos_ActivoPublicacionMoneda.dtsx` | carga principal | recurrente | paquete especifico para monedas asociadas al activo publicado |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de monedas por activo publicado
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Activos].[ActivoPublicacionMoneda]`
- Tablas relacionadas: `Activos.ActivoPublicacion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Activos_ActivoPublicacionMoneda.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla tiene un paquete exclusivo.
- No se observaron operaciones de borrado o update en la evidencia resumida.

## Inferencias

- La tabla expone monedas habilitadas o asociadas a cada activo publicado.

## Dudas abiertas

- Si la multiplicidad responde a moneda de liquidacion, cotizacion o ambas.

## Clasificacion final

- Motivo de clasificacion: paquete dedicado con destino explicito.
- Riesgo de error: bajo.
- Proxima validacion sugerida: relevar columnas para distinguir el tipo de asociacion monetaria.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Activos_ActivoPublicacionMoneda.dtsx`
- Fecha de analisis: `2026-08-11`
