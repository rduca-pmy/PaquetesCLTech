# Esquema MensajesGeneral

## Resumen

- Tablas en `Publicacion.sql`: `5`
- Tablas con evidencia en SSIS: `0`
- Tablas sin evidencia en SSIS: `5`

## Lectura inicial

Al igual que `Mensajes`, este esquema no muestra evidencia SSIS directa en `IntegrationServices/Publicacion`.

## Matriz inicial de tablas

No se detectaron tablas de `MensajesGeneral` con `OpenRowset`, `DELETE` o `UPDATE` explicito dentro de `IntegrationServices/Publicacion`.

## Tablas sin evidencia observada

- `MensajesGeneral.MensajePublicacionHistorico`
- `MensajesGeneral.Mensaje`
- `MensajesGeneral.MensajePublicacion`
- `MensajesGeneral.Accion`
- `MensajesGeneral.ArchivoAdjuntoMensaje`

## Nota

Probablemente este esquema dependa de otro circuito tecnico ajeno a los paquetes analizados en esta fase.

## Artefactos de soporte

- [mensajesgeneral-tablas-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/mensajesgeneral-tablas-matriz.csv)
