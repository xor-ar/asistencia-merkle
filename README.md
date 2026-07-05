# asistencia-merkle
Validador criptográfico de asistencia mediante árboles de Merkle y pruebas de inclusión (.js). Verifica CUITs vía URL con absoluta privacidad.

# descripción

Este proyecto consiste en una plataforma descentralizada de auditoría y control de asistencia basada en estructuras criptográficas de árboles de Merkle, diseñada específicamente para entornos donde la confidencialidad de los datos personales y operativos —como las Claves Únicas de Identificación Tributaria (CUIT)— constituye un requisito crítico e ineludible en el flujo de trabajo forense o corporativo. 

Arquitectónicamente, la solución rompe con el paradigma convencional de almacenamiento centralizado de registros en bases de datos legibles en texto plano, implementando en su lugar un mecanismo avanzado de pruebas de inclusión criptográfica inspirado en los principios de privacidad de conocimiento cero (Zero-Knowledge). 

Durante la fase de generación del evento, el sistema recolecta las entradas confidenciales junto con los metadatos contextuales de la jornada (tales como la descripción jerárquica y la fecha cronológica) y los procesa de forma estrictamente local en la memoria del navegador del operador, utilizando el algoritmo de hash unidireccional y determinista SHA-256 de la librería CryptoJS. 

Cada registro individual se transforma de este modo en una hoja criptográfica, y el sistema procede a computar los pares combinados aplicando una ordenación sistemática de los nodos hermanos (sortPairs: true) para mitigar de raíz cualquier vulnerabilidad asociada a ataques de ordenamiento o colisiones en estructuras de datos ramificadas. 

El proceso continúa de manera iterativa y ascendente hasta consolidar una raíz de Merkle única (Merkle Root), la cual actúa como una firma digital inmutable, compacta y matemática de la totalidad de la nómina. 

El núcleo disruptivo de esta arquitectura radica en su estrategia de exportación y anonimización absoluta: en lugar de volcar los vectores de datos originales en archivos JSON desprotegidos, la aplicación genera un mapa relacional indexado donde las claves del objeto corresponden exclusivamente a los hashes resultantes y los valores contienen los arreglos de hashes complementarios requeridos para trazar la ruta de validación hacia la raíz. 

Al empaquetar este mapa en un script nativo ejecutable con extensión .js, se garantiza la destrucción inmediata de la información privada en claro al finalizar la sesión del operador, persistiendo únicamente evidencias abstractas que imposibilitan la ingeniería inversa, asegurando el cumplimiento de las normativas de protección de datos más rigurosas.

Desde una perspectiva puramente operativa, de automatización y despliegue técnico, la herramienta destaca por su versatilidad al ofrecer un flujo de trabajo dual que integra tanto una interfaz de usuario interactiva y estilizada mediante Tailwind CSS como un canal de ejecución automatizado y sin fricciones basado en la extracción dinámica de parámetros a través de la URI del navegador. 

El componente de verificación asíncrona faculta a los auditores o inspectores de seguridad a constatar la presencia de un individuo específico en un evento determinado sin necesidad de interactuar con un servidor central o una API externa, eliminando así vectores de ataque de intercepción de tráfico de red y puntos únicos de fallo. 

Cuando el sistema recibe por parámetro GET la ruta de un script de firmas criptográficas (?file=evento.js) y un elemento de búsqueda (&cuit=20-12345678-9), el cargador asincrónico del cliente inyecta dinámicamente un nodo de script en la cabecera del documento (document.head.appendChild), instanciando de forma instantánea el objeto de datos globales dentro de la ventana de ejecución (window.merkleEventData). 

Acto seguido, el motor criptográfico calcula el hash SHA-256 del CUIT provisto en la URL y realiza una búsqueda directa por clave en el mapa de evidencias importado; si el hash existe, se extrae la ruta Merkle correspondiente y se ejecuta el método estático de validación matemática computando el hash objetivo junto a sus nodos hermanos contra la raíz inmutable declarada en el encabezado del archivo. 

El resultado se despliega visualmente en milisegundos mediante un sistema de alertas cromáticas de alta legibilidad que notifica estados de presencia confirmada, ausencia ratificada o fallos críticos de integridad si el archivo hubiese sido adulterado maliciosamente en su tránsito, ofreciendo un artefacto de auditoría forense altamente eficiente, portable, que no requiere de infraestructura backend dedicada, bases de datos relacionales ni costosas configuraciones de servidores para certificar la autenticidad del proceso.
