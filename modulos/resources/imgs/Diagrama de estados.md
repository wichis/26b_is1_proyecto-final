@startuml
title Diagrama de Estados - Sesión de usuario

[*] --> Inactiva
Inactiva --> Autenticando : Iniciar sesión
Autenticando --> Activa : Credenciales correctas
Autenticando --> Inactiva : Credenciales incorrectas
Activa --> Cerrada : Cerrar sesión
Activa --> Expirada : Tiempo agotado
Cerrada --> [*]
Expirada --> [*]

@enduml
-------------------------------
@startuml
title Diagrama de Estados - Cuenta de usuario

[*] --> Activa : Registrar usuario
Activa --> Bloqueada : Intentos fallidos
Bloqueada --> Activa : Desbloquear cuenta
Activa --> Recuperacion : Solicitar recuperación
Recuperacion --> Activa : Cambiar contraseña
Activa --> Deshabilitada : Desactivar cuenta
Deshabilitada --> Activa : Reactivar cuenta

@enduml