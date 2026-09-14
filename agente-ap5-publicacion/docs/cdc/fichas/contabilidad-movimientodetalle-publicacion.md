# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Contabilidad_MovimientoDetalle_Publicacion`
- Esquema inferido: `Contabilidad`
- Objeto inferido: `MovimientoDetalle`
- Clasificacion: `mapeo_probable`
- Nivel de confianza: `alta`

## Respuesta corta

Publica el detalle de movimientos contables desde PBP. AP5 no tiene tabla homonima, pero cuenta con `Contabilidad.MergeMovimientoDetallePublicacion` y consolida la informacion en `MovimientoPublicacionHistorico`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Contabilidad_MovimientoDetalle_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Contabilidad.MovimientoDetalle` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Contabilidad.MovimientoPublicacionHistorico` | destino candidato | alta | tabla publicada historica |
| `Contabilidad.MergeMovimientoDetallePublicacion` | procedimiento candidato | alta | SP AP5 observado |
| `965_Movimientos.dtsx` | mecanismo relacionado | alta | paquete SSIS previo |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| procedimiento AP5 | `Publicacion.sql` | existe `Contabilidad.MergeMovimientoDetallePublicacion` |
| matriz SSIS | `data/contabilidad-tablas-matriz.csv` | `MovimientoPublicacionHistorico` se carga con `965_Movimientos.dtsx` |

## Hechos observados

- No existe tabla AP5 `Contabilidad.MovimientoDetalle`.
- Hay procedimiento AP5 especifico para detalle.

## Inferencias

- El detalle CDC complementa el movimiento publicado historico.

## Dudas abiertas

- Confirmar granularidad final en `MovimientoPublicacionHistorico`.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
