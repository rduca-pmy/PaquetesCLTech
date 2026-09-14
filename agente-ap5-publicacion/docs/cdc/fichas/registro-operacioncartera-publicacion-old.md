# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Registro_OperacionCartera_Publicacion_old`
- Esquema inferido: `Registro`
- Objeto inferido: `OperacionCartera`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `media`

## Respuesta corta

La funcion `old` parece ser una variante legacy del circuito CDC de `Registro.OperacionCartera`. El destino AP5 candidato coincide con la version activa: `Registro.OperacionCarteraPublicacionHistorico` y `Registro.OperacionCarteraPublicacion`, mediante `Registro.MergeOperacionCarteraPublicacion`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Registro_OperacionCartera_Publicacion_old` | variante legacy |
| objeto funcional | `Registro.OperacionCartera` | mismo objeto inferido que la funcion activa |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Registro.OperacionCarteraPublicacionHistorico` | destino historico candidato | media | coincide con el circuito activo, pero falta confirmar vigencia |
| `Registro.OperacionCarteraPublicacion` | destino actual candidato | media | tabla publicada del mismo dominio |
| `Registro.MergeOperacionCarteraPublicacion` | receptor candidato | media | mismo receptor que el circuito activo |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe `cdc.fn_cdc_get_Registro_OperacionCartera_Publicacion_old` |
| funcion activa equivalente | `Clearing.sql` | existe `cdc.fn_cdc_get_Registro_OperacionCartera_Publicacion` |
| procedimiento AP5 | `Publicacion.sql` | existe `Registro.MergeOperacionCarteraPublicacion` |

## Hechos observados

- La funcion tiene sufijo `old`.
- El objeto inferido es el mismo que la funcion CDC activa de operaciones de cartera.
- AP5 tiene un circuito de merge claro para operaciones publicadas.

## Inferencias

- La funcion probablemente representa una version anterior del mismo circuito `OperacionCartera -> OperacionCarteraPublicacion`.

## Dudas abiertas

- Confirmar si sigue siendo invocada por algun servicio o si solo queda en el esquema por compatibilidad.
- Comparar diferencias de columnas contra la funcion activa.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-primer-tanda.csv`
- Fecha de analisis: `2026-08-27`
