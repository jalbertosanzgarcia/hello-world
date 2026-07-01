# EP2: DISEÑO DE LA PÁGINA PRINCIPAL (SIN AUTENTICACIÓN)

## Resumen

| Campo | Valor |
|---|---|
| ID | EP2 |
| Nombre | Diseño de la página principal (modo no autenticado) |
| Objetivo | Diseñar e implementar una página principal básica accesible sin autenticación, que sirva como punto de entrada al sistema y permita acceder a las funcionalidades iniciales como registro, login (futuro), y visualización de eventos y noticias. |
| Criterio de aceptación de la épica | La página principal debe estar accesible públicamente, mostrar enlaces básicos y contenido dinámico inicial (eventos y noticias), y estar preparada para evolucionar cuando se implemente la autenticación. |

## Historias de usuario

### US2.1: Página principal para usuarios no autenticados

**Como** visitante de la plataforma
**Quiero** acceder a una página principal con enlaces básicos y contenido informativo
**Para** poder orientarme y comenzar a interactuar con el sistema.

**Criterios de aceptación:**
- La página debe incluir:
- Enlaces visibles a: “Registrarse” y “Login” (aunque no estén implementados aún).
- Un área para mostrar los 5 próximos eventos (contenido estático o simulado si no está disponible aún).
- Un área para mostrar las 5 últimas noticias (contenido estático o simulado si no está disponible aún).
- Diseño sencillo y funcional, implementado con JSP.
- Estructura HTML clara y reutilizable para futuras mejoras.

## Dependencias

- Finalización de la Épica 1 (entorno y estructura).
- Datos de prueba para eventos y noticias (pueden ser simulados).
- No requiere autenticación ni gestión de sesiones en esta fase.
