# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Compensacion_PorcentajeMontoDrpPorCuenta_Publicacion`
- Esquema inferido: `Compensacion`
- Objeto inferido: `PorcentajeMontoDrpPorCuenta`
- Clasificacion: `mapeo_probable`
- Nivel de confianza: `media`

## Respuesta corta

Publica porcentajes/montos DRP por cuenta desde PBP. AP5 no tiene tabla homonima, pero si el circuito `Compensacion.DerivacionDRP`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Compensacion_PorcentajeMontoDrpPorCuenta_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Compensacion.PorcentajeMontoDrpPorCuenta` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Compensacion.DerivacionDRP` | destino candidato | media | tabla AP5 del dominio DRP |
| `Compensacion_DerivacionDRP*.dtsx` | mecanismo relacionado | media | paquetes SSIS de derivacion |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| matriz SSIS | `data/compensacion-tablas-matriz.csv` | `DerivacionDRP` tiene paquetes asociados |

## Hechos observados

- No se encontro tabla AP5 homonima.
- El nombre DRP coincide con el dominio publicado en AP5.

## Inferencias

- El porcentaje por cuenta podria ser insumo de `DerivacionDRP`.

## Dudas abiertas

- Confirmar si el payload CDC se persiste en `DerivacionDRP` o en una tabla intermedia.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
