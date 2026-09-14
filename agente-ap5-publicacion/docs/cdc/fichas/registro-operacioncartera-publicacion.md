# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Registro_OperacionCartera_Publicacion`
- Esquema inferido: `Registro`
- Objeto inferido: `OperacionCartera`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

La funcion CDC publica cambios de `Registro.OperacionCartera` desde PBP. En AP5 el destino candidato no es una tabla homonima, sino el conjunto de publicacion `Registro.OperacionCarteraPublicacionHistorico`, `Registro.OperacionCarteraPublicacion` y `Registro.OperacionCarteraOnlinePublicacion`, procesado por procedimientos `Merge*`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Registro_OperacionCartera_Publicacion` | funcion activa o no validada |
| tabla CT | `cdc.Registro_OperacionCartera_CT` | fuente CDC observada en el cuerpo |
| tabla PBP | `Registro.OperacionCartera` | tabla base usada para enriquecer el payload |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Registro.OperacionCarteraPublicacionHistorico` | destino historico candidato | alta | `Registro.MergeOperacionCarteraPublicacion` hace `MERGE` sobre esta tabla |
| `Registro.OperacionCarteraPublicacion` | destino actual candidato | alta | `Registro.MergeOperacionCarteraPublicacionActual` forma parte del circuito |
| `Registro.OperacionCarteraOnlinePublicacion` | destino online candidato | media | aparece procedimiento especifico `MergeOperacionCarteraOnlinePublicacion` |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | la funcion lee `cdc.Registro_OperacionCartera_CT` |
| enriquecimiento | `Clearing.sql` | el cuerpo une `Registro.OperacionCartera` con cuentas, participantes, contratos y reporte de operacion |
| procedimiento AP5 | `Publicacion.sql` | existe `Registro.MergeOperacionCarteraPublicacion` |
| tabla AP5 | `Publicacion.sql` | existen `Registro.OperacionCarteraPublicacionHistorico` y `Registro.OperacionCarteraPublicacion` |

## Hechos observados

- Existe una funcion CDC especifica para `Registro.OperacionCartera`.
- En AP5 existen procedimientos `Merge*` para publicar operaciones de cartera.
- La tabla AP5 no conserva el mismo nombre base, sino que agrega el sufijo `Publicacion`.

## Inferencias

- El flujo probable es `Clearing.Registro.OperacionCartera -> cdc.fn_cdc_get_Registro_OperacionCartera_Publicacion -> Registro.MergeOperacionCarteraPublicacion -> tablas Registro.OperacionCarteraPublicacion*`.

## Dudas abiertas

- Confirmar que componente de transporte invoca el `Merge` en AP5.
- Confirmar en que casos se llena la tabla online versus la tabla actual.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-primer-tanda.csv`, `docs/fichas/registro-operacioncarterapublicacionhistorico.md`
- Fecha de analisis: `2026-08-27`
