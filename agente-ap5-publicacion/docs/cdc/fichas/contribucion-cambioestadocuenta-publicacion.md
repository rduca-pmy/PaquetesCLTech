# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Contribucion_CambioEstadoCuenta_Publicacion`
- Esquema inferido: `Contribucion`
- Objeto inferido: `CambioEstadoCuenta`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

La funcion CDC publica cambios de estado de cuenta desde `Contribucion.CambioEstadoCuenta` en PBP. En AP5 existe la tabla homonima y el procedimiento `Contribucion.MergeCambioEstadoCuenta`, por lo que el mapeo es directo.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Contribucion_CambioEstadoCuenta_Publicacion` | funcion activa o no validada |
| tabla CT | `cdc.Contribucion_CambioEstadoCuenta_CT` | fuente CDC observada |
| tabla PBP | `Contribucion.CambioEstadoCuenta` | tabla base inferida |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Contribucion.CambioEstadoCuenta` | destino directo | alta | tabla homonima en AP5 |
| `Contribucion.MergeCambioEstadoCuenta` | procedimiento receptor candidato | alta | procedimiento `Merge*` especifico |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | lee `cdc.Contribucion_CambioEstadoCuenta_CT` |
| tabla AP5 | `Publicacion.sql` | existe `Contribucion.CambioEstadoCuenta` |
| procedimiento AP5 | `Publicacion.sql` | existe `Contribucion.MergeCambioEstadoCuenta` |

## Hechos observados

- La tabla estaba sin evidencia SSIS, pero aparece cubierta por CDC.
- El procedimiento AP5 candidato es especifico y nominalmente consistente.

## Inferencias

- El circuito de cambios de estado de cuenta viaja por CDC y se materializa en AP5 por `MergeCambioEstadoCuenta`.

## Dudas abiertas

- Confirmar si el cambio de estado impacta tambien tablas de `Personas` o `PersonasGeneral`.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-primer-tanda.csv`
- Fecha de analisis: `2026-08-27`
