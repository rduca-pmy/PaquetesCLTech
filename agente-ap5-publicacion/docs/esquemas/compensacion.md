# Esquema Compensacion

## Resumen

- Tablas en `Publicacion.sql`: `12`
- Tablas con evidencia en SSIS: `10`
- Tablas sin evidencia en SSIS: `2`

## Lectura inicial

Esquema con cobertura alta y muy alineado a paquetes especificos del dominio `Compensacion_*`, mas algunos numerados de margenes y simulacion.

## Paquetes relevantes

- `090_ConversionContrato.dtsx`
- `600_MargenesContratos.dtsx`
- `999_MargenPublicacion.dtsx`
- `999_MargenPublicacion_5Dias.dtsx`
- `Compensacion_DerivacionDRP.dtsx`
- `Compensacion_DerivacionDRP_Update.dtsx`
- `Compensacion_MargenDetalleGrupoProducto.dtsx`
- `Compensacion_ParametroContratoPublicacion.dtsx`
- `SimulacionContratoPublicacion.dtsx`
- `SimulacionEscenarioPublicacion.dtsx`

## Matriz inicial de tablas

| Tabla | Paquete o paquetes principales | Evidencia observada |
| --- | --- | --- |
| `Compensacion.DerivacionDRP` | `Compensacion_DerivacionDRP.dtsx` | `OpenRowset`, `SELECT` |
| `Compensacion.DerivacionDRPFlujoEstado` | `Compensacion_DerivacionDRP_Update.dtsx` | `OpenRowset` |
| `Compensacion.MargenDetalleGrupoProducto` | `Compensacion_MargenDetalleGrupoProducto.dtsx` | `OpenRowset` |
| `Compensacion.MargenesContrato` | `600_MargenesContratos.dtsx` | `OpenRowset` |
| `Compensacion.MargenPublicacionHistorico` | `999_MargenPublicacion.dtsx`, `999_MargenPublicacion_5Dias.dtsx`, `PersonasEntrega.dtsx` | `OpenRowset`, `DELETE` |
| `Compensacion.MiembroCompensadorEmail` | `Personas_Usuario.dtsx` | `OpenRowset`, `SELECT` |
| `Compensacion.MiembroCompensadorEmailPorMotivo` | `Personas_Usuario.dtsx` | `OpenRowset`, `SELECT` |
| `Compensacion.ParametroContratoPublicacion` | `Compensacion_ParametroContratoPublicacion.dtsx` | `OpenRowset`, `UPDATE`, `SELECT` |
| `Compensacion.SimulacionContratoPublicacion` | `SimulacionContratoPublicacion.dtsx` | `OpenRowset` |
| `Compensacion.SimulacionEscenarioPublicacion` | `SimulacionEscenarioPublicacion.dtsx` | `OpenRowset` |

## Tablas sin evidencia observada

- `Compensacion.MargenPublicacion`
- `Compensacion.SaldoOpcion`

## Nota

La diferencia entre `MargenPublicacionHistorico` y `MargenPublicacion`, junto con variantes de `999_*`, merece una lectura posterior mas fina.

## Artefactos de soporte

- [compensacion-tablas-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/compensacion-tablas-matriz.csv)
