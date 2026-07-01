# EP3: GESTIÓN DE USUARIOS

## Resumen

| Campo | Valor |
|---|---|
| ID | EP3 |
| Nombre | Gestión de usuarios |
| Objetivo | Implementar las funcionalidades necesarias para permitir el registro, autenticación, gestión de perfil y baja de usuarios, así como el control de sesiones y actividad. |
| Criterio de aceptación de la épica | El sistema debe permitir a los usuarios registrarse, iniciar y cerrar sesión, modificar sus datos, cambiar su contraseña, y darse de baja. Además, debe registrarse la actividad del usuario y aplicarse validaciones básicas en los formularios. |

## Historias de usuario

### US3.1: Diseño del modelo ER + Script MySQL

**Como** desarrollador
**Quiero** diseñar el modelo entidad-relación y generar el script SQL correspondiente
**Para** poder crear la base de datos necesaria para la gestión de usuarios.

**Esta tarea es individual. Al finalizar, el diseño será evaluado por todo el equipo y consensuado para continuar con el trabajo.**

**Criterios de aceptación:**
- El modelo debe incluir todos los campos necesarios para la gestión de usuarios, direcciones y actividad.
- El script debe poder ejecutarse sin errores en MySQL.
- Debe contemplar la relación entre usuarios y sus direcciones (envío y facturación).

**Propuesta de campos:**
- Tabla `usuarios`:
  - id_usuario (PK)
  - nombre, apellidos
  - dni, email, teléfono
  - password (encriptada)
  - direccion_envio_id, direccion_facturacion_id (FK)
  - fecha_alta, fecha_baja
  - bloqueado (booleano)
- Tabla `direcciones`:
  - id_direccion (PK)
  - calle, número, ciudad, provincia, país, código_postal
- Tabla `actividad_usuario`:
  - id_evento (PK)
  - id_usuario (FK)
  - tipo_evento, fecha_hora, ip_origen

### US3.2: Registro de usuarios

**Como** visitante de la plataforma
**Quiero** poder registrarme mediante un formulario con validaciones
**Para** poder acceder a las funcionalidades del sistema como usuario autenticado.

**Criterios de aceptación:**
- El formulario debe validar campos obligatorios, longitudes, formato de DNI, teléfono y email.
- Se debe permitir introducir dirección de envío y facturación (pueden ser la misma).
- La información debe guardarse correctamente en la base de datos.
- Tras autenticarse, se debe guardar el evento en la tabla de actividad y se debe redireccionar a la página principal en modo autenticado:
Enlace de cerrar sesión
Enlace de acceso a perfil
Enlace a Grupos. En función de si el usuario es un usuario normal o administrador, podrá hacer unas acciones u otras.
Enlace a Eventos. En función de si el usuario es un usuario normal o administrador, podrá hacer unas acciones u otras.
Enlace a Panel de control. Se realizarán operaciones de gestión que no han sido integradas en la navegación normal de la web.
Visualizando el mock de eventos y noticias que se usa en la página en modo no autenticado.

### US3.3: Login, logout y gestión de sesiones

**Como** usuario registrado
**Quiero** poder iniciar y cerrar sesión de forma segura
**Para** acceder a mi perfil y funcionalidades personalizadas.

**Criterios de aceptación:**
- El sistema debe permitir login con validación de credenciales.
- Tras 3 intentos fallidos consecutivos, la cuenta debe bloquearse temporalmente.
- Las contraseñas deben almacenarse encriptadas.
- Se debe registrar cada intento de inicio de sesión en la tabla de actividad.
- Debe existir una funcionalidad de cambio de contraseña con doble factor simulado (popup sin validación real).
- Tras autenticarse, el usuario debe ser redirigido a la página principal, donde ya no verá las opciones de 'Registrarse' y 'Login', sino las descritas anteriormente para el modo autenticado.

### US3.4: Perfil de usuario

**Como** usuario autenticado
**Quiero** poder ver y editar mis datos personales
**Para** mantener mi información actualizada y gestionar mi cuenta.

**Criterios de aceptación:**
- El usuario debe poder ver y modificar sus datos personales.
- Debe poder cambiar su contraseña con confirmación y doble factor simulado.
- Debe poder darse de baja, registrando el evento en la tabla de actividad. La baja será lógica: el usuario se marcará como bloqueado.
- Se debe mostrar un log de actividad del usuario.

### US3.5: Documentación técnica

**Como** desarrollador
**Quiero** generar la documentación técnica del análisis y diseño implementado
**Para** dejar constancia de las decisiones tomadas y facilitar el mantenimiento y evolución del sistema.

**Criterios de aceptación:
- Debe aportarse un documento de análisis con la siguiente información:
Una descripción del análisis funcional realizado para la funcionalidad desarrollada.
El diseño técnico implementado (diagrama de clases, estructura de paquetes, tecnologías utilizadas, diseño de BBDD).
Una justificación razonada de las decisiones de diseño adoptadas.
Se utilizará la plantilla **Documento Análisis - Historia XX.docx**.
Este documento debe subirse a Confluence.
- Debe aportarse un documento de pruebas de regresión con la siguiente informació:
Este documento indicará las pruebas de regresión que servirán para verificar la corrección del funcionamiento cuando vayamos a PRO.
Se deben marcar un subconjunto de ellas para ejecutarse tras el despliegue.
Se utilizará la plantilla **Pruebas Regresión - Historia XX.xlsx**.
Este documento debe subirse a Confluence.

### US3.6: Manual de usuario

**Como** desarrollador
**Quiero** documentar el uso de las funcionalidades implementadas
**Para** que los usuarios finales puedan entender cómo utilizar el sistema.

**Criterios de aceptación:**
- El manual debe incluir capturas de pantalla y explicaciones claras.
- Debe cubrir todas las funcionalidades implementadas.
- Tener en cuenta que esta documentación se irá ampliando a medida que evolucionemos el sistema.

## Posibles mejoras

- Mostrar en la página principal, autenticado, eventos destacados que se celebren en la misma localidad que el usuario. Habría que guardar información de localidad del usuario.
- También se podrían guardar los géneros musicales favoritos del usuario, y hacer recomendaciones de eventos en base a ese dato.

## Dependencias

- Finalización de la Épica 1 (entorno y estructura).
- Página principal básica operativa (EP2).
- Conexión a base de datos funcional.
- Conocimiento básico de validaciones en formularios y encriptación de contraseñas.
