# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Caucion`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.Caucion` se llena mediante `040_Productos.dtsx`. La evidencia hallada es un `OpenRowset` directo a la tabla destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete maestro del esquema |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga general de productos
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[Caucion]`
- Tablas relacionadas: `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- Forma parte del set de subtipos cargados por el paquete `040`.
- No se vieron otros paquetes directos para la misma tabla.

## Inferencias

- AP5 publica la caucion como instrumento o producto derivado del maestro de contratos.

## Dudas abiertas

- Si la tabla se usa solo para consulta o tambien como apoyo operativo dentro de AP5.

## Clasificacion final

- Motivo de clasificacion: destino explicito en paquete troncal.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar columnas de negocio especificas de caucion.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
