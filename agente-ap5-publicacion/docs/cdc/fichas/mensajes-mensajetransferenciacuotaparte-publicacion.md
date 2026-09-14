# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Mensajes_MensajeTransferenciaCuotaParte_Publicacion`
- Esquema inferido: `Mensajes`
- Objeto inferido: `MensajeTransferenciaCuotaParte`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

La funcion CDC publica transferencias de cuotaparte desde PBP. En AP5 se materializa en dos tablas candidatas segun el lado del movimiento: `Mensajes.MensajeTransferenciaCuotaparteIngreso` y `Mensajes.MensajeTransferenciaCuotaparteEgreso`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Mensajes_MensajeTransferenciaCuotaParte_Publicacion` | funcion activa o no validada |
| tabla CT | `cdc.Mensajes_MensajeTransferenciaCuotaParte_CT` | fuente CDC observada |
| objeto funcional | `MensajeTransferenciaCuotaParte` | no conserva exactamente el mismo nombre en AP5 |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Mensajes.MensajeTransferenciaCuotaparteIngreso` | destino directo por lado ingreso | alta | tabla AP5 especifica |
| `Mensajes.MensajeTransferenciaCuotaparteEgreso` | destino directo por lado egreso | alta | tabla AP5 especifica |
| `Mensajes.InsertMensajeTransferenciaCuotaparteIngreso` | procedimiento de insercion | alta | inserta la variante ingreso |
| `Mensajes.InsertMensajeTransferenciaCuotaparteEgreso` | procedimiento de insercion | alta | inserta la variante egreso |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | lee `cdc.Mensajes_MensajeTransferenciaCuotaParte_CT` |
| enriquecimiento | `Clearing.sql` | usa cotizacion, aforo, finalidad, cuenta neteo, cuenta compensacion y activo |
| tablas AP5 | `Publicacion.sql` | existen tablas de ingreso y egreso de cuotaparte |
| procedimientos AP5 | `Publicacion.sql` | existen inserts especificos para ingreso y egreso |

## Hechos observados

- Una sola funcion CDC puede corresponder a mas de una tabla AP5.
- La division AP5 parece modelar el sentido de la transferencia.
- Este circuito no tenia evidencia SSIS directa.

## Inferencias

- El payload CDC probablemente contiene datos suficientes para que AP5 derive si corresponde ingreso o egreso.

## Dudas abiertas

- Identificar la regla exacta que separa ingreso y egreso.
- Confirmar si existe tambien una cabecera general en `Mensajes.MensajeTransferencia`.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-primer-tanda.csv`, `docs/esquemas/mensajes.md`
- Fecha de analisis: `2026-08-27`
