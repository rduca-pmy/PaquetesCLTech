# Esquema Personas

## Objetivo

Documentar el esquema `Personas` de AP5 y responder, en esta primera version:

- que tablas tiene el esquema en `Publicacion`
- que tablas muestran sincronizacion explicita desde paquetes SSIS
- que tablas aparecen solo con evidencia parcial
- que tablas no muestran evidencia en los paquetes relevados

## Fuente analizada

- Esquema SQL: `Publicacion.sql`
- Proyecto SSIS: `IntegrationServices/Publicacion/Publicacion.dtproj`
- Paquetes foco del dominio:
  - `030_PersonasGeneral.dtsx`
  - `030_PersonasGeneralLight.dtsx`
  - `030_PersonasGeneralViejo.dtsx`
  - `031_CuentaRegistroPublicacion.dtsx`
  - `990_PersonasParte.dtsx`
  - `PersonasEntrega.dtsx`
  - `Personas_CuentaDepositariaPublicacion.dtsx`
  - `Personas_CuentaRegistroCoTitular.dtsx`
  - `Personas_DatosPatrimoniales.dtsx`
  - `Personas_Emisor.dtsx`
  - `Personas_FondoComunInversion.dtsx`
  - `Personas_SociedadDepositaria.dtsx`
  - `Personas_Usuario.dtsx`
  - `Personas_UsuarioMiPortafolio.dtsx`


- Paquetes con evidencia util pero fuera de `dtproj`:
  - `Personas_ArchivoPublicacion.dtsx`
  - `Personas_CuentaRegistroCoTitularUpdate.dtsx`
  - `Persona_PersonaHistorico.dtsx`

## Totales

- Tablas del esquema `Personas` en `Publicacion.sql`: `44`
- Tablas con sincronizacion explicita observada en SSIS: `35`
- Tablas sin evidencia observada en los paquetes relevados: `7`

## Lectura general del esquema

El esquema `Personas` es uno de los mas complejos porque combina:

- cargas generalistas concentradas en `030_PersonasGeneral*`
- paquetes especificos por tabla o subdominio
- variantes activas, light, legacy y algunos artefactos fuera del `dtproj`

El patron dominante observado es:

- conexion `Clearing` como origen
- conexion `Publicacion` como destino
- operaciones de `OpenRowset` sobre tablas de `Personas`
- en muchas tablas, `DELETE` previo y luego `UPDATE` o recarga

## Paquetes activos relevantes

| Paquete | Estado |
| --- | --- |
| `030_PersonasGeneral.dtsx` | `activo_dtproj` |
| `030_PersonasGeneralLight.dtsx` | `activo_dtproj` |
| `030_PersonasGeneralViejo.dtsx` | `activo_dtproj` |
| `031_CuentaRegistroPublicacion.dtsx` | `activo_dtproj` |
| `990_PersonasParte.dtsx` | `activo_dtproj` |
| `PersonasEntrega.dtsx` | `activo_dtproj` |
| `Personas_CuentaDepositariaPublicacion.dtsx` | `activo_dtproj` |
| `Personas_CuentaRegistroCoTitular.dtsx` | `activo_dtproj` |
| `Personas_DatosPatrimoniales.dtsx` | `activo_dtproj` |
| `Personas_Emisor.dtsx` | `activo_dtproj` |
| `Personas_FondoComunInversion.dtsx` | `activo_dtproj` |
| `Personas_SociedadDepositaria.dtsx` | `activo_dtproj` |
| `Personas_Usuario.dtsx` | `activo_dtproj` |
| `Personas_UsuarioMiPortafolio.dtsx` | `activo_dtproj` |
| `Personas_ArchivoPublicacion.dtsx` | `fuera_dtproj` |
| `Personas_CuentaRegistroCoTitularUpdate.dtsx` | `fuera_dtproj` |
| `Persona_PersonaHistorico.dtsx` | `fuera_dtproj` |

## Matriz inicial de tablas

### Tablas con sincronizacion explicita observada

| Tabla | Paquete o paquetes principales | Evidencia observada |
| --- | --- | --- |
| `Personas.ArchivoPublicacion` | `Personas_ArchivoPublicacion.dtsx` | `OpenRowset` |
| `Personas.ClasificacionParticipanteCnv` | `030_PersonasGeneral*` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Personas.CuentaCompensacion` | `030_PersonasGeneral*` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Personas.CuentaDepositariaPublicacion` | `Personas_CuentaDepositariaPublicacion.dtsx` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Personas.CuentaEntrega` | `PersonasEntrega.dtsx` | `OpenRowset` |
| `Personas.CuentaEntregaDetalle` | `PersonasEntrega.dtsx` | `OpenRowset` |
| `Personas.CuentaFacturacion` | `030_PersonasGeneral*` | `OpenRowset` |
| `Personas.CuentaNeteo` | `030_PersonasGeneral*` | `OpenRowset` |
| `Personas.CuentaNeteoPublicacion` | `030_PersonasGeneralViejo.dtsx` | `UPDATE`, `OpenRowset` |
| `Personas.CuentaRegistro` | `030_PersonasGeneral*` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Personas.CuentaRegistroCoTitular` | `Personas_CuentaRegistroCoTitular.dtsx`, `Personas_CuentaRegistroCoTitularUpdate.dtsx` | `OpenRowset`, `UPDATE` |
| `Personas.CuentaRegistroEntidadBursatil` | `030_PersonasGeneral*`, `031_CuentaRegistroPublicacion.dtsx` | `DELETE`, `OpenRowset` |
| `Personas.CuentaRegistroParticipante` | `030_PersonasGeneral*` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Personas.CuentaRegistroPublicacion` | `030_PersonasGeneral*`, `031_CuentaRegistroPublicacion.dtsx` | `OpenRowset` |
| `Personas.DatosPatrimoniales` | `Personas_DatosPatrimoniales.dtsx` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Personas.Emisor` | `Personas_Emisor.dtsx` | `UPDATE`, `OpenRowset` |
| `Personas.EntidadBursatil` | `030_PersonasGeneral*` | `DELETE`, `OpenRowset` |
| `Personas.EntidadLiquidadora` | `030_PersonasGeneral.dtsx` | `OpenRowset` |
| `Personas.FondoComunInversion` | `Personas_FondoComunInversion.dtsx`, `Personas_Emisor.dtsx`, `Personas_SociedadDepositaria.dtsx`, `Personas_Usuario.dtsx` | `UPDATE`, `OpenRowset` |
| `Personas.Mercado` | `030_PersonasGeneral*` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Personas.MiembroCompensador` | `030_PersonasGeneral*` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Personas.MiembroCompensadorEntrega` | `PersonasEntrega.dtsx` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Personas.MiembroCompensadorParticipante` | `030_PersonasGeneral*` | `DELETE`, `OpenRowset` |
| `Personas.Parte` | `990_PersonasParte.dtsx` | multiples `INSERT` sobre `OpenRowset` |
| `Personas.Participante` | `030_PersonasGeneral*` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Personas.ParticipanteInterconexion` | `030_PersonasGeneral*` | `OpenRowset` |
| `Personas.PersonaEntrega` | `PersonasEntrega.dtsx` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Personas.PersonaEntregaCategoriaSISA` | `PersonasEntrega.dtsx` | `OpenRowset` |
| `Personas.PersonaHistorico` | `Persona_PersonaHistorico.dtsx` | `DELETE`, `OpenRowset` |
| `Personas.Representante` | `030_PersonasGeneral*` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Personas.SociedadDepositaria` | `Personas_SociedadDepositaria.dtsx` | `UPDATE`, `OpenRowset` |
| `Personas.Usuario` | `Personas_Usuario.dtsx` | `DELETE`, `UPDATE`, `OpenRowset` |
| `Personas.UsuarioAcciones` | `Personas_Usuario.dtsx` | `DELETE`, `OpenRowset` |
| `Personas.UsuarioMiPortafolio` | `Personas_UsuarioMiPortafolio.dtsx` | `OpenRowset` |
| `Personas.UsuarioMultiRol` | `Personas_Usuario.dtsx` | `OpenRowset` |
| `Personas.CompaniaSeguro` | `Personas_CompaniaSeguro.dtsx` | `OpenRowset`,`UPDATE`,`DELETE` |
| `Personas.CuotaPartistaFondoComunInversionPublicacion` | `Personas_CuotaPartistaFondoComunInversion.dtsx` | `OpenRowset`,`UPDATE`,`DELETE` |

### Tablas sin evidencia observada en los paquetes relevados

| Tabla | Observacion inicial |
| --- | --- |
| `Personas.ConfiguracionMargen` | sin referencias en los paquetes analizados |
| `Personas.CuentaAutomatica` | sin referencias en los paquetes analizados |
| `Personas.CuentaNegociacion` | sin referencias en los paquetes analizados |
| `Personas.CuentaRegistroGrupoProductoCancelacion` | sin referencias en los paquetes analizados |
| `Personas.SociedadGarantiaReciproca` | sin referencias en los paquetes analizados |
| `Personas.SolicitudCuentaRegistro` | sin referencias en los paquetes analizados |
| `Personas.SolicitudCuentaRegistroTitularAdicional` | sin referencias en los paquetes analizados |

## Hallazgos clave

- `030_PersonasGeneral.dtsx`, `030_PersonasGeneralLight.dtsx` y `030_PersonasGeneralViejo.dtsx` son el nucleo del esquema.
- Hay tablas que dependen de paquetes especificos y no del generalista, por ejemplo:
  - `CuentaDepositariaPublicacion`
  - `DatosPatrimoniales`
  - `Usuario`
  - `CuentaRegistroCoTitular`
  - `Parte`
- Existen tablas con evidencia util en paquetes fuera de `dtproj`, por ejemplo:
  - `ArchivoPublicacion`
  - `PersonaHistorico`
  - actualizacion puntual de `CuentaRegistroCoTitular`
- `CuentaNeteoPublicacion` solo aparecio en la variante `030_PersonasGeneralViejo.dtsx`, lo cual requiere validacion funcional posterior.

## Riesgos y ambiguedades

- En algunas tablas la evidencia visible es `OpenRowset` sin `DELETE` o `UPDATE` explicito; eso indica destino observado, pero conviene confirmar el patron exacto de carga.
- La coexistencia de `General`, `Light` y `Viejo` sugiere variantes de ejecucion o etapas historicas que todavia no estan resueltas semanticamente.
- La ausencia de referencias SSIS no prueba que una tabla no se llene; puede implicar que se completa por otra via o que depende de logica SQL no relevada aun.

## Artefactos de soporte

- [personas-tablas-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/personas-tablas-matriz.csv)
- [personas-paquete-tabla-matriz.csv](/C:/Users/framos/Documents/Paquetes/agente-ap5-publicacion/data/personas-paquete-tabla-matriz.csv)

## Proximos pasos sugeridos

1. Completar fichas detalladas para las tablas mas centrales del esquema.
2. Reconstituir para `030_PersonasGeneral*` la consulta origen en `Clearing`.
3. Validar si `CuentaNeteoPublicacion`, `ArchivoPublicacion` y `PersonaHistorico` siguen vigentes operativamente.
4. Revisar si las 7 tablas sin evidencia dependen de CDC, logica SQL o acciones internas de AP5.
