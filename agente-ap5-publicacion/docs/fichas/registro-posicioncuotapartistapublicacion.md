# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `PosicionCuotaPartistaPublicacion`
- Esquema destino: `Registro`
- Clasificacion: `sincronizada`
- Dominio funcional: `Registro / Cuotapartista`
- Nivel de confianza: `media`

## Respuesta corta

La tabla `Registro.PosicionCuotaPartistaPublicacion` se llena mediante `Contribucion_PosicionCuotaPartista.dtsx`. La evidencia observada es un `OpenRowset` directo, aunque el paquete pertenece nominalmente al dominio `Contribucion`.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Contribucion_PosicionCuotaPartista.dtsx` | carga principal observada | recurrente | paquete de otro dominio que publica hacia `Registro` |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: publicacion de posicion de cuotapartistas
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Registro].[PosicionCuotaPartistaPublicacion]`
- Tablas relacionadas: `Productos.FondoComunInversionPublicacion`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Contribucion_PosicionCuotaPartista.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla se carga desde un paquete cuyo prefijo no coincide con el esquema destino.
- La relacion tecnica con el destino es, sin embargo, explicita.

## Inferencias

- El circuito de posicion de cuotapartistas cruza dominios y se materializa en `Registro`.

## Dudas abiertas

- Si existe una carga complementaria desde otro paquete del esquema `Registro`.

## Clasificacion final

- Motivo de clasificacion: destino explicito, con salvedad por provenir de otro dominio.
- Riesgo de error: medio.
- Proxima validacion sugerida: revisar si el paquete consume contribuciones o tablas base de fondos.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Contribucion_PosicionCuotaPartista.dtsx`
- Fecha de analisis: `2026-08-11`
