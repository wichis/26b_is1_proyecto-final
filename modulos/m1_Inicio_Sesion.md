**Módulo:** Inicio de Sesión 

**Equipo Responsable:** Equipo 1  
**Fecha:** Noviembre 2026

**Integrantes:**
- Eric Uriel Rojas Torres
- Job Natanael Flores Flores
- Alejandro Corral Zarza
- Alfonso Cid Angeles

**Módulos Asignados:**
- Módulo Alumnos
- Módulo de Inicio de Sesión

## 1. Resumen

El Módulo de Inicio de Sesión constituye la compuerta primordial de autenticación y seguridad para el ecosistema de gestión escolar. Su función central es verificar fehacientemente la identidad de los usuarios (alumnos, personal académico y administradores) a partir de sus credenciales institucionales, evaluar sus privilegios de acceso vigentes y derivarlos de manera transparente al panel correspondiente. Asimismo, supervisa la persistencia de sesión en cliente y servidor, el cierre controlado y la prevención de vulneraciones por fuerza bruta.

## 2. Objetivo y Alcance

### 2.1 Objetivo General

Proveer una arquitectura robusta, intuitiva y centralizada para la autenticación y control de accesos de la comunidad académica, salvaguardando la confidencialidad de la información y garantizando una experiencia de usuario fluida.

### 2.2 Alcance del Módulo

- **Autenticación Centralizada:** Validación de credenciales de acceso (matrícula/correo institucional y contraseña cifrada).
- **Resolución de Roles:** Detección dinámica del perfil activo (Alumno, Docente, Administrador) y enrutamiento hacia la vista autorizada.
- **Recuperación de Cuenta:** Mecanismo asistido para el restablecimiento de contraseñas mediante correo electrónico institucional.
- **Gestión de Ciclo de Vida de Sesión:** Generación, validación y expiración segura de tokens de sesión con soporte para desconexión explícita.
- **Auditoría y Protección Activa:** Bloqueo preventivo temporal frente a umbrales consecutivos de reintentos fallidos.

## 3. Requerimientos Funcionales

| Código | Requerimiento | Descripción Detallada |
|---|---|---|
| RF01 | Captura de Credenciales | El sistema debe proveer una interfaz para capturar el identificador (matrícula o correo institucional) y la contraseña del usuario. |
| RF02 | Validación y Cotejo Criptográfico | El sistema debe validar contra el repositorio de datos que las credenciales coincidan con el hash almacenado y que la cuenta esté activa. |
| RF03 | Resolución de Rol y Enrutamiento | El sistema debe identificar el rol asociado al usuario autenticado (Alumno, Docente, Administrador) y redireccionar al panel que le corresponda. |
| RF04 | Recuperación de Contraseña | El sistema debe emitir un token temporal de un solo uso con caducidad definida para el restablecimiento de contraseña vía correo. |
| RF05 | Cierre Seguro de Sesión | El sistema debe destruir la sesión activa y revocar el token en almacenamiento cliente cuando el usuario elija salir del portal. |
| RF06 | Bloqueo por Fuerza Bruta | El sistema debe suspender temporalmente el acceso por 15 minutos tras 5 intentos fallidos consecutivos desde la misma cuenta o IP. |

## 4. Actores del Sistema

- **Usuario (Genérico):** Alumno, docente o personal administrativo que interactúa con la interfaz de login para autenticarse.
- **Sistema de Autenticación / BD:** Componente backend encargado de verificar credenciales, verificar estados de cuenta y emitir tokens.
- **Servicio de Notificaciones:** Subsistema encargado del envío de correos electrónicos con enlaces temporales de recuperación.

## 5. Diagrama de Casos de Uso

A continuación se presenta el modelo conceptual de interacción entre los actores identificados y los casos de uso fundamentales del módulo de inicio de sesión:

[Nota: Diagrama UML renderizado externamente - Error al adjuntar imagen: <urlopen error [Errno -3] Temporary failure in name resolution>]

### 5.1 Código Fuente UML (PlantUML)

@startuml
left to right direction
skinparam packageStyle rectangle

actor "Usuario" as usr
actor "Sistema de Autenticación" as auth

rectangle "Módulo: Inicio de Sesión" {
  usecase "CU01: Ingresar credenciales" as UC1
  usecase "CU02: Validar credenciales" as UC2
  usecase "CU03: Recuperar contraseña" as UC3
  usecase "CU04: Cerrar sesión" as UC4
  usecase "CU05: Bloquear acceso por reintentos" as UC5
  usecase "CU06: Redireccionar según rol" as UC6
}

usr --> UC1
usr --> UC3
usr --> UC4

UC1 .> UC2 : <<include>>
UC2 ..> UC6 : <<include>>
UC2 <.. UC5 : <<extend>>
UC2 --> auth
@enduml


## 6. Glosario y Abreviaturas

| Término | Definición Contextual |
|---|---|
| Credenciales | Conjunto de datos confidenciales provistos por el usuario (identificador único y contraseña) para constatar su identidad ante el sistema. |
| Hash Criptográfico | Representación alfanumérica unidireccional no invertible obtenida mediante un algoritmo seguro (ej. BCrypt, Argon2) para proteger la contraseña almacenada. |
| Token de Sesión | Cadena digital firmada (como un JWT) que acredita el estado de autenticación del usuario en peticiones subsecuentes sin reenviar su contraseña. |
| Rol de Usuario | Categoría jerárquica de permisos asignada a una cuenta (Alumno, Docente, Administrador) que determina la accesibilidad funcional en el sistema. |
| Fuerza Bruta | Método de intrusión basado en la prueba sucesiva y automatizada de combinaciones de credenciales hasta dar con la correcta. |

## 7. Requerimientos No Funcionales

| Código | Atributo | Criterio de Calidad |
|---|---|---|
| RNF01 | Seguridad Criptográfica | Las credenciales deben viajar cifradas bajo canal TLS/HTTPS y las contraseñas deben almacenarse bajo funciones de dispersión robustas (BCrypt con factor de costo >= 10). |
| RNF02 | Eficiencia y Tiempo de Respuesta | El proceso completo de validación y respuesta de sesión no debe exceder los 2.0 segundos bajo condiciones estándar de red. |
| RNF03 | Mitigación de Ataques | Implementación de Rate Limiting en la API de autenticación y bloqueo preventivo para mitigar ataques automatizados de denegación o fuerza bruta. |
| RNF04 | Ofuscación de Respuestas de Error | La interfaz no debe revelar si un fallo corresponde a una contraseña errónea o a un usuario inexistente; el mensaje debe ser neutral ('Credenciales inválidas').
