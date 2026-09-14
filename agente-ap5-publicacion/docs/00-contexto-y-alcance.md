# Contexto y alcance

## Contexto funcional

- `Clearing` corresponde a la plataforma PBP (`Postrade Backoffice Platform`).
- `Publicacion` corresponde a AP5 (`Anywhere Portfolio 5`).
- En terminos generales, PBP procesa acciones de post-trade y AP5 expone informacion orientada al cliente final.
- La informacion viaja principalmente desde PBP hacia AP5 para su publicacion.
- Esa transferencia puede materializarse por paquetes, jobs, contribuciones o CDCs, segun el caso.
- En ambas aplicaciones, gran parte de la logica relevante vive en base de datos; los frontends no son la fuente prioritaria de analisis.

## Problema a resolver

Se necesita documentar de forma consistente:

1. Que tablas de AP5 reciben datos mediante sincronizaciones.
2. Con que paquete o job se llenan.
3. Que mecanismo tecnico ejecuta la carga, actualizacion o merge.
4. Que evidencia del paquete respalda esa conclusion.

## Preguntas rectoras

- Como se llenan las tablas de AP5?
- Cuales son las tablas que se llenan en AP5?
- Que tablas no surgen de sincronizaciones y parecen ser propias de AP5?

## Alcance de esta etapa

- Analizar solo `IntegrationServices/Publicacion`.
- Tomar como fuente principal los paquetes `.dtsx`.
- Tomar como fuentes logicas complementarias `Clearing.sql` y `Publicacion.sql`.
- Diseñar la arquitectura de arneses y la forma de documentar hallazgos.
- Preparar un template uniforme para las futuras fichas.

## Fuera de alcance por ahora

- Escanear otras carpetas del repositorio `IntegrationServices`.
- Analizar funciones CDC de PBP.
- Relevar colas, servicios o componentes externos al proyecto `Publicacion`.
- Confirmar semanticamente cada tabla con usuarios funcionales.

## Supuestos de trabajo

- Los paquetes `.dtsx` contienen evidencia suficiente para detectar muchas sincronizaciones.
- Las tablas destino de AP5 pueden aparecer en comandos SQL embebidos, componentes OLE DB o stored procedures tipo `Merge*`.
- Los esquemas SQL permiten reconstruir objetos, stored procedures, tipos tabla y relaciones logicas que no siempre quedan claros desde SSIS solamente.
- No toda tabla de `Publicacion` sera una tabla sincronizada; algunas seran tablas locales, pivot o de soporte funcional.
