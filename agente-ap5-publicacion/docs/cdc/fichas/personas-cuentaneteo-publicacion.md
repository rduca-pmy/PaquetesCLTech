# Ficha CDC PBP -> AP5

## Identificacion

- Funcion CDC: `cdc.fn_cdc_get_Personas_CuentaNeteo_Publicacion`
- Esquema inferido: `Personas`
- Objeto inferido: `CuentaNeteo`
- Clasificacion: `mapeo_directo`
- Nivel de confianza: `alta`

## Respuesta corta

Publica cuentas neteo desde PBP. AP5 tiene `Personas.CuentaNeteo` y una variante `CuentaNeteoPublicacion`, con evidencia previa en `030_PersonasGeneral*`.

## Objeto CDC analizado

| Tipo | Nombre | Observaciones |
| --- | --- | --- |
| funcion CDC | `cdc.fn_cdc_get_Personas_CuentaNeteo_Publicacion` | funcion activa o no validada |
| tabla PBP inferida | `Personas.CuentaNeteo` | entidad fuente |

## Relacion con AP5

| Tabla o dominio AP5 | Tipo de relacion | Confianza | Observaciones |
| --- | --- | --- | --- |
| `Personas.CuentaNeteo` | destino principal | alta | tabla AP5 homonima |
| `Personas.CuentaNeteoPublicacion` | destino relacionado | media | variante publicada observada |
| `030_PersonasGeneral*` | mecanismo relacionado | alta | paquetes SSIS previos |

## Evidencias

| Tipo | Fuente | Detalle |
| --- | --- | --- |
| funcion CDC | `Clearing.sql` | existe funcion CDC de publicacion |
| tabla AP5 | `Publicacion.sql` | existe `Personas.CuentaNeteo` |
| matriz SSIS | `data/personas-tablas-matriz.csv` | `CuentaNeteo` y `CuentaNeteoPublicacion` tienen evidencia |

## Hechos observados

- La entidad existe en AP5 con nombre homonimo.
- Hay evidencia SSIS previa.

## Inferencias

- CDC y paquetes podrian ser mecanismos alternativos o complementarios.

## Dudas abiertas

- Confirmar si `CuentaNeteoPublicacion` sigue vigente operativamente.

## Trazabilidad

- Fuente principal: `Clearing.sql`
- Artefactos complementarios: `Publicacion.sql`, `data/cdc-mapeo-segunda-tanda.csv`
- Fecha de analisis: `2026-09-11`
