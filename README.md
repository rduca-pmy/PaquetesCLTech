# Documentacion AP5 Publicacion

Repositorio de documentacion para relevar como se llenan las tablas de `Publicacion` (AP5) a partir de procesos de PBP/Clearing.

El trabajo principal vive en [agente-ap5-publicacion](agente-ap5-publicacion/README.md), donde estan la arquitectura de arneses, matrices, fichas por tabla y mapeos CDC.

## Objetivo

Responder de forma trazable:

- Que tablas de AP5 se llenan desde procesos de publicacion.
- Que paquete, CDC, procedimiento o mecanismo alimenta cada tabla.
- Que evidencia sostiene cada relacion.

## Alcance

La documentacion se construye usando como insumos locales:

- `IntegrationServices/Publicacion`
- `Clearing.sql`
- `Publicacion.sql`

Esos insumos no se versionan en este repositorio. Quedan excluidos por `.gitignore` para evitar subir codigo fuente, dumps de esquema o repositorios externos.

## Navegacion rapida

- [README del agente documental](agente-ap5-publicacion/README.md)
- [Contexto y alcance](agente-ap5-publicacion/docs/00-contexto-y-alcance.md)
- [Arquitectura de arneses](agente-ap5-publicacion/docs/01-arquitectura-de-arneses.md)
- [Inventario inicial de paquetes](agente-ap5-publicacion/docs/04-inventario-inicial-paquetes.md)
- [Inventario CDC](agente-ap5-publicacion/docs/cdc/02-inventario-inicial-cdc.md)
- [Mapeo CDC primera tanda](agente-ap5-publicacion/docs/cdc/03-mapeo-primer-tanda-cdc.md)
- [Mapeo CDC segunda tanda](agente-ap5-publicacion/docs/cdc/04-mapeo-segunda-tanda-cdc.md)

## Estado actual

- Documentacion por esquemas y tablas basada en paquetes SSIS.
- Fichas detalladas para tablas sincronizadas relevantes.
- Fase CDC separada en `agente-ap5-publicacion/docs/cdc`.
- `IntegrationServices`, `Clearing.sql` y `Publicacion.sql` ignorados intencionalmente.

## Nota de trabajo

Este repo versiona la documentacion y artefactos derivados del analisis. Los insumos fuente deben permanecer locales o gestionarse desde sus repositorios/sistemas correspondientes.
