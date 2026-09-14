# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ActivoPublicacion`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.ActivoPublicacion` se llena mediante `700_ActivosPublicacion.dtsx`. La evidencia encontrada muestra un `OpenRowset` directo al destino, lo que deja clara la relacion entre el job y la tabla publicada en AP5.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `700_ActivosPublicacion.dtsx` | carga principal | recurrente | paquete dedicado a la publicacion de activos |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: publicacion de activos
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Activos].[ActivoPublicacion]`
- Tablas relacionadas: `Activos.Activo`, `Activos.ActivoPublicacionMoneda`, `Activos.ActivoPublicacionFinalidad`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `700_ActivosPublicacion.dtsx` | componente destino | `OpenRowset` apunta a `[Activos].[ActivoPublicacion]` |

## Hechos observados

- El paquete es especifico de publicacion de activos.
- La tabla figura como destino explicito.

## Inferencias

- `ActivoPublicacion` funciona como tabla de salida orientada a consumo en AP5.

## Dudas abiertas

- Que campos provienen directamente de `Activos.Activo` y cuales se enriquecen en el flujo.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita y paquete especializado.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar el layout de columnas del data flow del paquete `700`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `700_ActivosPublicacion.dtsx`
- Fecha de analisis: `2026-08-11`
