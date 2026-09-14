# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Personas_CuentaRegistro_Publicacion`
- Esquema inferido: `Personas`
- Objeto inferido: `CuentaRegistro`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

Publica cuentas registro desde PBP. AP5 tiene tabla homonima, tabla `CuentaRegistroPublicacion` y procedimiento `Personas.MergeCuentaRegistroPublicacion`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Personas_CuentaRegistro_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Personas.CuentaRegistro` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Personas.CuentaRegistro` | destino principal | alta | tabla AP5 homonima |
| `Personas.CuentaRegistroPublicacion` | destino publicado | alta | tabla de publicacion |
| `Personas.MergeCuentaRegistroPublicacion` | procedimiento candidato | alta | SP AP5 especifico |
| `031_CuentaRegistroPublicacion.dtsx` | mecanismo relacionado | alta | paquete especifico |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| tabla y SP AP5 | `Publicacion.sql` | existen `CuentaRegistro` y `MergeCuentaRegistroPublicacion` |
| matriz SSIS | `data/personas-tablas-matriz.csv` | `CuentaRegistroPublicacion` tiene evidencia |

## Hechos observados

- Relacion directa y consistente con documentacion previa del esquema Personas.

## Inferencias

- El CDC probablemente alimenta o sincroniza el circuito publicado de cuentas registro.

## Dudas abiertas

- Confirmar si el SP es invocado directamente por cola CDC.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`, `docs/esquemas/personas.md`
- Fecha de analisis: `2026-09-11`
