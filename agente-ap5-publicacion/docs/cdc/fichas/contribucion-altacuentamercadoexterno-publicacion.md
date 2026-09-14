# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Contribucion_AltaCuentaMercadoExterno_Publicacion`
- Esquema inferido: `Contribucion`
- Objeto inferido: `AltaCuentaMercadoExterno`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

La funcion CDC publica cambios de `Contribucion.AltaCuentaMercadoExterno` desde PBP. En AP5 existe la tabla homonima y el procedimiento `Contribucion.MergeAltaCuentaMercadoExterno`, por lo que el mapeo es directo.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Contribucion_AltaCuentaMercadoExterno_Publicacion` | funcion activa o no validada |
| tabla CT | `cdc.Contribucion_AltaCuentaMercadoExterno_CT` | fuente CDC observada |
| tabla PBP | `Contribucion.AltaCuentaMercadoExterno` | tabla base inferida |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Contribucion.AltaCuentaMercadoExterno` | destino directo | alta | tabla homonima en AP5 |
| `Contribucion.MergeAltaCuentaMercadoExterno` | procedimiento receptor candidato | alta | hace `MERGE` contra la tabla AP5 |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | lee `cdc.Contribucion_AltaCuentaMercadoExterno_CT` |
| tabla AP5 | `Publicacion.sql` | existe `Contribucion.AltaCuentaMercadoExterno` |
| procedimiento AP5 | `Publicacion.sql` | existe `Contribucion.MergeAltaCuentaMercadoExterno` |

## Hechos observados

- La funcion, la tabla AP5 y el `Merge` comparten el mismo objeto funcional.
- El procedimiento AP5 parsea JSON y ejecuta `MERGE`.

## Inferencias

- El flujo probable es `Clearing.Contribucion.AltaCuentaMercadoExterno -> CDC -> Contribucion.MergeAltaCuentaMercadoExterno -> Publicacion.Contribucion.AltaCuentaMercadoExterno`.

## Dudas abiertas

- Confirmar si solo procesa updates o tambien altas completas.
- Validar el mecanismo que invoca el `Merge` desde el payload CDC.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-primer-tanda.csv`
- Fecha de analisis: `2026-08-27`
