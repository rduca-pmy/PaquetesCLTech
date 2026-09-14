# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `OperacionCarteraMovimientoActivo`
- Esquema destino: `Registro`
- Clasificacion: `sincronizada`
- Dominio funcional: `Registro / Operaciones`
- Nivel de confianza: `media`

## Respuesta corta

La tabla `Registro.OperacionCarteraMovimientoActivo` muestra evidencia en `Registro_OperacionCarteraExtension.dtsx` y en `Registro_OperacionCarteraMovimientoActivo.dtsx`. En ambos casos aparece `OpenRowset` al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Registro_OperacionCarteraExtension.dtsx` | carga complementaria | recurrente | la toca junto con la tabla de extension |
| `Registro_OperacionCarteraMovimientoActivo.dtsx` | carga principal probable | recurrente | paquete especifico de la entidad |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de movimientos de activos por operacion de cartera
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Registro].[OperacionCarteraMovimientoActivo]`
- Tablas relacionadas: `Registro.OperacionCarteraExtension`, `Activos.MovimientoPublicacion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Registro_OperacionCarteraExtension.dtsx` | componente destino | reaparece `OpenRowset` a la tabla |
| tabla destino | `Registro_OperacionCarteraMovimientoActivo.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla es compartida por dos jobs del mismo subdominio.
- Uno de ellos es especifico y el otro la carga en conjunto con la extension.

## Inferencias

- Puede tratarse de una tabla hija que acompana distintas variantes de publicacion de operaciones.

## Dudas abiertas

- Cual de los dos paquetes define la carga base y cual actua como complemento.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita en dos paquetes relacionados.
- Riesgo de error: medio.
- Proxima validacion sugerida: reconstruir el orden y alcance de ambos jobs.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Registro_OperacionCarteraMovimientoActivo.dtsx`
- Fecha de analisis: `2026-08-11`
