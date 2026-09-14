# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Compensacion_MargenLimitePosicionAbierta_Publicacion`
- Esquema inferido: `Compensacion`
- Objeto inferido: `MargenLimitePosicionAbierta`
- Clasificacion: `mapeo_probable`
- Nivel de confianza: `baja`

## Respuesta corta

Publica cambios de limites de posicion abierta vinculados a margen. En AP5 no hay tabla homonima; se asocia tentativamente a `MargenPublicacion`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Compensacion_MargenLimitePosicionAbierta_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Compensacion.MargenLimitePosicionAbierta` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Compensacion.MargenPublicacion` | destino candidato | baja | relacion por dominio funcional |
| `Compensacion.MargenPublicacionHistorico` | destino candidato | baja | circuito historico de margen |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| tabla AP5 | `Publicacion.sql` | existen tablas de margen publicado |

## Hechos observados

- No se encontro tabla AP5 homonima.
- No se observo procedimiento `Merge*` especifico.

## Inferencias

- Podria ser una regla que impacta la publicacion de margenes, no una entidad expuesta directamente.

## Dudas abiertas

- Confirmar consumidor exacto del payload CDC.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
