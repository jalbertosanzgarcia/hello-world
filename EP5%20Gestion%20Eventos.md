# EP5: GESTIÓN DE EVENTOS MUSICALES

## Resumen

| Campo | Valor |
|---|---|
| ID | EP5 |
| Nombre | Gestión de eventos musicales |
| Objetivo | Implementar la gestión completa de eventos musicales desde la propia web, permitiendo a los administradores autenticados crear, editar, desactivar y visualizar eventos, así como definir tipos de asiento, stock y precios. Los usuarios podrán consultar los eventos, filtrarlos y acceder a su ficha detallada. |
| Criterio de aceptación de la épica | El sistema debe permitir a los administradores gestionar eventos desde la interfaz web, y a los usuarios visualizar y consultar eventos activos. Cada evento tendrá una imagen principal, tipos de asiento configurables y entradas generadas automáticamente. **No indicar a los alumnos que incluyan un control de tamaño de las imágenes. Lo deseable es que no lo hagan y que este problema de rendimiento salga en el Imprevisto IMP9.** |

## Historias de usuario

### US5.1: Diseño del modelo ER + Script MySQL

**Como** desarrollador
**Quiero** diseñar el modelo entidad-relación y generar el script SQL correspondiente
**Para** poder crear la base de datos necesaria para la gestión de eventos musicales.

**Esta tarea es individual. Al finalizar, el diseño será evaluado por todo el equipo y consensuado para continuar con el trabajo.**
**Indicar que las tablas maestras de localidades y tipo_asiento se implementarán en la épica del panel de administración.**

**Criterios de aceptación:**
- Cada evento tendrá una imagen principal (almacenada como BLOB).
- Cada tipo de asiento tendrá precio, número de filas y asientos por fila.
- Las entradas se generarán automáticamente a partir de los tipos de asiento.
- Se guardará el estado de la entrada:
- disponible: se puede vender o reservar
- reservada_carrito: está activa dentro de algún carrito de la compra
- reservada_temporal: está reservada temporalmente
- vendida: está vendida
- Se deberá guardar la fecha en la que se guarda en el carrito y la fecha en la que se reserva temporalmente
- El script debe poder ejecutarse sin errores en MySQL.

**Propuesta de tablas:**
- Tabla `eventos`:
- id_evento (PK)
- id_grupo (FK)
- nombre_evento
- descripcion
- fecha_hora
- id_localidad (FK)
- imagen_principal (BLOB)
- activo (booleano)
- Tabla `tipo_asiento`:
- id_tipo_asiento(PK)
- nombre_tipo (general, VIP, grada, etc)
- Tabla `tipos_asiento_evento`:
- id_tipo_asiento_evento (PK)
- id_evento (FK)
- id_tipo_asiento (FK)
- precio
- num_filas
- asientos_por_fila
- Tabla `entradas`:
- id_entrada (PK)
- id_evento (FK)
- id_tipo_asiento_evento (FK)
- fila, asiento (enteros)
- estado (disponible, reservada_carrito, reservada_temporal, vendida)
- fecha_reserva_carrito (nullable)
- fecha_reserva_temporal(nullable)
- id_usuario_reserva (nullable)
- fecha_compra (nullable)
- Tabla `imagenes_evento`:
- id_imagen (PK)
- id_evento (FK)
- imagen (BLOB)
- descripcion (opcional)
- Tabla `localidades`:
- id_localidad (PK)
- Nombre
- Provincia
- país

### US5.2: CRUD de eventos musicales

**Como** administrador autenticado
**Quiero** poder gestionar eventos desde la propia web
**Para** mantener actualizada la oferta de eventos musicales.

**Criterios de aceptación:**
- Solo los administradores autenticados podrán crear. Modificar o eliminar eventos.
- Se podrá definir tipos de asiento con precio, filas y asientos por fila.
- Si hay entradas vendidas, el evento no se podrá eliminar.
- Se podrá desactivar un evento.
- Se debe permitir adjuntar una imagen principal y varias imágenes de galería.
- Las imágenes deben guardarse en bbdd.
- Al crear un evento, se tienen que generar las entradas que posteriormente estarán a la venta, teniendo cada entrada el tipo de asiento, precio, fila, asiento, fecha de compra
- Al modificar un evento, se solicitará si se quiere regenerar las entradas existentes. En ese caso, se eliminarán todas las entradas y se volverán a generar. Esta operación sólo se puede hacer si no hay ninguna entrada vendida.
- Se debe poder buscar eventos por país, localidad, grupo y fecha.

### US5.3: Listado, búsqueda y filtrado de eventos

**Como** usuario
**Quiero** poder ver un listado de eventos musicales y filtrarlos por criterios
**Para** encontrar fácilmente los eventos que me interesan.

**Criterios de aceptación:**
- Al entrar en la opción de Eventos musicales, se mostrarán los últimos 5 eventos musicales dados de alta.
- El listado debe permitir búsqueda por país, localidad, grupo y fecha. Si es administrador, también se podrá buscar por eventos activos/desactivados.
- Si es usuario normal, solo se mostrarán eventos activos.
- Cada resultado de la búsqueda mostrará la imagen principal en miniatura, el nombre del evento y, si es administrador, si está activo o no. La lista estará paginada con 10 resultados por página.
- Al pinchar sobre el nombre del evento, se accederá a su ficha.

### US5.4: Ficha de evento

**Como** usuario
**Quiero** poder ver la ficha detallada de un evento musical
**Para** conocer su información, precios, imágenes y disponibilidad.

**Criterios de aceptación:**
- Al pinchar en un elemento de la lista de resultados de eventos musicales, se accederá a la ficha del evento.
- La ficha debe incluir la imagen principal, nombre del evento, descripción, fecha, lugar, grupo asociado y galería. También mostrará un apartado de precios donde se verá qué tipo de asientos existen y a qué precio, así como el stock disponible de cada tipo.
- El stock se calculará en base a las entradas disponibles o cuya reserva_carrito o reserva_temporal haya caducado.
- Las imágenes deben cargarse desde la base de datos.
- Si el usuario es administrador, habrá un botón para actualizar los datos (se accederá a un formulario donde se podrá modificar toda la información) y otro para eliminar el evento.

### US5.5: Eventos en ficha de grupo

**Como** usuario
**Quiero** ver los eventos asociados a un grupo musical desde su ficha
**Para** conocer cuándo y dónde se presentará.

**Criterios de aceptación:**
- En la ficha del grupo deben mostrarse los eventos futuros asociados.
- Cada evento debe enlazar a su ficha detallada.

### US5.6: Próximos eventos en página principal

**Como** usuario
**Quiero** ver los próximos 5 eventos en la página principal
**Para** estar al tanto de lo que viene.

**Criterios de aceptación:**
- Mostrar los 5 eventos más próximos ordenados por fecha.

### US5.7: Listado de compradores

**Como** administrador autenticado
**Quiero** poder sacar un listado de las personas que han comprado entradas para un evento
**Para** poder comunicarnos con ellas en caso de que sea necesario (por ejemplo si un evento se ha cancelado o aplazado para devolver el dinero)

**Criterios de aceptación:**
- Desde la ficha del evento se podrá generar este listado, que se mostrará por pantalla.
- En el listado deben aparecer la fecha de generación del informe, los datos del evento y el nombre, teléfono y número de entradas compradas (se mostrará también las localidades (fila-asiento)

### US5.8: Documentación técnica

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

### US5.9: Manual de usuario

**Como** desarrollador
**Quiero** documentar el uso de las funcionalidades implementadas
**Para** que los usuarios finales y administradores comprendan cómo utilizar el sistema.

**Criterios de aceptación:**
- El manual debe incluir capturas de pantalla y explicaciones claras.
- Debe cubrir tanto la experiencia del usuario como la del administrador.

## Dependencias

- Finalización de la Épica 1 (entorno y estructura).
- Conexión a base de datos funcional.
- Implementación de la gestión de grupos musicales (EP4).
- Sistema de autenticación operativo (EP3).
