# Dinaup Tecnología

Bienvenido a Dinaup Tecnología. Si estás buscando entender qué es y cómo puede revolucionar tus proyectos, estás en el lugar correcto. Esta guía te proporcionará una visión clara de sus conceptos fundamentales, facilitando la comprensión para aquellos que son nuevos en este sistema.




## Conceptos básicos

### 1. Secciones y Campos
Piensa en secciones y campos como las tablas y columnas de una base de datos. Sin embargo, en Dinaup, estas secciones y campos poseen funcionalidades avanzadas, como EDU, Bases, Secciones Incrustadas y más.
### 2. Informes y Columnas
Son herramientas para configurar consultas específicas a las secciones y campos, facilitando la extracción de la información deseada. Además esto permite crear funcionalides. 
 - Informe para usuarios
 - Definir estructura para consultas API
 - Definir estructura para consultas API cachables
 - Informes de tipo procesables
 - Informes para crear Boards
 - Informes para crear Gantts
 - Informes visualizados en modo gráficas
 - Informes incrustados en secciones.
 - Informes de paneles.
### 3. Documentos dinámicos
Herramienta para generar archivos de texto plano de forma dinámica, como HTML, JSON y XML. Además, se puede previsualizar r y exportar a formatos como PDF, EXCEL y WORD.
### 4. Scripts
Representan la lógica que se ejecuta al interactuar con un registro, es decir, las acciones que ocurren cuando un usuario realiza ciertas acciones.
###  5. Algoritmos
Estos son segmentos de lógica abstracta, diseñados para ser utilizados en múltiples contextos, ofreciendo flexibilidad y reusabilidad. Permiten abstraer la lógica.


## Combinaciones 
### 1. Scripts + Secciones = Scripts de Secciones
- **Ventana Iniciada (Nuevo Registro)**: Al agregar un nuevo registro, este evento dispara scripts que establecen valores iniciales.
- **Recálculo**: Activado cuando un campo cambia, permitiendo recalcular valores, como el total de una factura.
- **Antes de Guardar**: Una oportunidad para verificar y, si es necesario, bloquear el guardado.

### 2. Scripts + Campos = Scripts de Campos
- **Campo Cambiado**: Asocia un script para acciones automáticas cuando un campo se modifica.
- **Filtrado Desplegable**: Personaliza y filtra las opciones de un menú desplegable.
- **Agregar Relación**: Transfiere datos al nuevo registro relacionado.

### 3. Algoritmos + Campos = Campos Autocalculados
Un campo puede autocalcularse con la ayuda de un algoritmo. A diferencia de los scripts, estos campos pueden actualizarse de manera indirecta.

### 4. Algoritmos + Columnas:
Diseña una columna con un valor calculado a través de un algoritmo.

### 5. Algoritmos + Informe (filtrado)
Usa expresiones avanzadas para filtrar informes, aunque es aconsejable usar el filtrado de condiciones de informe.

### 6. Algoritmos + Documentos Dinámicos
Incorpora algoritmos en tus documentos dinámicos para enriquecerlos.

### 7. Algoritmos + Algoritmos
¡Sí, es posible! Llama a un algoritmo desde otro algoritmo.





## Campos y Secciones al detalle
### Formatos de Campos:
- Entero
- Decimal
- Texto (Estandar, Multilínea, Visor HTML, Editor HTML, Web, Contraseña, etc.)
- Sí/No
- GUID (Relación)
- Fecha (Local)
- Fecha y Hora (UTC con o sin segundos)
- Hora (con o sin segundos)

### Campos avanzados 
 - **Campos EDU (Extensión Dato Ubicación)**: Estos campos ofrecen una funcionalidad singular, permitiendo que un mismo elemento, como un producto, mantenga atributos que varían según la ubicación. Por ejemplo, mientras que un "iPhone" es un objeto consistente y reconocible independientemente de donde esté, su stock puede variar de una tienda a otra. Un campo EDU se encarga precisamente de esto, asignando valores distintos a un mismo producto, dependiendo de la ubicación específica. En otras palabras, aunque el producto sea el mismo en todas las ubicaciones, el campo EDU permite que ciertas características, como el stock, sean únicas para cada una. Los datos EDU se almacenan en secciones EDU. Dichas secciones se gestionan internamente y no son visibles ni el usuario debe preocuparse por ellas.
  
  > **Funcionamiento** Si una sección con 1.000.000 de registros tiene activo algún campo EDU. Suponiendo que tiene 50 ubicaciones, la sección EDU tendrá 50.000.000 de registros.

  > **Interacción** Puede crear informes, algoritmos sobre las secciones EDU, ya que aparece visible para seleccionar dicha sección en las opciones de crear informe, el nombre está estandarizado con el Prefijo `EDU - {Nombre de sección}` 


### Tipos de Secciones:
 - **Estándar**: Sección con una base, una derivada y sin funcionalidadesa avanzadas activadas.
 - **Multiderivada**:  Esta funcionalidad permite segmentar una sección base en múltiples secciones derivadas. Imagina una sección principal denominada Base - Productos. A través de la característica multiderivada, esta sección puede subdividirse en, por ejemplo, Base - Productos > Servicios y Base - Productos > Productos. Esta división no solo facilita la creación de informes o algoritmos específicos para cada derivada o la base en sí, sino que también brinda flexibilidad en la personalización. Cada sección derivada puede tener su propio diseño de formulario y emplear campos distintos, lo que permite una adaptación y gestión de datos más eficiente y específica. Es como tener múltiples capas de información, todas originadas desde una sección base pero con características y funciones diferenciadas.
 - **Con Lista o Lista**: Permite administrar listas dentro de un registro, por ejemplo, la lista de productos que tiene una venta, apuntes que tiene un asiento... cada sección soporta como máximo una lista, sin embargo, se puede utilizar la técnica de informes incrustados para simular el comportamiento.
 - **CDU (Control de Datos por Ubicación)**: Esta funcionalidad, activada desde la sección base, permite asociar datos específicos a una ubicación determinada. Por ejemplo, en una empresa con 50 sucursales dispersas en un territorio, cada venta y cada inventario se atribuye a una sucursal específica. Esto no solo ayuda a mantener una organización clara, sino que también facilita la gestión de permisos, permitiendo restricciones como "solo puede acceder a las nóminas de su respectiva ubicación".

### Limitaciones
- EDU y CDU no son compatibles.
- Las secciones tipo lista no pueden tener EDU.
- Máximo de 10.000 elementos en una lista.

### Notas:
> Las opciones CDU, CDF y CDE siempre están presentes internamente, garantizando eficiencia sin afectar el rendimiento.



 