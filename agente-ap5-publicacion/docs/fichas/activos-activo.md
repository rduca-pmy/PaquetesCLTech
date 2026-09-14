# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Activo`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.Activo` se llena principalmente mediante `920_Activos.dtsx`, donde se observa un patron de `DELETE`, `UPDATE` y `OpenRowset` explicito al destino. Ademas, la tabla reaparece como apoyo o reutilizacion en otros paquetes del dominio y de dominios consumidores.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `920_Activos.dtsx` | carga principal de la tabla | recurrente | paquete troncal del esquema |
| `Activos_ActivoCertificadoDepositoWarrantPublicacion.dtsx` | reutilizacion / relacion de soporte | recurrente | toca `Activo` junto con una tabla publicacion especifica |
| `Comprobantes_Facturacion.dtsx` | referencia operativa | recurrente | usa `Activo` en un flujo de consumo |
| `Comprobantes_Liquidaciones.dtsx` | referencia operativa | recurrente | usa `Activo` en un flujo de consumo |
| `Comprobantes_ManualPublicacion.dtsx` | referencia operativa | recurrente | usa `Activo` en un flujo de consumo |
| `Contrato_Personas_Cotizaciones_StockWatch.dtsx` | referencia operativa | recurrente | usa `Activo` en un flujo de consumo |
| `Registro_AgrupamientoOfertaEntregaPublicacion.dtsx` | referencia operativa | recurrente | usa `Activo` en un flujo de consumo |

## Mecanismo tecnico

- Tipo de carga: `delete + update + openrowset`
- Tarea o data flow: carga central del paquete `920_Activos.dtsx`
- Stored procedure: no observado en la evidencia principal
- SQL relevante: `DELETE [Activos].[Activo]`, `UPDATE [Activos].[Activo]`
- Tablas relacionadas: `Activos.FuenteCotizacionActivo`, `Activos.ActivoPublicacion*`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| carga principal | `920_Activos.dtsx` | flujo de carga | aparecen `DELETE`, `UPDATE` y `OpenRowset` hacia `[Activos].[Activo]` |
| reutilizacion | `Activos_ActivoCertificadoDepositoWarrantPublicacion.dtsx` | componente destino / lookup | aparece `OpenRowset` a `[Activos].[Activo]` |
| consumo | `Comprobantes_Facturacion.dtsx` | componente destino / referencia | aparece `OpenRowset` a `[Activos].[Activo]` |

## Hechos observados

- `920_Activos.dtsx` es el paquete mas claro para esta tabla.
- La tabla es central y reaparece en varios paquetes de otros dominios.
- La evidencia del paquete principal es explicita y suficiente.

## Inferencias

- `Activos.Activo` funciona como maestro de activos publicado en AP5.

## Dudas abiertas

- Que origen exacto en `Clearing` alimenta el maestro.
- Si la carga es total o incremental por subconjuntos de activos.

## Clasificacion final

- Motivo de clasificacion: destino explicito en el paquete troncal del esquema.
- Riesgo de error: bajo.
- Proxima validacion sugerida: reconstruir la consulta origen de `920_Activos.dtsx`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `920_Activos.dtsx`
- Fecha de analisis: `2026-08-10`
