# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Contribucion_Cancelacion_Publicacion`
- Esquema inferido: `Contribucion`
- Objeto inferido: `Cancelacion`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

La funcion CDC publica cambios de `Contribucion.Cancelacion` desde PBP. En AP5 existe la tabla homonima `Contribucion.Cancelacion` y el procedimiento `Contribucion.MergeCancelacion`, por lo que el mapeo es directo.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Contribucion_Cancelacion_Publicacion` | funcion activa o no validada |
| tabla CT | `cdc.Contribucion_Cancelacion_CT` | fuente CDC observada |
| tabla PBP | `Contribucion.Cancelacion` | tabla base del circuito |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Contribucion.Cancelacion` | destino directo | alta | existe tabla homonima en `Publicacion.sql` |
| `Contribucion.MergeCancelacion` | procedimiento receptor candidato | alta | parsea JSON y hace `MERGE` contra `Contribucion.Cancelacion` |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | lee `cdc.Contribucion_Cancelacion_CT` |
| enriquecimiento | `Clearing.sql` | une con `Personas.CuentaRegistro`, `Productos.vContrato` y `Sistema.EstadoCancelacionManual` |
| procedimiento AP5 | `Publicacion.sql` | existe `Contribucion.MergeCancelacion` |
| tabla AP5 | `Publicacion.sql` | existe `Contribucion.Cancelacion` |

## Hechos observados

- La tabla AP5 tiene el mismo esquema y objeto que la funcion CDC infiere.
- El procedimiento AP5 usa `OPENJSON` y `MERGE`, consistente con un payload de publicacion.

## Inferencias

- El flujo probable es `Clearing.Contribucion.Cancelacion -> cdc.fn_cdc_get_Contribucion_Cancelacion_Publicacion -> Contribucion.MergeCancelacion -> Publicacion.Contribucion.Cancelacion`.

## Dudas abiertas

- Confirmar el servicio o job que transporta el JSON desde CDC hasta AP5.
- Validar si el paquete SSIS participa tambien en alguna recomposicion.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-primer-tanda.csv`
- Fecha de analisis: `2026-08-27`
