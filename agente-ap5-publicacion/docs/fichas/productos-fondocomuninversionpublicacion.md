# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `FondoComunInversionPublicacion`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / FCI`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.FondoComunInversionPublicacion` se llena mediante `Productos_FondoComunInversionPublicacion.dtsx`. La evidencia combina `UPDATE` y `OpenRowset`, indicando mantenimiento e insercion dentro del mismo flujo.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Productos_FondoComunInversionPublicacion.dtsx` | carga principal | recurrente | paquete especifico de FCI publicado |

## Mecanismo tecnico

- Tipo de carga: `update + openrowset`
- Tarea o data flow: publicacion de FCI
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `UPDATE [Productos].[FondoComunInversionPublicacion]`
- Tablas relacionadas: `Productos.FondoComunInversion`, `Productos.Subyacente`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| update | `Productos_FondoComunInversionPublicacion.dtsx` | comando SQL | aparece `UPDATE [Productos].[FondoComunInversionPublicacion]` |
| tabla destino | `Productos_FondoComunInversionPublicacion.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- Existe una separacion clara entre la tabla base y la tabla publicada de FCI.
- El paquete tambien toca `Subyacente`.

## Inferencias

- La tabla concentra la vista orientada a AP5 del instrumento FCI.

## Dudas abiertas

- Como se reparten atributos entre `FondoComunInversion` y `FondoComunInversionPublicacion`.

## Clasificacion final

- Motivo de clasificacion: paquete dedicado con evidencia explicita.
- Riesgo de error: bajo.
- Proxima validacion sugerida: comparar ambas tablas FCI en `Publicacion.sql`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Productos_FondoComunInversionPublicacion.dtsx`
- Fecha de analisis: `2026-08-11`
