@startuml
title Diagrama de Secuencia - Iniciar sesión
actor Usuario
participant Interfaz
participant Sistema
database BD

Usuario -> Interfaz: Ingresa usuario y contraseña
Interfaz -> Sistema: Enviar credenciales
Sistema -> BD: Validar usuario
BD --> Sistema: Resultado

alt Credenciales correctas
    Sistema --> Interfaz: Acceso autorizado
    Interfaz --> Usuario: Mostrar menú principal
else Credenciales incorrectas
    Sistema --> Interfaz: Acceso denegado
    Interfaz --> Usuario: Mostrar error
end
@enduml

-----------------------------------------

@startuml
title Diagrama de Secuencia - Cambiar contraseña
actor Usuario
participant Interfaz
participant Sistema
database BD

Usuario -> Interfaz: Solicita cambio
Interfaz --> Usuario: Mostrar formulario
Usuario -> Interfaz: Ingresa contraseñas
Interfaz -> Sistema: Enviar información
Sistema -> BD: Validar contraseña actual
BD --> Sistema: Resultado

alt Contraseña correcta
    Sistema -> BD: Guardar nueva contraseña
    BD --> Sistema: Confirmar cambio
    Sistema --> Interfaz: Cambio exitoso
else Contraseña incorrecta
    Sistema --> Interfaz: Mostrar error
end

Interfaz --> Usuario: Mostrar resultado
@enduml

----------------------------------------------

@startuml
title Diagrama de Secuencia - Recuperar contraseña
actor Usuario
participant Interfaz
participant Sistema
database BD

Usuario -> Interfaz: Solicita recuperación
Interfaz --> Usuario: Solicitar correo
Usuario -> Interfaz: Ingresa correo
Interfaz -> Sistema: Buscar cuenta
Sistema -> BD: Consultar usuario
BD --> Sistema: Resultado

alt Cuenta encontrada
    Sistema --> Interfaz: Permitir recuperación
    Interfaz --> Usuario: Solicitar nueva contraseña
    Usuario -> Interfaz: Ingresa nueva contraseña
    Interfaz -> Sistema: Actualizar contraseña
    Sistema -> BD: Guardar contraseña
    BD --> Sistema: Confirmación
    Sistema --> Interfaz: Recuperación exitosa
else Cuenta no encontrada
    Sistema --> Interfaz: Mostrar error
end

Interfaz --> Usuario: Mostrar resultado
@enduml
-------------------------------------------------------
@startuml
title Diagrama de Secuencia - Agregar usuario
actor "Personal Administrativo" as Admin
participant Interfaz
participant Sistema
database BD

Admin -> Interfaz: Solicita agregar usuario
Interfaz --> Admin: Mostrar formulario
Admin -> Interfaz: Ingresa datos y rol
Interfaz -> Sistema: Enviar información
Sistema -> BD: Verificar usuario

alt Usuario no existente
    Sistema -> BD: Registrar usuario
    BD --> Sistema: Registro exitoso
    Sistema --> Interfaz: Confirmar registro
else Usuario existente
    Sistema --> Interfaz: Usuario ya registrado
end

Interfaz --> Admin: Mostrar resultado
@enduml
----------------------------------------------------------
@startuml
title Diagrama de Secuencia - Cerrar sesión
actor Usuario
participant Interfaz
participant Sistema

Usuario -> Interfaz: Selecciona cerrar sesión
Interfaz -> Sistema: Solicitar cierre
Sistema -> Sistema: Finalizar sesión
Sistema --> Interfaz: Confirmar cierre
Interfaz --> Usuario: Regresar al inicio de sesión

@enduml
----------------------------------------------------------------