# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_General_Proceso_Publicacion`
- Esquema inferido: `General`
- Objeto inferido: `Proceso`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

Publica procesos desde PBP. AP5 tiene tabla homonima `General.Proceso`, con evidencia SSIS en `020_General.dtsx`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_General_Proceso_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `General.Proceso` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `General.Proceso` | destino principal | alta | tabla AP5 homonima |
| `020_General.dtsx` | mecanismo relacionado | alta | paquete SSIS previo |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| tabla AP5 | `Publicacion.sql` | existe `General.Proceso` |
| matriz SSIS | `data/general-tablas-matriz.csv` | `Proceso` se carga con `020_General.dtsx` |

## Hechos observados

- No se observo `General.MergeProceso` en esta pasada.
- Hay tabla AP5 exacta y paquete existente.

## Inferencias

- La funcion CDC podria alimentar la misma entidad que historicamente aparece en `020_General.dtsx`.

## Dudas abiertas

- Confirmar si hay consumidor CDC directo o si el paquete sigue siendo el camino principal.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
