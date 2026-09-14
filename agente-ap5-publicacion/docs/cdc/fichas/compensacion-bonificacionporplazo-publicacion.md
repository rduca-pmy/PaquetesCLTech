# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Compensacion_BonificacionPorPlazo_Publicacion`
- Esquema inferido: `Compensacion`
- Objeto inferido: `BonificacionPorPlazo`
- Clasificacion: `mapeo_probable`
- Nivel de confianza: `baja`

## Respuesta corta

La funcion CDC publica cambios de bonificaciones por plazo en PBP. En AP5 no se encontro tabla homonima; el destino candidato queda asociado al circuito de margenes publicados.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Compensacion_BonificacionPorPlazo_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Compensacion.BonificacionPorPlazo` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Compensacion.MargenPublicacionHistorico` | destino candidato | baja | tabla publicada por circuito de margenes |
| `Compensacion.MargenPublicacion` | destino candidato | baja | sin evidencia SSIS directa previa |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| matriz SSIS | `data/compensacion-tablas-matriz.csv` | `MargenPublicacionHistorico` se carga con `999_MargenPublicacion*.dtsx` |

## Hechos observados

- No se encontro tabla AP5 `Compensacion.BonificacionPorPlazo`.
- El nombre sugiere parametro funcional de margen/bonificacion.

## Inferencias

- La informacion podria impactar el calculo o publicacion de margenes, pero no queda cerrado el consumidor exacto.

## Dudas abiertas

- Confirmar si el servicio CDC entrega este payload a una tabla intermedia o a un SP no homonimo.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
