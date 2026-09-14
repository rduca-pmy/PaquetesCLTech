# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Mensajes_MensajeDepositoIVA_Publicacion`
- Esquema inferido: `Mensajes`
- Objeto inferido: `MensajeDepositoIVA`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

La funcion CDC publica cambios de mensajes de deposito de IVA desde PBP. En AP5 el destino candidato directo es `Mensajes.MensajeDepositoIva`, con relacion adicional a `Mensajes.MensajeDepositoIvaDetalle`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Mensajes_MensajeDepositoIVA_Publicacion` | funcion activa o no validada |
| tabla CT | `cdc.Mensajes_MensajeDepositoIVA_CT` | fuente CDC observada |
| tabla PBP | `Mensajes.MensajeDepositoIva` | tabla base inferida |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Mensajes.MensajeDepositoIva` | destino directo | alta | tabla homonima con diferencia de casing |
| `Mensajes.MensajeDepositoIvaDetalle` | destino relacionado | alta | detalle asociado al deposito IVA |
| `Mensajes.InsertMensajeDepositoDeIVA` | procedimiento de insercion | alta | inserta cabecera del mensaje |
| `Mensajes.InsertMensajeDepositoDeIVADetalle` | procedimiento de insercion | alta | inserta detalle |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | lee `cdc.Mensajes_MensajeDepositoIVA_CT` |
| enriquecimiento | `Clearing.sql` | une con `MensajesGeneral.Mensaje`, cuenta compensacion y cuenta registro |
| tabla AP5 | `Publicacion.sql` | existen `Mensajes.MensajeDepositoIva` y `Mensajes.MensajeDepositoIvaDetalle` |
| procedimiento AP5 | `Publicacion.sql` | existen inserts especificos para deposito IVA |

## Hechos observados

- `Mensajes` no tenia evidencia SSIS, pero este caso tiene CDC y SPs AP5 claros.
- AP5 separa cabecera y detalle del mensaje.
- El nombre alterna `IVA` e `Iva`, sin cambiar el concepto funcional.

## Inferencias

- El circuito probable usa CDC para detectar cambios de mensaje y procedimientos `Insert*` para materializar cabecera/detalle en AP5.

## Dudas abiertas

- Confirmar si el detalle siempre llega en el mismo payload que la cabecera.
- Revisar el rol exacto de `MensajesGeneral.MergeMensajePublicacion` en este circuito.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-primer-tanda.csv`, `docs/esquemas/mensajes.md`
- Fecha de analisis: `2026-08-27`
