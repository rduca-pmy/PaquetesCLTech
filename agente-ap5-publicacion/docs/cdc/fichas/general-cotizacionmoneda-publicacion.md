# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_General_CotizacionMoneda_Publicacion`
- Esquema inferido: `General`
- Objeto inferido: `CotizacionMoneda`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

Publica cotizaciones de moneda desde PBP. AP5 tiene tabla homonima `General.CotizacionMoneda` y procedimiento `General.MergeCotizacionMoneda`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_General_CotizacionMoneda_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `General.CotizacionMoneda` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `General.CotizacionMoneda` | destino principal | alta | tabla AP5 homonima |
| `General.MergeCotizacionMoneda` | procedimiento candidato | alta | SP AP5 especifico |
| `020_General.dtsx` | mecanismo relacionado | alta | paquete SSIS previo |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| tabla y SP AP5 | `Publicacion.sql` | existen tabla y `MergeCotizacionMoneda` |
| matriz SSIS | `data/general-tablas-matriz.csv` | `CotizacionMoneda` se carga con `020_General.dtsx` |

## Hechos observados

- Es uno de los mapeos mas directos de la tanda.

## Inferencias

- El CDC puede complementar o reemplazar el paquete general para esta entidad.

## Dudas abiertas

- Confirmar convivencia operativa entre CDC y `020_General.dtsx`.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
