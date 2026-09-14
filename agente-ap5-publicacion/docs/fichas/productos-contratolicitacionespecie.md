# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ContratoLicitacionEspecie`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / Licitaciones`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.ContratoLicitacionEspecie` se llena mediante `991_Licitacion.dtsx`. La evidencia muestra `DELETE`, `UPDATE` y `OpenRowset`, con una relacion directa entre el paquete de licitaciones y la tabla destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `991_Licitacion.dtsx` | carga principal | recurrente | paquete especializado en licitaciones |

## Mecanismo tecnico

- Tipo de carga: `delete + update + openrowset`
- Tarea o data flow: carga de especies por licitacion
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `DELETE [Productos].[ContratoLicitacionEspecie]`, `UPDATE [Productos].[ContratoLicitacionEspecie]`
- Tablas relacionadas: `Productos.Licitacion`, `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `991_Licitacion.dtsx` | comando SQL | aparece `DELETE [Productos].[ContratoLicitacionEspecie]` |
| update | `991_Licitacion.dtsx` | comando SQL | aparece `UPDATE [Productos].[ContratoLicitacionEspecie]` |
| tabla destino | `991_Licitacion.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El mismo paquete tambien llena `Productos.Licitacion`.
- La tabla expresa un cruce entre contrato y especie de licitacion.

## Inferencias

- La tabla materializa el detalle publicable de instrumentos incluidos en una licitacion.

## Dudas abiertas

- Si existe granularidad adicional por tramo o estado de licitacion.

## Clasificacion final

- Motivo de clasificacion: paquete dedicado con evidencia completa.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar llaves y cardinalidad con `Licitacion`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `991_Licitacion.dtsx`
- Fecha de analisis: `2026-08-11`
