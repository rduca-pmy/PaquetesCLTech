# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_ComprobantesGeneral_ComprobanteVentaDetalle_Publicacion_OLD`
- Esquema inferido: `ComprobantesGeneral`
- Objeto inferido: `ComprobanteVentaDetalle`
- Clasificacion: `mapeo_probable`
- Nivel de confianza: `media`

## Respuesta corta

Funcion legacy para publicar detalle de comprobantes de venta. En AP5 el destino equivalente es `ComprobantesGeneral.ComprobanteDetallePublicacion`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_ComprobantesGeneral_ComprobanteVentaDetalle_Publicacion_OLD` | variante legacy |
| tabla PBP inferida | `ComprobantesGeneral.ComprobanteVentaDetalle` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `ComprobantesGeneral.ComprobanteDetallePublicacion` | destino candidato | media | tabla publicada equivalente |
| `Comprobantes_Facturacion.dtsx` | mecanismo relacionado | media | paquete ya relevado |
| `Comprobantes_Liquidaciones.dtsx` | mecanismo relacionado | media | paquete ya relevado |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC legacy |
| tabla AP5 | `Publicacion.sql` | existe `ComprobantesGeneral.ComprobanteDetallePublicacion` |
| matriz SSIS | `data/comprobantesgeneral-tablas-matriz.csv` | paquetes de detalle publicado |

## Hechos observados

- La funcion esta marcada como `_OLD`.
- No existe tabla AP5 `ComprobanteVentaDetalle`.

## Inferencias

- El circuito pudo haber migrado, pero el destino funcional sigue siendo detalle publicado.

## Dudas abiertas

- Validar si esta funcion legacy sigue siendo invocada por el servicio CDC.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
