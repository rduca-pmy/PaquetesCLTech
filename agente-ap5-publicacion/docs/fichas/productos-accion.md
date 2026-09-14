# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Accion`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.Accion` se llena mediante `040_Productos.dtsx`. La evidencia encontrada es un `OpenRowset` directo al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete maestro del esquema |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga general de productos
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[Accion]`
- Tablas relacionadas: `Productos.Producto`, `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- Forma parte del set de subtipos base del modelo.
- No se detectaron paquetes alternativos.

## Inferencias

- La tabla expone la variante accionaria del maestro de productos/contratos.

## Dudas abiertas

- Si existe enriquecimiento posterior por market data fuera del esquema `Productos`.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita en paquete troncal.
- Riesgo de error: bajo.
- Proxima validacion sugerida: contrastar la tabla con circuitos de cotizacion.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
