# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Forward`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.Forward` se llena mediante `040_Productos.dtsx`. La evidencia relevada combina `DELETE`, `UPDATE` y `OpenRowset`, por lo que el paquete recompone y actualiza la publicacion.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete maestro del esquema |

## Mecanismo tecnico

- Tipo de carga: `delete + update + openrowset`
- Tarea o data flow: carga general de forwards
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `DELETE [Productos].[Forward]`, `UPDATE [Productos].[Forward]`
- Tablas relacionadas: `Productos.ForwardOTC`, `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `040_Productos.dtsx` | comando SQL | aparece `DELETE [Productos].[Forward]` |
| update | `040_Productos.dtsx` | comando SQL | aparece `UPDATE [Productos].[Forward]` |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El forward standard y el OTC siguen patrones parecidos.
- La carga es directa desde el paquete troncal.

## Inferencias

- La tabla representa un subtipo importante dentro del universo de contratos derivados.

## Dudas abiertas

- Si existe separacion funcional entre mercados o segmentos comerciales.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita con operaciones de mantenimiento.
- Riesgo de error: bajo.
- Proxima validacion sugerida: comparar estructura con `ForwardOTC`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
