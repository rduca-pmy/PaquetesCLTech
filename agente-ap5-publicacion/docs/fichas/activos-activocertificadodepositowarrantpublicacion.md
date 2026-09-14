# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ActivoCertificadoDepositoWarrantPublicacion`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.ActivoCertificadoDepositoWarrantPublicacion` se llena mediante `Activos_ActivoCertificadoDepositoWarrantPublicacion.dtsx`. La evidencia combina `DELETE`, `UPDATE` y `OpenRowset`, por lo que el paquete no solo inserta sino que tambien recompone o corrige el contenido publicado.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Activos_ActivoCertificadoDepositoWarrantPublicacion.dtsx` | carga principal | recurrente | paquete especifico del subtipo de activo |

## Mecanismo tecnico

- Tipo de carga: `delete + update + openrowset`
- Tarea o data flow: publicacion de certificados de deposito y warrant
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `DELETE [Activos].[ActivoCertificadoDepositoWarrantPublicacion]`, `UPDATE [Activos].[ActivoCertificadoDepositoWarrantPublicacion]`
- Tablas relacionadas: `Activos.Activo`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `Activos_ActivoCertificadoDepositoWarrantPublicacion.dtsx` | comando SQL | aparece `DELETE [Activos].[ActivoCertificadoDepositoWarrantPublicacion]` |
| update | `Activos_ActivoCertificadoDepositoWarrantPublicacion.dtsx` | comando SQL | aparece `UPDATE [Activos].[ActivoCertificadoDepositoWarrantPublicacion]` |
| tabla destino | `Activos_ActivoCertificadoDepositoWarrantPublicacion.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El paquete toca tambien `Activos.Activo`.
- La tabla tiene una carga especializada dentro del dominio.

## Inferencias

- La publicacion del subtipo depende de un maestro base de activos y de atributos adicionales del instrumento.

## Dudas abiertas

- Si el paquete opera sobre universo completo o solo sobre certificados vigentes.

## Clasificacion final

- Motivo de clasificacion: destino explicito con operaciones de mantenimiento visibles.
- Riesgo de error: bajo.
- Proxima validacion sugerida: reconstruir la consulta origen y el criterio de borrado.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Activos_ActivoCertificadoDepositoWarrantPublicacion.dtsx`
- Fecha de analisis: `2026-08-11`
