# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_MensajesGeneral_Mensaje_Publicacion`
- Esquema inferido: `MensajesGeneral`
- Objeto inferido: `Mensaje`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

La funcion CDC publica cambios del mensaje general de PBP. En AP5 el receptor candidato es `MensajesGeneral.MergeMensajePublicacion`, que actualiza `MensajesGeneral.MensajePublicacion`, `MensajesGeneral.MensajePublicacionHistorico` y estados relacionados.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_MensajesGeneral_Mensaje_Publicacion` | funcion activa o no validada |
| tabla PBP | `MensajesGeneral.Mensaje` | objeto inferido por nombre de funcion |
| procedimiento AP5 | `MensajesGeneral.MergeMensajePublicacion` | receptor candidato |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `MensajesGeneral.MensajePublicacion` | destino actual candidato | alta | tabla de publicacion de mensajes |
| `MensajesGeneral.MensajePublicacionHistorico` | destino historico candidato | alta | el merge actualiza historico |
| `Mensajes` | dominio relacionado | media | varios mensajes especificos dependen de la cabecera general |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe `cdc.fn_cdc_get_MensajesGeneral_Mensaje_Publicacion` |
| procedimiento AP5 | `Publicacion.sql` | existe `MensajesGeneral.MergeMensajePublicacion` |
| tablas AP5 | `Publicacion.sql` | existen `MensajesGeneral.MensajePublicacion` y `MensajesGeneral.MensajePublicacionHistorico` |
| estado de fase SSIS | `docs/esquemas/mensajesgeneral.md` | el esquema no tenia evidencia directa desde paquetes SSIS |

## Hechos observados

- `MensajesGeneral` quedo sin evidencia SSIS directa.
- La fase CDC introduce un camino de publicacion claro para el esquema.
- El procedimiento AP5 opera sobre mensajes publicados y estados relacionados.

## Inferencias

- `MensajesGeneral.Mensaje` parece ser la cabecera comun del circuito de mensajes y su publicacion se refleja en tablas `MensajePublicacion*`.

## Dudas abiertas

- Determinar como se vincula cada mensaje especifico con el merge general.
- Confirmar si `MergeMensajePublicacion` se invoca para todas las funciones CDC de `Mensajes`.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-primer-tanda.csv`, `docs/esquemas/mensajesgeneral.md`
- Fecha de analisis: `2026-08-27`
