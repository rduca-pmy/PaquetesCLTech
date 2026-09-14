# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Mensajes_MensajeCompensacionDepositariaDetalle_Publicacion`
- Esquema inferido: `Mensajes`
- Objeto inferido: `MensajeCompensacionDepositariaDetalle`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

La funcion CDC publica detalles de mensajes de compensacion depositaria desde PBP. En AP5 existe `Mensajes.MensajeCompensacionDepositariaDetalle` y se observa el procedimiento `Mensajes.InsertMensajeCompensacionMTMDepositarias`, ademas del merge general de publicacion de mensajes.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Mensajes_MensajeCompensacionDepositariaDetalle_Publicacion` | funcion activa o no validada |
| tabla CT | `cdc.Mensajes_MensajeCompensacionDepositariaDetalle_CT` | fuente CDC observada |
| tabla PBP relacionada | `Mensajes.MensajeCompensacionDepositaria` | cabecera usada en joins |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Mensajes.MensajeCompensacionDepositariaDetalle` | destino directo | alta | tabla homonima en AP5 |
| `Mensajes.InsertMensajeCompensacionMTMDepositarias` | procedimiento relacionado | alta | inserta detalle del mensaje |
| `MensajesGeneral.MergeMensajePublicacion` | actualizacion de cabecera/estado | media | candidato para estado publicado |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | lee `cdc.Mensajes_MensajeCompensacionDepositariaDetalle_CT` |
| enriquecimiento | `Clearing.sql` | une cabecera, mensaje general, cuenta neteo y cuenta compensacion |
| tabla AP5 | `Publicacion.sql` | existe `Mensajes.MensajeCompensacionDepositariaDetalle` |
| procedimiento AP5 | `Publicacion.sql` | existe `Mensajes.InsertMensajeCompensacionMTMDepositarias` |

## Hechos observados

- Este circuito no tenia evidencia SSIS directa.
- La funcion CDC y la tabla AP5 coinciden nominalmente.
- El mensaje especifico parece depender de una cabecera general.

## Inferencias

- CDC cubre la llegada incremental del detalle, y `MensajesGeneral.MergeMensajePublicacion` podria consolidar estado de publicacion.

## Dudas abiertas

- Confirmar si el detalle se inserta antes o despues del merge general del mensaje.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-primer-tanda.csv`, `docs/esquemas/mensajes.md`
- Fecha de analisis: `2026-08-27`
