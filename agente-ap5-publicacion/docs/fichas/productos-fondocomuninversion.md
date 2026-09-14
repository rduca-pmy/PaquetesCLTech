# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `FondoComunInversion`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / FCI`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.FondoComunInversion` se llena mediante `Productos_FondoComunInversion.dtsx`. La evidencia observada es un `OpenRowset` directo al destino, y el paquete tambien toca `Subyacente`.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Productos_FondoComunInversion.dtsx` | carga principal | recurrente | paquete especifico de FCI |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga base de FCI
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[FondoComunInversion]`
- Tablas relacionadas: `Productos.FondoComunInversionPublicacion`, `Productos.Subyacente`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Productos_FondoComunInversion.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- Hay separacion entre la tabla base FCI y su version de publicacion.
- El paquete parece cubrir el maestro base.

## Inferencias

- AP5 mantiene un nivel base y otro publicado del instrumento FCI.

## Dudas abiertas

- Cuales columnas distinguen ambos niveles de representacion.

## Clasificacion final

- Motivo de clasificacion: paquete dedicado con destino explicito.
- Riesgo de error: bajo.
- Proxima validacion sugerida: comparar su estructura con `FondoComunInversionPublicacion`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Productos_FondoComunInversion.dtsx`
- Fecha de analisis: `2026-08-11`
