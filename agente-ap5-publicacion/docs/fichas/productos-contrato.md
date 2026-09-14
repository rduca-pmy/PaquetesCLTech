# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Contrato`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.Contrato` se llena principalmente desde `040_Productos.dtsx` y recibe actualizaciones adicionales desde `Horus_Productos_Contrato.dtsx`. La evidencia observada combina `OpenRowset` y `UPDATE` sobre la misma tabla.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete troncal del esquema |
| `Horus_Productos_Contrato.dtsx` | actualizacion complementaria | recurrente | especializado para circuito Horus |

## Mecanismo tecnico

- Tipo de carga: `openrowset + update`
- Tarea o data flow: carga de productos y actualizacion Horus
- Stored procedure: no observado en la evidencia principal
- SQL relevante: `UPDATE [Productos].[Contrato]`
- Tabla relacionada: `Productos.Subyacente`, `Productos.Futuro`, `Productos.Opcion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a `[Productos].[Contrato]` |
| update | `Horus_Productos_Contrato.dtsx` | comando SQL / componente destino | aparece `UPDATE [Productos].[Contrato]` y `OpenRowset` |

## Hechos observados

- La tabla se alimenta por al menos dos paquetes activos.
- Uno de ellos es generalista y el otro especializado.

## Inferencias

- `Productos.Contrato` es una entidad central del esquema y sirve de pivote para otros subtipos de producto.

## Dudas abiertas

- Como se reparten funcionalmente `040_Productos` y `Horus_Productos_Contrato`.

## Clasificacion final

- Motivo de clasificacion: destino explicito observado en mas de un paquete activo.
- Riesgo de error: bajo.
- Proxima validacion sugerida: reconstruir el alcance funcional del circuito Horus.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`, `Horus_Productos_Contrato.dtsx`
- Fecha de analisis: `2026-08-10`
