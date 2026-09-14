# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_ComprobantesGeneral_ComprobanteVenta_Publicacion`
- Esquema inferido: `ComprobantesGeneral`
- Objeto inferido: `ComprobanteVenta`
- Clasificacion: `mapeo_probable`
- Nivel de confianza: `alta`

## Respuesta corta

Publica comprobantes de venta desde PBP. AP5 no conserva el nombre `ComprobanteVenta`, sino que materializa el comprobante como `ComprobantesGeneral.ComprobantePublicacion`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_ComprobantesGeneral_ComprobanteVenta_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `ComprobantesGeneral.ComprobanteVenta` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `ComprobantesGeneral.ComprobantePublicacion` | destino candidato | alta | tabla publicada equivalente |
| `Comprobantes_Facturacion.dtsx` | mecanismo relacionado | alta | paquete ya relevado |
| `Comprobantes_Liquidaciones.dtsx` | mecanismo relacionado | alta | paquete ya relevado |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| tabla AP5 | `Publicacion.sql` | existe `ComprobantesGeneral.ComprobantePublicacion` |
| matriz SSIS | `data/comprobantesgeneral-tablas-matriz.csv` | paquetes de comprobantes publicados |

## Hechos observados

- No existe tabla AP5 `ComprobanteVenta`.
- AP5 usa una tabla publicada mas generica.

## Inferencias

- El CDC de venta probablemente se transforma en comprobante publicado.

## Dudas abiertas

- Confirmar si el flujo CDC distingue venta/liquidacion antes de llegar a `ComprobantePublicacion`.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
