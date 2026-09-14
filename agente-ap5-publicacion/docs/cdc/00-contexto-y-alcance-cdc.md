# Contexto y alcance de la fase CDC

## Objetivo

Separar y documentar el circuito `Clearing -> CDC -> AP5` como una fase distinta del relevamiento de paquetes SSIS.

## Por que se separa

- Los paquetes SSIS muestran principalmente la capa de publicacion ya materializada en AP5.
- Las funciones `cdc` permiten reconstruir mejor el origen PBP de ciertos datos y mensajes.
- El circuito CDC tiene semantica propia y no conviene mezclarlo con la documentacion de jobs `IntegrationServices/Publicacion`.

## Fuentes habilitadas para esta fase

- `Clearing.sql`
- `Publicacion.sql`
- documentacion ya generada en `docs/esquemas`
- fichas ya generadas en `docs/fichas`

## Alcance inicial

- Inventariar funciones del esquema `[cdc]` presentes en `Clearing.sql`
- Inferir a que esquema y objeto funcional parecen corresponder
- Cruzar esas funciones con tablas ya documentadas en AP5
- Preparar la fase posterior de trazabilidad completa `PBP -> CDC -> AP5`

## Fuera de alcance por ahora

- Validar ejecucion real o scheduling de las funciones CDC
- Reconstruir colas, brokers o transporte fisico del mensaje
- Documentar toda la mensajeria de negocio en una sola pasada

## Resultado esperado de esta etapa

- carpeta CDC separada del resto de la documentacion
- inventario inicial de funciones CDC
- metodologia y template de documentacion especificos para CDC
