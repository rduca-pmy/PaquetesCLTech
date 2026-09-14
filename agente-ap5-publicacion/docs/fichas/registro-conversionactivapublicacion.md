# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ConversionActivaPublicacion`
- Esquema destino: `Registro`
- Clasificacion: `sincronizada`
- Dominio funcional: `Registro / Conversiones`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Registro.ConversionActivaPublicacion` se llena mediante `Registro_ConversionActivaPublicacion.dtsx`. La evidencia observada es un `OpenRowset` directo al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Registro_ConversionActivaPublicacion.dtsx` | carga principal | recurrente | paquete especifico de conversion activa |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: publicacion de conversiones activas
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Registro].[ConversionActivaPublicacion]`
- Tablas relacionadas: `Productos.ConversionContrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Registro_ConversionActivaPublicacion.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- Existe un paquete exclusivo para esta publicacion.
- El subdominio de conversiones aparece repartido entre `Productos` y `Registro`.

## Inferencias

- La tabla representa conversiones activas vinculadas a operaciones o posiciones ya registradas.

## Dudas abiertas

- Si reutiliza maestros de `ConversionContrato` o si modela otra capa del negocio.

## Clasificacion final

- Motivo de clasificacion: paquete especializado con destino explicito.
- Riesgo de error: bajo.
- Proxima validacion sugerida: contrastar con el circuito de conversion del esquema `Productos`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Registro_ConversionActivaPublicacion.dtsx`
- Fecha de analisis: `2026-08-11`
