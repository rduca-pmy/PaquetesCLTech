# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Compensacion_GrupoEscenarioPorcentajeBonificacionPorPlazo_Publicacion`
- Esquema inferido: `Compensacion`
- Objeto inferido: `GrupoEscenarioPorcentajeBonificacionPorPlazo`
- Clasificacion: `mapeo_probable`
- Nivel de confianza: `baja`

## Respuesta corta

Publica porcentajes de bonificacion por plazo asociados a grupo/escenario en PBP. AP5 no expone una tabla equivalente por nombre, por lo que queda como insumo probable del circuito de margenes.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Compensacion_GrupoEscenarioPorcentajeBonificacionPorPlazo_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Compensacion.GrupoEscenarioPorcentajeBonificacionPorPlazo` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Compensacion.MargenPublicacionHistorico` | destino candidato | baja | circuito de margen publicado |
| `Compensacion.MargenPublicacion` | destino candidato | baja | requiere consumidor exacto |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| tabla AP5 relacionada | `Publicacion.sql` | existen tablas `Compensacion.MargenPublicacion*` |

## Hechos observados

- No se encontro tabla AP5 homonima.
- El objeto fuente tiene granularidad de parametro, no de tabla publicada final.

## Inferencias

- Probablemente participa como parametro de calculo antes de publicar margenes.

## Dudas abiertas

- Identificar si hay SP o servicio que transforme esta entidad en filas de margen publicado.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
