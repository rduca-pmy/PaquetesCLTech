# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `TarifaDevengadaStage`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / Tarifas`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.TarifaDevengadaStage` se llena mediante `Productos_TarifaDevengada.dtsx`. La evidencia visible es un `OpenRowset` directo al destino, dentro del mismo job que carga `TarifaDevengada`.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Productos_TarifaDevengada.dtsx` | carga principal | recurrente | paquete especifico del circuito de tarifas |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: etapa intermedia de tarifas devengadas
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[TarifaDevengadaStage]`
- Tablas relacionadas: `Productos.TarifaDevengada`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Productos_TarifaDevengada.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El mismo paquete carga stage y tabla final.
- La evidencia no muestra por si sola si la stage queda persistida como parte del modelo o como apoyo tecnico.

## Inferencias

- Es probable que funcione como zona intermedia de preparacion antes de consolidar `TarifaDevengada`.

## Dudas abiertas

- Si AP5 consulta esta tabla directamente o si solo soporta el proceso ETL.

## Clasificacion final

- Motivo de clasificacion: destino explicito en paquete especializado.
- Riesgo de error: bajo para la relacion tecnica, medio para el rol funcional exacto.
- Proxima validacion sugerida: rastrear consumo posterior de la tabla dentro de AP5.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Productos_TarifaDevengada.dtsx`
- Fecha de analisis: `2026-08-11`
