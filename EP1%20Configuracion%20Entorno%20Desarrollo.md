# ÉPICA 1: CONFIGURACIÓN DEL ENTORNO DE DESARROLLO

## Resumen

| Campo | Valor |
|---|---|
| ID | EP1 |
| Nombre | Configuración del entorno de desarrollo |
| Objetivo | Establecer un entorno de desarrollo funcional, coherente y compartido para todos los miembros del equipo, que permita iniciar el desarrollo del sistema de venta de eventos musicales. |
| Criterio de aceptación de la épica | Todos los desarrolladores deben tener el entorno correctamente configurado, con acceso a la base de datos, estructura de proyecto definida y herramientas clave operativas. |

## Historias de usuario

### US1.1: Configuración del entorno de desarrollo

**Como** desarrollador
**Quiero** tener configurado el entorno de desarrollo con Maven, Spring MVC y Hibernate
**Para** poder comenzar a desarrollar funcionalidades de forma estructurada y reutilizable.

**Criterios de aceptación:**
- El proyecto debe compilar correctamente con Maven.
- Spring MVC debe estar correctamente integrado.
- Hibernate debe estar configurado para conectarse a la base de datos.

### US1.2: Definición de estructura del proyecto

**Como** desarrollador
**Quiero** tener una estructura de carpetas y paquetes definida
**Para** organizar el código de forma coherente y facilitar el trabajo en equipo.

**Criterios de aceptación:**
- La estructura debe seguir el patrón MVC.
- Deben estar definidos los nombres de los paquetes y clases principales.
- Documentación breve explicando la estructura.

### US1.3: Configuración de conexión a base de datos

**Como** desarrollador
**Quiero** configurar la conexión a la base de datos MySQL
**Para** poder persistir y consultar datos desde la aplicación.

**Criterios de aceptación:**
- La conexión debe estar definida en el fichero de configuración.
- Se debe poder ejecutar una consulta de prueba desde Hibernate.
- La base de datos debe estar accesible desde todos los entornos de desarrollo.

## Dependencias

- Acceso a herramientas: Eclipse, MySQL, GitHub, Sonar.
- Coordinación con el equipo de infraestructura si se requiere una base de datos compartida.
