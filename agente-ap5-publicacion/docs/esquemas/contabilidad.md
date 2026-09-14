# Esquema Contabilidad

## Resumen

- Tablas en `Publicacion.sql`: `4`
- Tablas con evidencia en SSIS: `1`
- Tablas sin evidencia en SSIS: `3`

## Lectura inicial

La cobertura observada es baja. En los paquetes relevados, solo aparece evidencia clara sobre una tabla a traves de `965_Movimientos.dtsx`.

## Paquete relevante

- `965_Movimientos.dtsx`

## Matriz inicial de tablas

| Tabla | Paquete o paquetes principales | Evidencia observada |
| --- | --- | --- |
| `Contabilidad.MovimientoPublicacionHistorico` | `965_Movimientos.dtsx` | `OpenRowset`, `UPDATE` |

## Tablas sin evidencia observada

- `Contabilidad.SaldoCuentaAdministrativa`
- `Contabilidad.RubroCuentaAdministrativa`
- `Contabilidad.Widgets`

## Nota

Conviene no asumir que el esquema se carga por SSIS; parte de su logica probablemente viva en base o en otro circuito.

## Artefactos de soporte

- [contabilidad-tablas-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/contabilidad-tablas-matriz.csv)
