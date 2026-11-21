# Módulo 2: Inscripciones

## Información del Equipo
- **Equipo:** 2
- **Módulo:** Inscripciones
- **Integrantes:**
    - Pamela Concepción Abasolo Díaz
    - Héctor Jesús García Monroy
    - Kevin Alejandro Nabor Matias
    - Santiago Cuevas Sanchez
  
## 1. Resumen
El Módulo de Inscripciones se encarga de gestionar el proceso de registro y asignación de materias para los alumnos dentro del sistema. Permite validar los requisitos de inscripción, gestionar cupos por grupo y generar los comprobantes o registros correspondientes.

## 2. Objetivo y Alcance
- **Objetivo General:** Automatizar el proceso de inscripción para garantizar un registro ágil y sin duplicidades de alumnos en las asignaturas.
- **Alcance:**
  - Consulta de oferta académica disponible.
  - Selección y validación de asignaturas/horarios.
  - Registro en base de datos y generación de comprobantes.

## 3. Actores
* *Alumno:* Consulta materias disponibles, arma su horario preliminar y solicita su inscripción formal.
* *Administrador / Coordinador:* Abre o cierra los periodos de inscripción, define cupos y valida/ajusta inscripciones cuando sea necesario.
* *Sistema (automatizado):* Valida que no existan traslapes de horario y actualiza los lugares disponibles.

## 4. Requerimientos Funcionales (RF)
* *Consultar oferta académica:* El sistema debe permitir visualizar las materias ofertadas, grupos, docentes asignados y cupos disponibles en tiempo real.
* *Selección de materias:* El sistema debe permitir al alumno agregar o quitar materias a una lista preliminar de inscripción.
* *Validación de choques de horario:* El sistema debe impedir que el alumno inscriba dos materias que compartan el mismo bloque de horario y día.
* *Validación de cupo máximo:* El sistema no debe permitir inscribir a un alumno en un grupo cuyo cupo se encuentre en 0.
* *Confirmar inscripción:* El sistema debe registrar la selección final del alumno, descontar los cupos correspondientes y generar un folio/comprobante de inscripción.
* *Gestión de periodos de inscripción:* El administrador debe poder activar y desactivar las fechas hábiles para que los alumnos puedan inscribirse.
* *Generación de horario/comprobante:* El sistema debe generar una vista resumen imprimible o descargable con el horario final del alumno inscrito.

## 5. Contenido
# 5.1 Diagrama de casos de uso:
```
@startuml
left to right direction

actor "Alumno" as alumno
actor "Administrador / Coordinador" as admin

rectangle "Módulo de Inscripciones" {
usecase "Consultar oferta académica" as UC1
usecase "Seleccionar materias" as UC2
usecase "Confirmar inscripción" as UC3
usecase "Validar traslape de horario" as UC4
usecase "Validar cupo disponible" as UC5
usecase "Descargar comprobante" as UC6
usecase "Abrir / Cerrar periodo" as UC7
usecase "Consultar reporte de inscritos" as UC8
}

alumno --> UC1
alumno --> UC2
alumno --> UC3

UC3 ..> UC4 : <<include>>
UC3 ..> UC5 : <<include>>
UC6 ..> UC3 : <<extend>>


admin --> UC7
admin --> UC8

@enduml
```
![Diagrama de Casos de Uso](resources/imgs/m2_inscripciones_casos_uso.png)


## 6. Abreviaciones
- **BD:** Base de Datos.
- **UI:** Interfaz de Usuario (*User Interface*).

## 7. Requerimientos No Funcionales (RNF)
* *Usabilidad:* La interfaz debe ser intuitiva, permitiendo completar el proceso de inscripción en no más de 4 pasos guiados.
* *Rendimiento:* El tiempo de respuesta del sistema para confirmar y guardar la inscripción no debe superar los 2 segundos.
* *Integridad de datos:* El sistema debe garantizar que dos alumnos no puedan ocupar el último cupo disponible al mismo tiempo (control de concurrencia básico).
* *Disponibilidad:* El módulo debe estar disponible de forma continua durante los periodos oficiales de inscripción establecidos por la coordinación.
* *Compatibilidad:* La interfaz debe ser accesible y funcional desde cualquier navegador web moderno (Chrome, Firefox, Edge).

  
# 5.2 Diagramas de estado

## 5.2.1 Diagrama de estado: Seleccionar materias

Este diagrama muestra el ciclo de vida de una solicitud de inscripción cuando el alumno selecciona materias.

**Código PlantUML:**

```plantuml
@startuml
!pragma layout smetana
title Estados de Seleccionar Materias

skinparam shadowing false
skinparam defaultFontName Arial
skinparam defaultFontSize 13
skinparam roundCorner 12
skinparam ArrowColor #444444
skinparam stateBackgroundColor #EAF2FB
skinparam stateBorderColor #2F5D8A
skinparam noteBackgroundColor #FFF7E6

state "Consultando oferta" as Consultando
state "Validando materia" as Validando
state "Materia aceptada" as Aceptada
state "Materia rechazada" as Rechazada
state "Selección completa" as Completa

[*] --> Consultando : el Alumno abre\nla oferta académica

Consultando --> Validando : el Alumno elige\nuna materia

Validando --> Aceptada : [hay cupo y no hay traslape]
Validando --> Rechazada : [sin cupo o con traslape]

Rechazada --> Consultando : el Alumno elige\notra materia
Aceptada --> Consultando : el Alumno agrega\notra materia
Aceptada --> Completa : el Alumno termina\nsu selección

Completa --> [*]

note right of Consultando
  El alumno revisa las materias
  disponibles del periodo.
end note

note right of Validando
  El sistema revisa cupo
  y traslape de horario.
end note

note right of Completa
  La selección queda lista
  para confirmar la inscripción.
end note
@enduml
```
**Diagrama:**

![Diagrama de estado - Seleccionar materias](resources/imgs/m2_inscripciones_estados_seleccionar_materias.png)

---

## 5.2.2 Diagrama de estado: Validar traslape de horario

Este diagrama muestra los estados por los que pasa la validación de horario cuando el alumno intenta inscribir una materia.

**Código PlantUML:**

```plantuml
@startuml
!pragma layout smetana
title Estados de Validación de Traslape de Horario

skinparam shadowing false
skinparam defaultFontName Arial
skinparam defaultFontSize 13
skinparam roundCorner 12
skinparam ArrowColor #444444
skinparam stateBackgroundColor #EAF2FB
skinparam stateBorderColor #2F5D8A
skinparam noteBackgroundColor #FFF7E6

state "Solicitada" as Solicitada
state "Comparando horarios" as Comparando
state "Sin traslape" as SinTraslape
state "Con traslape" as ConTraslape
state "Aprobada" as Aprobada
state "Alumno notificado" as Notificado

[*] --> Solicitada : el Alumno selecciona\nuna materia

Solicitada --> Comparando : el Sistema recibe\nlas materias seleccionadas

Comparando --> SinTraslape : [los horarios no coinciden]
Comparando --> ConTraslape : [los horarios coinciden]

SinTraslape --> Aprobada : se registra\nla validación correcta
ConTraslape --> Notificado : se informa qué\nmaterias chocan

Aprobada --> [*]
Notificado --> [*]

note right of Comparando
  Se comparan días y horas
  de las materias ya elegidas.
end note

note right of Notificado
  La materia no se agrega
  a la selección del alumno.
end note
@enduml
```

**Diagrama:**

![Diagrama de estado - Validar traslape de horario](resources/imgs/m2_inscripciones_estados_validar_traslape.png)

---

