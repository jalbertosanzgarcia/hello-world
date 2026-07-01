# EP4: GESTIÓN DE GRUPOS MUSICALES

## Resumen

| Campo | Valor |
|---|---|
| ID | EP4 |
| Nombre | Gestión de grupos musicales |
| Objetivo | Implementar las funcionalidades necesarias para la gestión de grupos musicales, incluyendo su creación, edición, visualización, búsqueda, favoritos y galería de imágenes. Se contemplará la gestión por parte del administrador y la visualización por parte de los usuarios. |
| Criterio de aceptación de la épica | El sistema debe permitir al administrador gestionar grupos musicales (CRUD), incluyendo imágenes y galerías, y a los usuarios visualizar, buscar y marcar como favoritos los grupos. Las imágenes deben almacenarse en base de datos. **No indicar a los alumnos que incluyan un control de tamaño de las imágenes. Lo deseable es que no lo hagan y que este problema de rendimiento salga en el Imprevisto IMP9.** |

## Historias de usuario

### US4.1: Diseño del modelo ER + Script MySQL

**Como** desarrollador
**Quiero** diseñar el modelo entidad-relación y generar el script SQL correspondiente
**Para** poder crear la base de datos necesaria para la gestión de grupos musicales.

**Esta tarea es individual. Al finalizar, el diseño será evaluado por todo el equipo y consensuado para continuar con el trabajo.**
**Indicar que la tabla maestra de géneros musicales y roles de componentes musicales se implementarán en la épica del panel de administración.**

**Criterios de aceptación:**
- Las imágenes (principal y galería) deben almacenarse en la base de datos.
- Se debe actualizar el modelo de usuarios para incluir el campo `rol` (usuario, administrador).
- De cada componente del grupo, se debe guardar información como Nombre, Apellidos, Fecha y lugar de nacimiento, y rol dentro del grupo.
- El script debe poder ejecutarse sin errores en MySQL.

**Propuesta de campos:**
- Tabla `usuarios`:
  - id_usuario (PK)
  - nombre, apellidos
  - dni, email, teléfono
  - password (encriptada)
  - direccion_envio_id, direccion_facturacion_id (FK)
  - fecha_alta, fecha_baja
  - tipo_usuario (normal, premium, VIP)
  - rol (usuario, administrador)
  - bloqueado (booleano)
- Tabla `grupos`:
  - id_grupo (PK)
  - nombre
  - genero_musical_id (FK)
  - biografia (TEXT)
  - componentes (TEXT)
  - discografia (TEXT)
  - imagen_principal (BLOB)
  - activo (booleano)
- Tabla `imagenes_grupo`:
  - id_imagen (PK)
  - id_grupo (FK)
  - imagen (BLOB)
  - descripcion (opcional)
- Tabla `favoritos_grupo`:
  - id_usuario (FK)
  - id_grupo (FK)
  - fecha_marcado
- Tabla `roles_componentes`:
  - id_rol (PK)
  - nombre_rol
- Tabla `generos_musicaes`:
  - id_genero (PK)
  - nombre_genero
- Tabla `componentes_grupo`:
  - id_componente (PK)
  - id_grupo (FK)
  - nombre
  - apellidos
  - fecha_nacimiento (DATE)
  - lugar_nacimiento (VARCHAR)
  - informacion_adicional (TEXT)
  - id_rol_componente (FK → roles_componentes.id_rol)

### US4.2: CRUD de grupos musicales

**Como** administrador
**Quiero** poder crear, editar, eliminar o desactivar grupos musicales
**Para** mantener actualizada la información de los grupos en el sistema.

**Criterios de aceptación:**
- Solo el administrador puede acceder a la funcionalidad de creación, modificación y borrado.
- Se debe permitir adjuntar una imagen principal y varias imágenes de galería.
- Si un grupo tiene entradas vendidas, no se puede eliminar.
- Un grupo se podrá desactivar.
- Las imágenes deben almacenarse en la base de datos.
- Se debe permitir buscar grupos por nombre o género musical.

### US4.3: Listado, búsqueda y filtrado de grupos

**Como** usuario
**Quiero** poder ver un listado de grupos musicales y filtrarlos por criterios
**Para** encontrar fácilmente los grupos que me interesan.

**Criterios de aceptación:**
- Al entrar en la opción de Grupos musicales, se mostrarán los últimos 5 grupos musicales dados de alta.
- El listado debe permitir búsqueda por nombre y filtrado por género musical y, si es administrador, por activo. También permitirá mostrar sólo los favoritos.
- Cada resultado de la búsqueda mostrará la imagen principal en miniatura, el nombre del grupo y, si es administrador, si está activo o no. La lista estará paginada con 10 resultados por página.
- Al pinchar sobre el nombre del grupo, se accederá a la ficha.

### US4.4: Ficha de grupo

**Como** usuario
**Quiero** poder ver la ficha detallada de un grupo musical
**Para** conocer su biografía, componentes, discografía e imágenes.

**Criterios de aceptación:**
- Al pinchar en un elemento de la lista de resultados de grupos musicales, se accederá a la ficha del grupo.
- La ficha debe incluir la imagen principal, galería, biografía, genero musical, componentes y discografía.
- Las imágenes están almacenadas en la bbdd, por lo que deben cargarse desde ahí.
- Debe mostrarse un botón para marcar como favorito. Esta opción
- Si el usuario es administrador, habrá un botón para actualizar los datos (se accederá a un formulario donde se podrá modificar toda la información) y otro para eliminar el grupo.

### US4.5: Gestión de favoritos

**Como** usuario autenticado
**Quiero** poder marcar grupos como favoritos
**Para** recibir notificaciones o avisos sobre novedades relacionadas.

**Criterios de aceptación:**
- Desde la ficha de un grupo, un usuario Normal puede marcarlo/desmarcarlo como favorito.
- En la página principal, autenticado, si hay algún grupo favorito del usuario con noticias o comentarios en las ultimas 24 horas, se mostrará una caja con esta información.

### US4.6: Documentación técnica

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
- Debe aportarse un documento de pruebas de regresión con la siguiente información:
Este documento indicará las pruebas de regresión que servirán para verificar la corrección del funcionamiento cuando vayamos a PRO.
Se deben marcar un subconjunto de ellas para ejecutarse tras el despliegue.
Se utilizará la plantilla **Pruebas Regresión - Historia XX.xlsx**.
Este documento debe subirse a Confluence.

### US4.7: Manual de usuario

**Como** desarrollador
**Quiero** documentar el uso de las funcionalidades implementadas
**Para** que los usuarios finales puedan entender cómo utilizar el sistema.

**Criterios de aceptación:**
- El manual debe incluir capturas de pantalla y explicaciones claras.
- Debe cubrir todas las funcionalidades implementadas en esta épica.

## Dependencias

- Finalización de la Épica 1 (entorno y estructura).
- Conexión a base de datos funcional.
- Implementación del sistema de autenticación y roles (EP3).
- Implementación de la página principal (EP2).
