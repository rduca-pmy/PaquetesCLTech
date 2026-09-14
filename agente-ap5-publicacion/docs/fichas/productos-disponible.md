# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Disponible`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.Disponible` se llena mediante `040_Productos.dtsx`. La evidencia combina `UPDATE` y `OpenRowset`, por lo que el job no solo inserta sino que tambien corrige registros existentes.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete troncal del esquema |

## Mecanismo tecnico

- Tipo de carga: `update + openrowset`
- Tarea o data flow: carga general de productos
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `UPDATE [Productos].[Disponible]`
- Tablas relacionadas: `Productos.DisponibleDeFuturo`, `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| update | `040_Productos.dtsx` | comando SQL | aparece `UPDATE [Productos].[Disponible]` |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- Se carga dentro del flujo general de tipos de producto.
- El patron tecnico es similar al de otros subtipos del paquete `040`.

## Inferencias

- `Disponible` es un subtipo operativo del contrato/producto maestro publicado.

## Dudas abiertas

- Si la actualizacion responde a enriquecimiento de atributos o a depuracion de vigencias.

## Clasificacion final

- Motivo de clasificacion: paquete principal con evidencia explicita.
- Riesgo de error: bajo.
- Proxima validacion sugerida: reconstruir la secuencia exacta de `UPDATE` e insercion.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
