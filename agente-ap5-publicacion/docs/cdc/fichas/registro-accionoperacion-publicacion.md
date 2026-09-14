# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Registro_AccionOperacion_Publicacion`
- Esquema inferido: `Registro`
- Objeto inferido: `AccionOperacion`
- Clasificacion: `mapeo_ambiguo`
- Nivel de confianza: `media`

## Respuesta corta

La funcion CDC publica cambios de `Registro.AccionOperacion`, pero en AP5 no se encontro una tabla homonima ni un `Merge*` especifico en esta pasada. Por el cuerpo observado, el destino candidato parece estar relacionado con `Registro.OperacionCarteraPublicacion` o su historico.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Registro_AccionOperacion_Publicacion` | funcion activa o no validada |
| tabla CT | `cdc.Registro_AccionOperacion_CT` | fuente CDC observada |
| tabla PBP relacionada | `Registro.AccionOperacionOperacionCartera` | une acciones con operaciones de cartera |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Registro.OperacionCarteraPublicacion` | destino candidato por dominio | media | la funcion une acciones con operaciones de cartera |
| `Registro.OperacionCarteraPublicacionHistorico` | destino historico candidato | media | comparte dominio con el circuito principal de operaciones |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | lee `cdc.Registro_AccionOperacion_CT` |
| relacion PBP | `Clearing.sql` | une `Registro.AccionOperacionOperacionCartera` con `Registro.OperacionCartera` |
| ausencia de homonimo AP5 | `Publicacion.sql` | no se encontro tabla `Registro.AccionOperacion` |

## Hechos observados

- La funcion existe y esta vinculada a operaciones de cartera.
- AP5 no muestra tabla homonima para el objeto `AccionOperacion`.
- El receptor AP5 exacto no quedo identificado.

## Inferencias

- La funcion podria alimentar estados, acciones o enriquecimientos de operaciones ya publicadas, no una tabla propia.

## Dudas abiertas

- Buscar si el payload de esta funcion es consumido por el mismo servicio que invoca `Registro.MergeOperacionCarteraPublicacion`.
- Identificar si la accion queda embebida en columnas de `OperacionCarteraPublicacion*`.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-primer-tanda.csv`
- Fecha de analisis: `2026-08-27`
