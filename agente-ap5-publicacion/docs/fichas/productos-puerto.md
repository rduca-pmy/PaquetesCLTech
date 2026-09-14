# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Puerto`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.Puerto` se llena mediante `040_Productos.dtsx`. La evidencia hallada es un `OpenRowset` directo al destino dentro del paquete troncal de productos.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete maestro del esquema |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga general de productos
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[Puerto]`
- Tablas relacionadas: `Productos.Forward`, `Productos.ValoresOTCAgro`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a `[Productos].[Puerto]` |

## Hechos observados

- La tabla forma parte del lote general de catalogos/productos.
- No se detectaron paquetes alternativos en la matriz.

## Inferencias

- Se publica como catalogo de apoyo para productos vinculados a granos, embarques o entregas.

## Dudas abiertas

- Si el concepto de puerto es solo geografico o tambien comercial.

## Clasificacion final

- Motivo de clasificacion: destino explicito en el paquete troncal.
- Riesgo de error: bajo.
- Proxima validacion sugerida: relacionar la tabla con los contratos que la consumen.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
