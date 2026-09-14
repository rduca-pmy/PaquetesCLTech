# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Producto`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.Producto` se llena mediante `040_Productos.dtsx`. La evidencia visible es un `OpenRowset` directo al destino dentro del paquete troncal del esquema.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete maestro del dominio |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga general de productos
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[Producto]`
- Tablas relacionadas: `Productos.Contrato`, `Productos.Accion`, `Productos.Titulo`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a `[Productos].[Producto]` |

## Hechos observados

- La tabla es central para el esquema.
- No se detectaron paquetes alternativos en la matriz.

## Inferencias

- Puede actuar como maestro base del que dependen varios subtipos especificos.

## Dudas abiertas

- Si `Producto` y `Contrato` conviven como maestros separados o si uno extiende al otro.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita en paquete troncal.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar el modelo relacional entre `Producto` y `Contrato`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
