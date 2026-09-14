# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `AvalPublicacion`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.AvalPublicacion` se llena mediante `Activos_AvalPublicacion.dtsx`. La evidencia relevada muestra un `OpenRowset` directo al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Activos_AvalPublicacion.dtsx` | carga principal | recurrente | paquete especifico para publicacion de avales |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: publicacion de avales
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Activos].[AvalPublicacion]`
- Tablas relacionadas: `Activos.ActivoPublicacion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Activos_AvalPublicacion.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La relacion paquete-tabla es directa.
- No se observaron otros paquetes compitiendo por el mismo destino.

## Inferencias

- `AvalPublicacion` expone en AP5 informacion de avales ligada a instrumentos o cuentas del dominio de activos.

## Dudas abiertas

- Cual es el origen puntual del concepto de aval en `Clearing`.

## Clasificacion final

- Motivo de clasificacion: paquete especializado con destino explicito.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar la tabla origen o vista fuente en `Clearing.sql`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Activos_AvalPublicacion.dtsx`
- Fecha de analisis: `2026-08-11`
