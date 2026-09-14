# Criterios de extraccion

## Senales tecnicas prioritarias

- nombre del paquete
- presencia o ausencia en `Publicacion.dtproj`
- nombres de tareas y data flows
- `SqlCommand`
- `OpenRowset`
- `Execute SQL Task`
- comandos `INSERT`, `UPDATE`, `DELETE`, `MERGE`
- llamadas a stored procedures
- referencias a esquemas de `Publicacion`
- referencias a esquemas u objetos de `Clearing`
- definiciones de stored procedures y tipos tabla en `Clearing.sql` y `Publicacion.sql`

## Prioridad de evidencia

1. Tabla destino nombrada explicitamente en SQL o componente destino.
2. Stored procedure nombrado explicitamente y asociado a la tarea.
3. Objeto confirmado en `Publicacion.sql` o `Clearing.sql`.
4. Tabla inferida por contexto del nombre del paquete.
5. Tabla inferida por nombres de columnas o comentarios del flujo.

## Criterios para marcar una tabla como sincronizada

- aparece como destino de carga, merge o update en `Publicacion`
- la operacion proviene de un paquete de `IntegrationServices/Publicacion`
- existe evidencia repetible en el `.dtsx`

## Criterios para marcar una tabla como local AP5

- no aparece como destino de sincronizacion
- solo se usa como soporte interno, temporal, pivot o post-proceso
- su uso observado no depende de una extraccion desde `Clearing`

## Criterios para marcar confianza

- `alta`: tabla y mecanismo explicitamente visibles
- `media`: tabla visible, pero mecanismo o origen parcial
- `baja`: conclusion apoyada principalmente en inferencias

## Regla de redaccion

Cada afirmacion importante debe poder responder:

- donde se vio
- en que paquete
- en que tarea o comando
- con que nivel de confianza
