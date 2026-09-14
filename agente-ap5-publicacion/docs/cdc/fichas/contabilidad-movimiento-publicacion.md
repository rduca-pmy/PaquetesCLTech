# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Contabilidad_Movimiento_Publicacion`
- Esquema inferido: `Contabilidad`
- Objeto inferido: `Movimiento`
- Clasificacion: `mapeo_probable`
- Nivel de confianza: `alta`

## Respuesta corta

Publica movimientos contables desde PBP. AP5 no tiene tabla `Contabilidad.Movimiento`, pero consolida la publicacion en `Contabilidad.MovimientoPublicacionHistorico` y cuenta con `Contabilidad.MergeMovimientoPublicacion`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Contabilidad_Movimiento_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Contabilidad.Movimiento` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Contabilidad.MovimientoPublicacionHistorico` | destino candidato | alta | tabla publicada historica |
| `Contabilidad.MergeMovimientoPublicacion` | procedimiento candidato | alta | SP AP5 observado |
| `965_Movimientos.dtsx` | mecanismo relacionado | alta | paquete SSIS previo |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| procedimiento AP5 | `Publicacion.sql` | existe `Contabilidad.MergeMovimientoPublicacion` |
| matriz SSIS | `data/contabilidad-tablas-matriz.csv` | `MovimientoPublicacionHistorico` se carga con `965_Movimientos.dtsx` |

## Hechos observados

- No existe tabla AP5 `Contabilidad.Movimiento`.
- El destino AP5 es una tabla historica de publicacion.

## Inferencias

- El movimiento CDC probablemente se publica como historico consolidado.

## Dudas abiertas

- Confirmar si el SP `MergeMovimientoPublicacion` es invocado por el consumidor CDC.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
