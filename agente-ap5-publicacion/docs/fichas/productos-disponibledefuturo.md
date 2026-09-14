# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `DisponibleDeFuturo`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.DisponibleDeFuturo` se llena mediante `040_Productos.dtsx`. La evidencia observada es un `OpenRowset` directo al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete troncal del esquema |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de subtipos de producto
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[DisponibleDeFuturo]`
- Tablas relacionadas: `Productos.Disponible`, `Productos.Futuro`, `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El nombre de la tabla sugiere una relacion entre instrumentos disponibles y futuros.
- No se observaron paquetes alternativos.

## Inferencias

- AP5 mantiene este subtipo como extension del universo de contratos/instrumentos.

## Dudas abiertas

- Si es una tabla pura de subtipo o una vista materializada de conversion entre productos.

## Clasificacion final

- Motivo de clasificacion: destino explicito en paquete maestro.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar la clave compartida con `Futuro`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
