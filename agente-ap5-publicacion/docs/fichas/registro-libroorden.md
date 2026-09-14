# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `LibroOrden`
- Esquema destino: `Registro`
- Clasificacion: `sincronizada`
- Dominio funcional: `Registro / Ordenes`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Registro.LibroOrden` se llena mediante `LibroDeOrdenes.dtsx`, archivo hoy fuera de `dtproj`. La evidencia visible es un `OpenRowset` directo a la tabla destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `LibroDeOrdenes.dtsx` | carga principal | recurrente | archivo fuera de `dtproj`, ligado al subdominio de ordenes |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de libro de ordenes
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Registro].[LibroOrden]`
- Tablas relacionadas: `Registro.OperacionCarteraPublicacionHistorico`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `LibroDeOrdenes.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La relacion tecnica paquete-tabla es directa.
- El archivo no esta declarado en el proyecto SSIS activo.

## Inferencias

- Puede ser un paquete historico o desplegado por fuera del `dtproj`, pero sigue siendo relevante para explicar la carga de la tabla.

## Dudas abiertas

- Si el circuito sigue vigente en produccion.

## Clasificacion final

- Motivo de clasificacion: destino explicito, con salvedad por estar fuera de `dtproj`.
- Riesgo de error: bajo en la relacion tecnica, medio en la vigencia operativa.
- Proxima validacion sugerida: confirmar si existe reemplazo dentro del proyecto actual.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `LibroDeOrdenes.dtsx`
- Fecha de analisis: `2026-08-11`
