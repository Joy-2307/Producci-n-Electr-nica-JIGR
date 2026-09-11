Guía de Inicio Rápido: Primeros pasos con KiCad
Bienvenido a esta guía básica sobre el uso de KiCad para el diseño de circuitos impresos (PCB). Aquí encontrarás los conceptos fundamentales y el flujo de trabajo esencial para pasar de un diagrama esquemático hasta el diseño físico de tu tarjeta, incluyendo la incorporación de librerías externas como la de Fab Lab (fablib).

1. Instalación y comprobación de la última versión de Kicad, para esto nos vamos al sitio oficial de Kicad donde podemos decidir desde donde descargarlo.
[link de la página oficial de instalación de Kicad]

---

2. Instalación y configuración de la librería Fab Lab (fablib)
Para trabajar con los componentes estándar utilizados en entornos de fabricación digital y laboratorios Fab Lab, es necesario integrar la librería fablib en KiCad.

-Pasos para instalar y configurar la librería:
Abre KiCad y dirígete al administrador de complementos y contenidos, desde la pestaña de Bibliotecas buscamos en la barra de búsqueda el nombre de la librería que deseamos instalar, en este caso instalaremos la librería de (FABLIB), una vez encontrada descargamos y esperamos a que se complete la instalación, guardamos los cambios para que los componentes queden disponibles en tus proyectos, finalmente cerramos y volvemos a abrir el programa para asegurar la instalación.

[ss mostrando el Administrador de bibliotecas de símbolos con la librería fablib añadida]

---

2. El Editor de Esquemas (Schematic Editor)
El editor de esquemas es el lugar donde defines la lógica de tu circuito electrónico mediante símbolos y conexiones eléctricas, sin preocuparte todavía por la forma física de la placa.

-Inserción de componentes:
Para añadir un componente al lienzo de trabajo, utiliza la herramienta de inserción o presiona la tecla A. Se abrirá una ventana de búsqueda donde podrás buscar componentes genéricos o de la librería fablib (como microcontroladores, resistencias, pines de conexión, etc.). Haz clic sobre el componente y colócalo en el espacio de trabajo.

[ss del diálogo de selección de componentes al presionar la tecla A]

-Uso de etiquetas (Labels) y conexiones
Para conectar componentes que se encuentran distantes sin necesidad de trazar líneas largas que saturen el diagrama, se utilizan las etiquetas (Labels). Al asignar el mismo nombre de etiqueta a dos nodos diferentes, KiCad entenderá que están conectados eléctricamente.Para agregar una etiqueta, presiona la tecla L y escribe el nombre deseado.Utiliza la herramienta de cable (W) para realizar conexiones directas entre pines cercanos.

[ss mostrando un esquema con cables y etiquetas de red aplicadas]

-Herramientas de apoyo visual (Rectángulos y Texto)
Para organizar mejor tu diagrama o documentar secciones importantes, puedes utilizar la herramienta de Rectángulo y Gráfico de Texto. Estas herramientas se encuentran en la barra lateral derecha y sirven únicamente con fines estéticos y de documentación visual, sin afectar las conexiones eléctricas.

[ss del esquema con cuadros organizadores y texto descriptivo]

-Detección de errores (ERC - Electrical Rules Check)
Antes de pasar al diseño de la placa, es fundamental comprobar que el circuito no tenga errores lógicos (como pines de alimentación sin conectar o salidas cruzadas). Haz clic en el icono del chequeo de reglas eléctricas (ERC) en la barra superior (símbolo de un bicho con una marca de verificación). Ejecuta la prueba y revisa la lista de advertencias o errores para corregirlos en el esquemático.

[ss de la ventana de ejecución del ERC mostrando cero errores]

---

3. El Editor de Placas (PCB Editor)
Una vez que el esquema está completo y verificado, se procede al diseño físico de la tarjeta en el PCB Editor.

-Sincronización: Actualizar placa desde el esquema
Para transferir los componentes y conexiones lógicas del diagrama esquemático al editor de placas, debes hacer clic en el botón "Actualizar PCB desde el esquema" (o presionar F8).Aquí es muy importante asegurarnos de ver que aparezca que no existen errores o conflictos, estpo significa que todos nuestros componentes usados cuentan con huella y símbolo.  Esto colocará los componentes agrupados listos para ser posicionados dentro del área de trabajo, este paso es muy importante ya que el posicionamiento debemos de evitar cruzar líneas ya que estas lineas son nuestras pistas.

[ss del botón y ventana de actualización de la PCB]

-Capas principales (Layers)
En el editor de placas, trabajas con diferentes capas superpuestas. Las más importantes son:

F.Cu (Front Copper): Capa de cobre frontal (pistas superiores).
Edge.Cuts: Capa de recortes, donde se dibuja el contorno o la silueta física que tendrá la tarjeta.
Puedes alternar entre capas utilizando el panel derecho de selección o mediante atajos rápidos.

[ss resaltando el panel de gestión de capas en el lado derecho]

-Personalización predeterminada de ancho de pistas.
Aquí podemos establecer posibles configuraciones para nuestro trazado de pistas, recomendando 0.4mm para las pistas de ruteo y 0.8mm para los bordes de corte de nuestras placas, para ello nos dirigimos a la parte superior izquierda, debajo de nuestra barra de tareas, en el menú desplegable podemos crear nuevas configuraciones predeterminadas de nuestras pistas.

[ss de la ventana de personalización de ancho de pistas]

-Rutear pistas (Routing)
El ruteo consiste en trazar las conexiones físicas de cobre entre los pines de los componentes. Selecciona la herramienta Ruta de pistas (o presiona la tecla X). Haz clic en el pin de origen y guía la pista hasta el pin de destino respetando las reglas de diseño y el ancho adecuado para tu aplicación, aquí es importante evitar dejar pistas con ángulos de 90°.Aqui es importante trabajar siempre en la capa F.Cu, ya que en esa capa es donde quedaran grabadas nuestras piestas sobre el cobre.

En caso de no poder completar una conexión, podemos recurrir a la creación de un puente, para esto podemos regresar a nuestro esquemático, donde podemos añadir resistencias con valor 0, las cuales serviran como puentes en nuestras conexiones y poder pasar sobre pistas ya trazadas. Colocamos la resistencia con valor 0, lueego regresamos a nuestro editor de placas, donde actualizamos para que se importe este nuevo  componente.

[ss mostrando pistas ruteadas entre diferentes componentes]

[ss mostrando un puente con una resistencia 0 sobre pistas ruteadas]

-Dibujar el contorno y polígonos (Filled Zones)
Selecciona la capa Edge.Cuts y utiliza la herramienta depolígono o Rectángulo para trazar el contorno de tu placa. Para crear planos de tierra o alimentación, utiliza la herramienta Añadir zona llena (Ctrl + Shift + Z). Selecciona la capa correspondiente (por ejemplo, GND en B.Cu o F.Cu) y dibuja el perímetro alrededor de tus componentes para rellenar los espacios vacíos de cobre.

[ss mostrando el contorno de la placa en Edge.Cuts y una zona de relleno generada]

-Adición de texto en la placa
Puedes añadir texto identificativo (como tu nombre, fecha o versión del circuito o simplemente añadir etiquetas a las pistas como GND ó V+) directamente sobre la placa utilizando la herramienta de Texto (T). Asegúrate de colocarlo en las capas de serigrafía (F.Silkscreen o B.Silkscreen) para que se imprima o se grave correctamente en el circuito final.

[ss mostrando texto en la capa de serigrafía de la placa]

-Detector de errores (DRC - Design Rules Check)
El paso final antes de mandar a fabricar o fresar la tarjeta es verificar que el diseño cumpla con los parámetros físicos de fabricación (distancias mínimas entre pistas, anchos, cortos circuitos, etc.). Abre el Verificador de Reglas de Diseño (DRC) desde la barra superior. Ejecuta la comprobación y asegúrate de solucionar cualquier violación reportada antes de exportar tus archivos de fabricación (Gerber o trazos para CNC).

[ss de la ventana del DRC indicando que la placa está lista y sin errores]

-Exportación de archivos
Para poder exportar nuestros archivos es importante no tener errores de diseño, una vez comprobado esto, nos dirigimos a la sección de archivo -> salidas de fabricación -> Gerbers una vez en esta ventana seleccionamos el formato de trazado, nosotros trabajaremos con SVG, es importante seleccionar únicamente las capas donde añadimos pistas, etiquetas o perforaciones y cortes, finalmente marcamos la opción de ajustar página a la placa y trazamos, estos archivos se guardaran donde hemos creado nuestro proyecto y con ellos podremos hacer nuestra PCB. 

[ss de la ventana de salidas de fabricación]

