# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Productos_ContratoMensajeWarrant_Publicacion`
- Esquema inferido: `Productos`
- Objeto inferido: `ContratoMensajeWarrant`
- Clasificacion: `mapeo_probable`
- Nivel de confianza: `media`

## Respuesta corta

Publica la relacion contrato/mensaje Warrant desde PBP. AP5 no tiene tabla homonima, pero el dato aparece en el circuito de activos y mensajes Warrant.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Productos_ContratoMensajeWarrant_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Productos.ContratoMensajeWarrant` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Activos.ActivoCertificadoDepositoWarrantPublicacion` | destino candidato | media | paquete consulta `Productos.ContratoMensajeWarrant` |
| `Mensajes.MensajeCertificadoDepositoWarrant` | dominio relacionado | media | circuito de mensajes Warrant |
| `Productos.ProductoWarrant` | tabla relacionada | media | dimension de producto Warrant |
| `MensajesGeneral.InsertMensajeWarrant` | procedimiento relacionado | media | SP de alta de mensaje Warrant |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| tabla AP5 | `Publicacion.sql` | existen tablas y SPs del circuito Warrant |
| paquete AP5 | `IntegrationServices/Publicacion/Activos_ActivoCertificadoDepositoWarrantPublicacion.dtsx` | consulta `Productos.ContratoMensajeWarrant` |

## Hechos observados

- No existe tabla AP5 `Productos.ContratoMensajeWarrant`.
- El circuito Warrant cruza `Productos`, `Activos` y `Mensajes`.

## Inferencias

- El CDC probablemente alimenta un insumo de publicacion Warrant que se materializa en activos y mensajes.

## Dudas abiertas

- Confirmar si el destino final principal es activo Warrant, mensaje Warrant o ambos.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `IntegrationServices/Publicacion`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
