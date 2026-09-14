# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `PortfolioDetalle`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos / Portfolio`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.PortfolioDetalle` se llena mediante `950_PortfolioDeActivos.dtsx`. La evidencia observada es un `OpenRowset` directo al destino, por lo que la relacion paquete-tabla es explicita.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `950_PortfolioDeActivos.dtsx` | carga principal | recurrente | paquete especifico para detalle de portfolio de activos |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de portfolio de activos
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Activos].[PortfolioDetalle]`
- Tablas relacionadas: `Registro.Portfolio`, `Activos.MovimientoPublicacion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `950_PortfolioDeActivos.dtsx` | componente destino | `OpenRowset` apunta a `[Activos].[PortfolioDetalle]` |

## Hechos observados

- El nombre del paquete y la tabla estan alineados funcionalmente.
- La evidencia visible es directa sobre el destino.

## Inferencias

- La tabla participa del despliegue de portfolio publicado en AP5 para el dominio de activos.

## Dudas abiertas

- Si la carga se reconstruye completa o por segmentos.

## Clasificacion final

- Motivo de clasificacion: destino explicito en paquete especifico.
- Riesgo de error: bajo.
- Proxima validacion sugerida: reconstruir la consulta origen del paquete `950`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `950_PortfolioDeActivos.dtsx`
- Fecha de analisis: `2026-08-11`
