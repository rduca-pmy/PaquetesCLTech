# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Licitacion`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / Licitaciones`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.Licitacion` se llena mediante `991_Licitacion.dtsx`. La evidencia incluye `DELETE`, `UPDATE` y `OpenRowset`, por lo que la publicacion se recompone y actualiza dentro del mismo job.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `991_Licitacion.dtsx` | carga principal | recurrente | paquete especializado del subdominio |

## Mecanismo tecnico

- Tipo de carga: `delete + update + openrowset`
- Tarea o data flow: carga de licitaciones
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `DELETE [Productos].[Licitacion]`, `UPDATE [Productos].[Licitacion]`
- Tablas relacionadas: `Productos.ContratoLicitacionEspecie`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `991_Licitacion.dtsx` | comando SQL | aparece `DELETE [Productos].[Licitacion]` |
| update | `991_Licitacion.dtsx` | comando SQL | aparece `UPDATE [Productos].[Licitacion]` |
| tabla destino | `991_Licitacion.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El paquete es exclusivo del subdominio licitaciones.
- La tabla es un maestro publicado, no una simple auxiliar.

## Inferencias

- La licitacion se publica junto con su detalle de especies y contratos.

## Dudas abiertas

- Si el paquete maneja historico o solo estado vigente.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita con mantenimiento visible.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar filtros temporales del paquete.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `991_Licitacion.dtsx`
- Fecha de analisis: `2026-08-11`
