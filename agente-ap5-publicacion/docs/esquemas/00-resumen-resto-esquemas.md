# Resumen del resto de esquemas

## Alcance

Este documento consolida la primera cobertura del resto de los esquemas de `Publicacion`, excluyendo:

- `MarketData`, ya documentado por separado
- `Personas`, ya documentado por separado

## Lectura global

- Esquemas con cobertura alta y fuerte presencia SSIS:
  - `Activos`
  - `General`
  - `PersonasGeneral`
  - `Productos`
  - `Sistema`
- Esquemas con cobertura media o focalizada:
  - `Compensacion`
  - `ComprobantesGeneral`
  - `Parametros`
  - `Registro`
- Esquemas con cobertura baja o casi nula desde `Publicacion`:
  - `Contabilidad`
  - `Contribucion`
  - `Mensajes`
  - `MensajesGeneral`

## Hallazgos transversales

- `General` y `PersonasGeneral` muestran cobertura total en los paquetes relevados.
- `Mensajes` y `MensajesGeneral` no muestran evidencia SSIS directa dentro de `IntegrationServices/Publicacion`, lo que sugiere una via alternativa de carga.
- `Contribucion` aparece mucho menos cargado de lo que su cantidad de tablas haria suponer; esto es consistente con el circuito de contribuciones y mensajeria separado del flujo de paquetes.
- `Sistema` tiene muchas tablas, pero una parte importante no aparece en los paquetes relevados, por lo que no conviene asumir que todo se carga por SSIS.

## Resumen cuantitativo

| Esquema | Tablas | Con evidencia en SSIS | Sin evidencia en SSIS |
| --- | ---: | ---: | ---: |
| `Activos` | 20 | 17 | 3 |
| `Compensacion` | 12 | 10 | 2 |
| `ComprobantesGeneral` | 9 | 8 | 1 |
| `Contabilidad` | 4 | 1 | 3 |
| `Contribucion` | 38 | 10 | 28 |
| `General` | 19 | 19 | 0 |
| `Mensajes` | 31 | 0 | 31 |
| `MensajesGeneral` | 5 | 0 | 5 |
| `Parametros` | 32 | 16 | 16 |
| `PersonasGeneral` | 32 | 32 | 0 |
| `Productos` | 44 | 38 | 6 |
| `Registro` | 29 | 15 | 14 |
| `Sistema` | 90 | 56 | 34 |

## Artefacto de soporte

- [esquemas-restantes-resumen.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/esquemas-restantes-resumen.csv)
