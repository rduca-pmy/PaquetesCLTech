# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Registro_RelacionOperacionAFijar_Publicacion`
- Esquema inferido: `Registro`
- Objeto inferido: `RelacionOperacionAFijar`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

La funcion CDC toma cambios de `Registro.RelacionOperacionAFijar` en PBP. En AP5 el destino candidato es `Registro.RelacionOperacionesAFijar`, con diferencia de pluralizacion entre origen y destino, y con evidencia SSIS previa en `Registro_RelacionOperacionesAFijar.dtsx`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Registro_RelacionOperacionAFijar_Publicacion` | funcion activa o no validada |
| tabla CT | `cdc.Registro_RelacionOperacionAFijar_CT` | fuente CDC observada |
| tabla PBP | `Registro.RelacionOperacionAFijar` | tabla base inferida |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Registro.RelacionOperacionesAFijar` | destino directo candidato | alta | tabla AP5 existente con nombre plural |
| `Registro_RelacionOperacionesAFijar.dtsx` | mecanismo complementario observado | alta | paquete SSIS ya documentado para la misma tabla |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | lee `cdc.Registro_RelacionOperacionAFijar_CT` |
| enriquecimiento | `Clearing.sql` | une operaciones compra y venta con `Registro.OperacionCartera` |
| tabla AP5 | `Publicacion.sql` | existe `Registro.RelacionOperacionesAFijar` |
| ficha SSIS | `docs/fichas/registro-relacionoperacionesafijar.md` | el paquete SSIS carga la tabla AP5 |

## Hechos observados

- Hay una diferencia nominal entre singular en PBP y plural en AP5.
- La tabla AP5 ya tenia evidencia por paquete SSIS.
- La funcion CDC abre un segundo carril de trazabilidad para el mismo concepto.

## Inferencias

- El circuito puede combinar CDC para detectar cambios y SSIS para materializar o recomponer la tabla publicada.

## Dudas abiertas

- Determinar si el paquete SSIS consume el resultado CDC o si ambos mecanismos son independientes.
- Confirmar cual es el receptor AP5 exacto del payload CDC.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-primer-tanda.csv`, `docs/fichas/registro-relacionoperacionesafijar.md`
- Fecha de analisis: `2026-08-27`
