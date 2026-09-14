# Arquitectura de arneses

## Objetivo

Separar el trabajo del agente en arneses pequenos, auditables y reusables para que la documentacion se pueda generar, revisar y ampliar por etapas.

## Principios

- Alcance estricto: solo `IntegrationServices/Publicacion`.
- Soporte de contexto logico: `Clearing.sql` y `Publicacion.sql`.
- Evidencia primero: toda conclusion debe citar el paquete y la señal tecnica observada.
- Trazabilidad: cada ficha debe poder reconstruirse desde el artefacto fuente.
- Distincion explicita entre hecho, inferencia y duda abierta.
- Iteracion segura: primero paquetes, despues CDCs.

## Arnese 1. Descubrimiento

### Mision

Inventariar todos los paquetes del proyecto `Publicacion` y normalizar sus nombres.

### Entrada

- `Publicacion.dtproj`
- listado de archivos `.dtsx`
- `Clearing.sql`
- `Publicacion.sql`

### Salida

- catalogo de paquetes
- grupos funcionales por prefijo o dominio
- deteccion de duplicados, variantes o paquetes legacy

## Arnese 2. Extraccion tecnica

### Mision

Leer cada `.dtsx` y extraer evidencias tecnicas relevantes.

### Evidencias buscadas

- connection managers `Clearing` y `Publicacion`
- `SqlCommand`
- `Execute SQL Task`
- `OLE DB Source`
- `OLE DB Destination`
- `OLE DB Command`
- llamadas a `Merge*`, `Insert*`, `Update*`, `Delete*`
- referencias a tablas y esquemas de `Publicacion`
- referencias a objetos equivalentes en `Clearing`
- stored procedures y tipos tabla que permitan completar el circuito

### Salida

- evidencia cruda por paquete
- lista preliminar de tablas destino
- lista preliminar de objetos fuente

## Arnese 3. Mapeo de sincronizaciones

### Mision

Transformar evidencia tecnica en relaciones entendibles para negocio y soporte.

### Relaciones a construir

- paquete -> tabla AP5
- paquete -> stored procedure
- stored procedure o SQL -> tabla AP5
- paquete -> posible dominio funcional
- paquete -> tipo de sincronizacion

### Tipos de sincronizacion sugeridos

- carga completa
- merge / upsert
- update puntual
- delete / limpieza
- historizacion
- mantenimiento interno AP5

## Arnese 4. Clasificacion funcional

### Mision

Distinguir tablas sincronizadas desde PBP de tablas locales o de soporte interno AP5.

### Reglas iniciales

- Si una tabla aparece como destino directo de un paquete, se marca como `sincronizada`.
- Si una tabla solo participa en procesos internos de AP5, se marca como `local_ap5`.
- Si la evidencia es incompleta, se marca como `pendiente_validacion`.

## Arnese 5. Generacion documental

### Mision

Crear una ficha estandar por tabla sincronizada o por relacion relevante.

### Salida

- documento Markdown basado en template unico
- nivel de confianza
- evidencias y observaciones

## Arnese 6. Control de calidad

### Mision

Verificar coherencia antes de publicar una ficha.

### Controles minimos

- la tabla destino esta nombrada de forma explicita
- existe al menos una evidencia tecnica citada
- el paquete fuente esta identificado
- el tipo de sincronizacion fue clasificado
- las inferencias estan marcadas como tales

## Secuencia recomendada

1. Descubrimiento
2. Extraccion tecnica
3. Mapeo de sincronizaciones
4. Clasificacion funcional
5. Generacion documental
6. Control de calidad

## Forma de crecimiento

- Fase 1: paquetes SSIS de `Publicacion`
- Fase 2: stored procedures complementarios
- Fase 3: funciones CDC y contribuciones de PBP
- Fase 4: consolidacion end-to-end PBP -> AP5

## Extension para fase CDC

Cuando el proyecto entra en fase CDC, conviene agregar un carril separado con estos arneses especificos:

### Arnese CDC 1. Inventario de funciones

- Entrada: `Clearing.sql`
- Salida: catalogo de `cdc.fn_cdc_get_*`

### Arnese CDC 2. Inferencia funcional

- Entrada: nombre y cuerpo de funcion CDC
- Salida: esquema y objeto funcional inferidos

### Arnese CDC 3. Cruce con AP5

- Entrada: inventario CDC + matrices AP5
- Salida: relacion `funcion CDC -> tabla AP5 candidata`

### Arnese CDC 4. Consolidacion end-to-end

- Entrada: evidencia CDC + fichas SSIS previas
- Salida: circuito consolidado `Clearing -> CDC -> AP5`
