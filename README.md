# Proyecto Final

# Tabla de contenido

# I. Introducci?n

# II. Contexto del proyecto

{TODO diagrama de contexto del proyecto png}

{TODO diagrama de contexto codigo fuente uml - una referencia}

## 2.1. Problemas que se prenden resolver

La gesti?n de los procesos escolares implica el manejo constante de informaci?n relacionada con alumnos, profesores, asignaturas, periodos acad?micos, inscripciones y evaluaciones. Cuando estos procesos se administran mediante procedimientos separados o registros no centralizados, pueden presentarse dificultades para consultar, actualizar y mantener la consistencia de la informaci?n.

Entre los principales problemas que se buscan atender se encuentran:

- **Dispersi?n de la informaci?n acad?mica:** La informaci?n de alumnos, profesores, materias y evaluaciones puede encontrarse distribuida en diferentes registros, dificultando su consulta y actualizaci?n.
- **Inconsistencias en los procesos de inscripci?n:** La selecci?n de asignaturas puede generar conflictos cuando no se validan adecuadamente los horarios, requisitos acad?micos y cupos disponibles.
- **Dificultades en la administraci?n de periodos escolares:** La falta de control centralizado sobre las fechas de inicio, finalizaci?n y ventanas de captura puede ocasionar confusiones en los procesos acad?micos.
- **Conflictos en la programaci?n de espacios y evaluaciones:** La asignaci?n de aulas y horarios requiere verificar la disponibilidad de los espacios y evitar empalmes entre actividades, alumnos y profesores.
- **Errores en el registro de calificaciones:** La captura, modificaci?n y oficializaci?n de resultados requiere controles que garanticen la integridad de la informaci?n y permitan identificar a los responsables de cada operaci?n.
- **Falta de seguimiento acad?mico:** La consulta del avance curricular, historial de calificaciones y situaci?n escolar requiere informaci?n relacionada entre diferentes ?reas del sistema.

Ante estas necesidades, se propone un Sistema de Control Escolar modular que permita organizar los procesos, establecer validaciones y facilitar el intercambio de informaci?n entre las diferentes ?reas acad?micas y administrativas.
## 2.2. Oportunidades que buscan aprovechar

El desarrollo del Sistema de Control Escolar representa una oportunidad para mejorar la organizaci?n y administraci?n de los procesos acad?micos mediante una soluci?n modular e integrada.

Entre las principales oportunidades que se buscan aprovechar se encuentran:

- **Centralizaci?n de la informaci?n:** Integrar los registros de alumnos, profesores, asignaturas, periodos y evaluaciones para facilitar su consulta y actualizaci?n.
- **Automatizaci?n de validaciones:** Incorporar mecanismos que permitan verificar requisitos de inscripci?n, disponibilidad de cupos, periodos de captura y condiciones para presentar ex?menes.
- **Mejor coordinaci?n acad?mica:** Facilitar la relaci?n entre los m?dulos de inscripciones, asignaturas, calendario de ex?menes, aulas y registro de calificaciones.
- **Mayor integridad y trazabilidad:** Establecer controles para identificar modificaciones, conservar historiales y mantener registros consistentes.
- **Acceso organizado a la informaci?n:** Permitir que cada usuario consulte y realice las operaciones correspondientes de acuerdo con sus responsabilidades.
- **Generaci?n de informaci?n acad?mica:** Facilitar la consulta de resultados, historiales, reportes de aprovechamiento y datos relacionados con la actividad escolar.
- **Facilidad de mantenimiento y crecimiento:** Utilizar una estructura modular que permita actualizar o ampliar funcionalidades sin modificar innecesariamente el resto del sistema.

Estas oportunidades buscan establecer una base para mejorar la administraci?n escolar y facilitar la integraci?n de los diferentes procesos institucionales.
# III. Alcance del proyecto

El proyecto contempla el an?lisis y dise?o de un Sistema de Control Escolar integrado por m?dulos que permiten gestionar diferentes actividades acad?micas y administrativas. Cada m?dulo cuenta con responsabilidades espec?ficas y establece relaciones con otros componentes para compartir la informaci?n necesaria.

El alcance general comprende los siguientes procesos:

- Administraci?n de informaci?n de alumnos y profesores.
- Gesti?n de periodos escolares y procesos de inscripci?n.
- Consulta y administraci?n de asignaturas, materias y planes de estudio.
- Organizaci?n de grupos y asignaci?n de aulas.
- Programaci?n y consulta de calendarios de ex?menes.
- Administraci?n del cat?logo de tipos de examen y sus requisitos.
- Captura, consulta, revisi?n y oficializaci?n de calificaciones.
- Administraci?n de informaci?n acad?mica y generaci?n de reportes relacionados con los procesos escolares.

La propuesta tambi?n contempla la definici?n de actores, permisos, requerimientos funcionales y no funcionales, as? como modelos UML y diagramas de arquitectura que permitan describir la estructura y las interacciones del sistema.
## 3.1 Limites del proyecto
El sistema se enfoca en los procesos acad?micos y administrativos relacionados directamente con el control escolar. Su funcionamiento se delimita a las responsabilidades establecidas para cada m?dulo y a la informaci?n necesaria para mantener la comunicaci?n entre ellos.

Los principales l?mites son:

Cada m?dulo administra ?nicamente las funciones que le corresponden.

La programaci?n de ex?menes se gestiona desde el m?dulo Calendario de Ex?menes, mientras que el registro de resultados corresponde al m?dulo Registro de Calificaciones.

El Cat?logo de Ex?menes administra los tipos de evaluaci?n y sus requisitos, pero no programa fechas, horarios ni aulas.

El m?dulo de Profesores administra la informaci?n docente, pero no contempla la gesti?n de n?mina ni contrataci?n.

Los procesos de inscripci?n dependen de la informaci?n acad?mica, los periodos vigentes y la disponibilidad de grupos y asignaturas.

Las operaciones administrativas deben realizarse conforme a los permisos definidos para cada tipo de usuario.
## 3.2 Exclusiones
Quedan fuera del alcance principal del proyecto las siguientes funcionalidades:

Administraci?n de n?mina, pagos salariales y procesos de contrataci?n de profesores.

Gesti?n financiera y contable general de la instituci?n.

Implementaci?n de servicios externos de correo y notificaciones como componentes obligatorios.

Desarrollo de un repositorio institucional independiente para almacenar temarios.

Gesti?n de procesos ajenos a las actividades acad?micas y administrativas documentadas en los m?dulos.

Las posibles integraciones con servicios externos, como autenticaci?n institucional, correo electr?nico y repositorios de documentos, se consideran propuestas que requieren validaci?n antes de formar parte de una implementaci?n definitiva.
# IV. Requerimientos
Los requerimientos del Sistema de Control Escolar establecen las funcionalidades y condiciones que debe cumplir cada m?dulo para satisfacer las necesidades de los usuarios. Se dividen en requerimientos funcionales, que describen las operaciones que debe realizar el sistema, y requerimientos no funcionales, que establecen las caracter?sticas de calidad, seguridad y desempe?o esperadas.
## 4.1 Requerimientos funcionales (RF)
Los requerimientos funcionales describen las operaciones que permiten administrar y consultar la informaci?n acad?mica y escolar. De acuerdo con la organizaci?n modular del proyecto, se identifican las siguientes funcionalidades generales:

Gesti?n de alumnos: Registrar, consultar y actualizar la informaci?n personal y acad?mica de los estudiantes.

Gesti?n de profesores: Administrar los registros docentes y permitir la consulta y actualizaci?n del perfil propio.

Gesti?n de periodos escolares: Registrar, activar y finalizar periodos, as? como configurar las ventanas de captura de calificaciones.

Gesti?n de inscripciones: Consultar la oferta acad?mica, seleccionar asignaturas, validar horarios y cupos, y confirmar inscripciones.

Gesti?n de asignaturas: Consultar y administrar materias, planes de estudio, seriaci?n y avance curricular.

Gesti?n de aulas y grupos: Administrar espacios, capacidades y recursos, as? como validar su disponibilidad y asignaci?n.

Calendario de ex?menes: Programar evaluaciones, asignar horarios y espacios, detectar conflictos y permitir consultas personalizadas.

Cat?logo de ex?menes: Registrar tipos de examen, configurar requisitos y establecer esquemas de evaluaci?n.

Registro de calificaciones: Capturar resultados, generar y oficializar actas, gestionar revisiones y rectificaciones, y consultar reportes acad?micos.

Cada m?dulo contiene sus propios requerimientos funcionales detallados, actores y diagramas de casos de uso, los cuales se encuentran documentados en la carpeta modulos del repositorio.
## 4.2 Requerimientos No Funcionales (RNF) 

# V. Modelado del sistema

## 5.1 Diagramas UML (casos de uso, clases, secuencia, etc.)

{TODO - vista general de los modulos - diagrama de herencia de usuarios/roles/actores}

{TODO - vista general de los modulos - diagrama de casos de uso}

{TODO - vista general de los modulos - diagrama de componentes}

## 5.2 Interfaz de usuario (mockups, wireframes)

# ��ndice de Módulos
-
- [Módulo 2: Inscripciones](./modulos/modulo-inscripciones.md)
- 
- [Módulo 4: Asignaturas/Materias](./modulos/m4_asignaturas.md)
-
- [Módulo Registro de calificaciones (Equipo 6)](./modulos/m8_calificaciones.md)
- [Módulo Catálogo de exámenes (Equipo 6)](./modulos/m9_catalogo_examenes.md)

## Autenticación y autorización

{TODO - tabla de aginacion de permisos roles versus modulos}

# Abreviaturas
- **RF:** Requerimiento funcional.
- **RNF:** Requerimiento no funcional.
- **UC:** Caso de uso (*use case*).
- **UML:** Lenguaje Unificado de Modelado.
- **ER:** Modelo entidad-relación.
- **NP:** No presentó (calificación de un alumno que no se presentó al examen).
# Nomenclaturas
Nombres de archivo que usa el Equipo 6:

| Archivo | Qué es | Ejemplo |
|---|---|---|
| `mN_nombre.md` | Documento del módulo N | `m8_calificaciones.md` |
| `ucNN_accion_tipo.puml` | Diagrama de un caso de uso; `tipo` es componentes, secuencia o actividades | `uc01_capturar_calificaciones_secuencia.puml` |
| `estados_objeto.puml` | Diagrama de estados de un objeto | `estados_acta.puml` |
| `eN_nombre.uml` (en `docs/architecture/diagrams`) | Diagrama de arquitectura del equipo N | `e6_clases_calificaciones_catalogo.uml` |
| `.puml` / `.uml` y `.png` | Código fuente PlantUML y su imagen; llevan el mismo nombre | `estados_acta.puml` y `estados_acta.png` |
# Referencias bibliográficas 
