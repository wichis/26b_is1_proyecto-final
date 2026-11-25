# UC1. Registrar profesor

**Actor:** Administrador escolar. **Requerimientos relacionados:** RF-01, RF-02, RF-08.

Permite al administrador escolar dar de alta a un profesor, validando que los datos estén completos y que no exista un registro duplicado.

## Diagrama de secuencia

[Fuente UML](../resources/uml/m3_uc1_secuencia.uml)

![Diagrama de secuencia: Registrar profesor](../resources/imgs/m3_uc1_secuencia.png)

El administrador abre el formulario en el Módulo Profesores. Desde ahí puede cancelar el registro, en cuyo caso se descartan los datos capturados y se regresa a la pantalla anterior sin llamar al controlador ni a la base de datos. Si intenta recargar la página con datos sin guardar, el módulo le advierte y le permite quedarse; solo si confirma se descartan los datos y se muestra el formulario vacío. En ningún caso se guarda un registro incompleto.

Si captura los datos y presiona «Guardar», el módulo envía la información al controlador, que pide al servicio validarla. Si los datos son inválidos o incompletos, se muestra un error para corregirlos. Si son válidos, el servicio busca en la base de datos si el profesor ya existe (por correo o número de empleado): en ese caso informa el duplicado; si es nuevo, lo guarda y se muestra la confirmación. Si después de guardar se recarga la página y se reenvía el formulario, la verificación de duplicados evita registrar dos veces al mismo profesor.

| Participante | Tipo | Responsabilidad lógica |
|---|---|---|
| Administrador escolar | Actor | Inicia la operación y captura los datos. |
| Módulo Profesores | Interfaz | Muestra formularios y mensajes, y gestiona la cancelación y la advertencia de recarga. |
| ProfesorController | Control | Recibe las solicitudes y las dirige al servicio. |
| ProfesorService | Servicio | Valida datos y detecta duplicados. |
| Base de datos | Registro | Guarda y devuelve la información de profesores. |

## Diagrama de actividades

[Fuente UML](../resources/uml/m3_uc1_actividades.uml)

![Diagrama de actividades: Registrar profesor](../resources/imgs/m3_uc1_actividades.png)

El flujo se divide entre el administrador escolar (selecciona la opción, captura y guarda) y el sistema (valida, verifica que no exista, guarda y confirma). Tiene dos decisiones: si los datos son válidos y si el profesor ya existe.

## Diagrama de estados

[Fuente UML](../resources/uml/m3_uc1_estados.uml)

![Diagrama de estados: Registro de profesor](../resources/imgs/m3_uc1_estados.png)

El registro inicia en el estado compuesto *En proceso*, que agrupa *Borrador* y *En validación*. Dentro de él, al guardar se pasa de *Borrador* a *En validación*; si los datos son inválidos o hay duplicado se regresa a *Borrador*. Si los datos son válidos, el registro pasa a *Registrado*. Desde *En proceso*, es decir, tanto en *Borrador* como en *En validación*, el administrador puede cancelar y pasar a *Cancelado*, siempre antes de que los datos se guarden en la base de datos. *Registrado* y *Cancelado* llevan al estado final.

| Estado | Al entrar | Durante | Al salir |
|---|---|---|---|
| En proceso (compuesto) | Abrir formulario de registro vacío | Mantener disponibles los datos capturados | Cerrar formulario |
| Borrador | Mostrar formulario con los datos capturados | Capturar datos del profesor | — |
| En validación | Recibir datos capturados | Validar campos y verificar duplicado | Detener validación en curso |
| Registrado | Guardar profesor en la BD | Mostrar confirmación | — |
| Cancelado | Descartar datos capturados | — | — |

## Condiciones, resultados y alternativas

- **Resultado normal:** el profesor queda registrado y se muestra la confirmación.
- **Alternativa 1:** datos inválidos o incompletos; se muestran los campos a corregir.
- **Alternativa 2:** profesor duplicado; se informa que ya está registrado.
- **Alternativa 3:** el administrador cancela, ya sea desde el formulario o durante la validación, y se descartan los datos capturados sin guardar nada en la base de datos.
- **Alternativa 4:** el administrador intenta recargar la página con datos sin guardar; el módulo le advierte y, solo si confirma, se descartan los datos. Si decide quedarse, conserva el formulario tal como estaba.