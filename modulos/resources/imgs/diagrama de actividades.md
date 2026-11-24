@startuml
title Diagrama de Actividad - Iniciar sesión

start
:Ingresar usuario y contraseña;
:Validar credenciales;

if (¿Son correctas?) then (Sí)
    :Identificar rol;
    :Mostrar menú principal;
else (No)
    :Mostrar mensaje de error;
endif

stop
@enduml
---------------------------------------
@startuml
title Diagrama de Actividad - Cambiar contraseña

start
:Solicitar cambio de contraseña;
:Ingresar contraseña actual y nueva;
:Validar contraseña actual;

if (¿Es correcta?) then (Sí)
    :Guardar nueva contraseña;
    :Mostrar confirmación;
else (No)
    :Mostrar mensaje de error;
endif

stop
@enduml
--------------------------------------------
@startuml
title Diagrama de Actividad - Recuperar contraseña

start
:Ingresar correo electrónico;
:Buscar cuenta;

if (¿Cuenta encontrada?) then (Sí)
    :Solicitar nueva contraseña;
    :Ingresar nueva contraseña;
    :Guardar contraseña;
    :Mostrar confirmación;
else (No)
    :Mostrar mensaje de error;
endif

stop
@enduml
-----------------------------------------------
@startuml
title Diagrama de Actividad - Agregar usuario

start
:Ingresar datos del usuario;
:Seleccionar rol;
:Validar información;

if (¿Datos correctos?) then (Sí)
    :Verificar si existe;
    if (¿Ya existe?) then (Sí)
        :Mostrar usuario existente;
    else (No)
        :Registrar usuario;
        :Mostrar confirmación;
    endif
else (No)
    :Mostrar errores;
endif

stop
@enduml
------------------------------------------------
@startuml
title Diagrama Actividad - Cerrar sesión

start
:Seleccionar cerrar sesión;
:Finalizar sesión;
:Regresar al inicio de sesión;
stop

@enduml
