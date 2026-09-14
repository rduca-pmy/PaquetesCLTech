# Metodologia de analisis CDC

## Preguntas guia

- Que funciones CDC existen en `Clearing.sql`
- Que esquema y objeto funcional parecen publicar
- Que tabla o conjunto de tablas de AP5 podrian estar alimentando
- En que casos el circuito CDC complementa o reemplaza lo visible en SSIS

## Unidad de trabajo

La unidad recomendada para esta fase es:

- una funcion `cdc.fn_cdc_get_*`
- un objeto funcional inferido
- una posible tabla o familia de tablas destino en AP5

## Evidencias buscadas

- nombre exacto de la funcion CDC
- patron de nombre `fn_cdc_get_<Esquema>_<Objeto>_Publicacion`
- variantes `OLD` o `old`
- tablas o vistas referenciadas dentro de la funcion
- objetos equivalentes en `Publicacion.sql`
- coincidencias con matrices y fichas ya documentadas

## Clasificaciones sugeridas

- `mapeo_directo`: la funcion CDC apunta con alta confianza a una tabla ya conocida en AP5
- `mapeo_probable`: la funcion y el objeto AP5 coinciden por nombre o dominio, pero falta evidencia interna
- `mapeo_ambiguo`: hay varias tablas posibles o la nomenclatura no alcanza
- `sin_destino_ap5_identificado`: existe funcion CDC pero aun no se encontro tabla destino clara

## Secuencia recomendada

1. Inventario de funciones CDC
2. Agrupacion por esquema funcional
3. Cruce con tablas documentadas en AP5
4. Ficha CDC por funcion o por familia funcional
5. Consolidacion del circuito `Clearing -> CDC -> AP5`

## Criterio de cierre

Una ficha CDC se considera util cuando deja asentado:

- funcion CDC identificada
- esquema y objeto inferidos
- tabla AP5 candidata o relacionada
- evidencia directa
- inferencias y dudas abiertas
