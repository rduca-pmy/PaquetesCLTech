# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Registro_CancelacionCartera_Publicacion`
- Esquema inferido: `Registro`
- Objeto inferido: `CancelacionCartera`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

La funcion CDC toma cambios de `Registro.CancelacionCartera` en PBP y los transforma en datos publicables de cancelaciones. En AP5 el destino se ve como `Registro.OperacionCarteraCanceladaHistorico` y `Registro.OperacionCarteraCancelada`, mediante `Registro.MergeCancelacionCarteraPublicacion`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Registro_CancelacionCartera_Publicacion` | funcion activa o no validada |
| tabla CT | `cdc.Registro_CancelacionCartera_CT` | fuente CDC observada |
| tabla PBP | `Registro.CancelacionCartera` | tabla base de cancelaciones en Clearing |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Registro.OperacionCarteraCanceladaHistorico` | destino historico candidato | alta | `MergeCancelacionCarteraPublicacion` hace `MERGE` sobre esta tabla |
| `Registro.OperacionCarteraCancelada` | destino actual candidato | alta | existe `MergeCancelacionCarteraPublicacionActual` |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | la funcion lee `cdc.Registro_CancelacionCartera_CT` |
| enriquecimiento | `Clearing.sql` | une operaciones compra/venta, cuenta registro, contrato, moneda, proceso y ejecucion |
| procedimiento AP5 | `Publicacion.sql` | existe `Registro.MergeCancelacionCarteraPublicacion` |
| tabla AP5 | `Publicacion.sql` | existen `Registro.OperacionCarteraCanceladaHistorico` y `Registro.OperacionCarteraCancelada` |

## Hechos observados

- El objeto PBP se llama `CancelacionCartera`.
- El objeto AP5 queda publicado como `OperacionCarteraCancelada`.
- Publicacion contiene procedimientos de merge especificos para este circuito.

## Inferencias

- La diferencia de nombres responde a una transformacion funcional: PBP registra la cancelacion, AP5 la publica como operacion de cartera cancelada.

## Dudas abiertas

- Confirmar si todas las operaciones canceladas llegan por CDC o si algunas siguen llegando por paquete SSIS.
- Revisar como convive con `010_OperacionCarteraCancelada.dtsx`.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-primer-tanda.csv`, `docs/fichas/registro-operacioncarteracancelada.md`
- Fecha de analisis: `2026-08-27`
