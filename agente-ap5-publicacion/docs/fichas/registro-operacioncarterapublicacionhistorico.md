# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `OperacionCarteraPublicacionHistorico`
- Esquema destino: `Registro`
- Clasificacion: `sincronizada`
- Dominio funcional: `Registro / Operaciones`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Registro.OperacionCarteraPublicacionHistorico` se llena mediante `050_Registro.dtsx` y `050_Registro_Ampliado.dtsx`. La evidencia visible es `OpenRowset` al destino en ambos paquetes, lo que indica un circuito compartido para la publicacion historica.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `050_Registro.dtsx` | carga principal | recurrente | paquete troncal del esquema |
| `050_Registro_Ampliado.dtsx` | ampliacion o variante | recurrente | extiende el circuito base |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: publicacion historica de operaciones de cartera
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Registro].[OperacionCarteraPublicacionHistorico]`
- Tablas relacionadas: `Registro.OperacionCarteraPublicacion`, `Registro.OperacionCarteraExtension`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `050_Registro.dtsx` | componente destino | `OpenRowset` apunta a la tabla |
| tabla destino | `050_Registro_Ampliado.dtsx` | componente destino | reaparece `OpenRowset` al mismo destino |

## Hechos observados

- La tabla depende de mas de una variante del paquete de registro.
- El sufijo `Historico` sugiere persistencia de eventos u operaciones cerradas.

## Inferencias

- AP5 conserva una publicacion historica de operaciones separada de otras vistas vigentes.

## Dudas abiertas

- Como se reparte la responsabilidad entre la variante base y la ampliada.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita en dos paquetes del circuito principal.
- Riesgo de error: bajo.
- Proxima validacion sugerida: comparar diferencias funcionales entre `050_Registro` y `050_Registro_Ampliado`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `050_Registro.dtsx`
- Fecha de analisis: `2026-08-11`
