# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Portfolio`
- Esquema destino: `Registro`
- Clasificacion: `sincronizada`
- Dominio funcional: `Registro`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Registro.Portfolio` se llena mediante `Registro_Portfolio.dtsx`. La evidencia visible muestra un patron de `DELETE` previo y `OpenRowset` al destino, lo que sugiere una recarga o reconstruccion de la tabla publicada.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Registro_Portfolio.dtsx` | carga principal | recurrente | paquete activo y especifico |

## Mecanismo tecnico

- Tipo de carga: `delete + openrowset`
- Tarea o data flow: carga de portfolio
- Stored procedure: no observado en la evidencia principal
- SQL relevante: `DELETE [Registro].[Portfolio]`
- Tabla relacionada: `InsertPortfolio` aparece como referencia auxiliar

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `Registro_Portfolio.dtsx` | comando SQL | aparece `DELETE [Registro].[Portfolio]` |
| tabla destino | `Registro_Portfolio.dtsx` | componente destino | `OpenRowset` apunta a `[Registro].[Portfolio]` |

## Hechos observados

- El paquete es especifico de la entidad.
- La tabla aparece como destino explicito.

## Inferencias

- `Registro.Portfolio` parece ser una tabla de publicacion consolidada y no simplemente una tabla transaccional.

## Dudas abiertas

- Si la recarga es completa o segmentada.
- Como se vincula con `PortfolioDetalle` y `PortfolioResumen`, que hoy no muestran evidencia explicita en SSIS.

## Clasificacion final

- Motivo de clasificacion: destino explicito con borrado previo en paquete activo.
- Riesgo de error: bajo.
- Proxima validacion sugerida: profundizar el circuito completo del subdominio portfolio.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Registro_Portfolio.dtsx`
- Fecha de analisis: `2026-08-10`
