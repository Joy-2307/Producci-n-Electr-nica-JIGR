# Guía de Inicio Rápido: Primeros pasos con KiCad

Bienvenido a esta guía básica sobre el uso de **KiCad** para el diseño de circuitos impresos (PCB). Aquí encontrarás los conceptos fundamentales y el flujo de trabajo esencial para pasar de un diagrama esquemático hasta el diseño físico de tu tarjeta, incluyendo la incorporación de librerías externas como la de Fab Lab (`fablib`).

---

## 1. Instalación y comprobación de KiCad
Para comenzar, nos dirigimos al sitio oficial de KiCad para descargar e instalar la versión más reciente compatible con tu sistema operativo.

> 🔗 [Sitio oficial de descarga de KiCad](https://www.kicad.org/download/)

---

## 2. Instalación y configuración de la librería Fab Lab (`fablib`)
Para trabajar con los componentes estándar utilizados en entornos de fabricación digital y laboratorios Fab Lab, es necesario integrar la librería `fablib` en KiCad.

### Pasos para instalar y configurar la librería:
1. Abre KiCad y dirígete al **Administrador de complementos y contenidos**.
2. Desde la pestaña de **Bibliotecas**, busca en la barra de búsqueda `FABLIB`.
3. Una vez encontrada, descárgala y espera a que se complete la instalación.
4. Guarda los cambios para que los componentes queden disponibles en tus proyectos.
5. Finalmente, cierra y vuelve a abrir el programa para asegurar una correcta integración.

![Administrador de bibliotecas de símbolos con la librería fablib añadida](img/fablib_instalacion.png)

---

## 3. El Editor de Esquemas (Schematic Editor)
El editor de esquemas es el lugar donde defines la lógica de tu circuito electrónico mediante símbolos y conexiones eléctricas, sin preocuparte todavía por la forma física de la placa.

### Inserción de componentes
Para añadir un componente al lienzo de trabajo, utiliza la herramienta de inserción o presiona la tecla `A`. Se abrirá una ventana de búsqueda donde podrás buscar componentes genéricos o de la librería `fablib` (como microcontroladores, resistencias, pines, etc.). Haz clic sobre el componente y colócalo en el espacio de trabajo.

![Diálogo de selección de componentes al presionar la tecla A](img/esquematico_agregar_componente.png)

### Uso de etiquetas (Labels) y conexiones
Para conectar componentes distantes sin saturar el diagrama con líneas largas, se utilizan las **etiquetas (Labels)**. Al asignar el mismo nombre de etiqueta a dos nodos diferentes, KiCad entenderá que están conectados eléctricamente.
* Para agregar una etiqueta, presiona la tecla `L` y escribe el nombre deseado.
* Utiliza la herramienta de **cable (`W`)** para realizar conexiones directas entre pines cercanos.

![Esquema con cables y etiquetas de red aplicadas](img/esquematico_etiquetas.png)

### Herramientas de apoyo visual (Rectángulos y Texto)
Para organizar mejor tu diagrama o documentar secciones importantes, puedes utilizar la herramienta de **Rectángulo** y **Gráfico de Texto**. Estas herramientas se encuentran en la barra lateral derecha y sirven exclusivamente con fines estéticos y de documentación visual, sin alterar las conexiones eléctricas.

![Esquema con cuadros organizadores y texto descriptivo](img/esquematico_apoyo_visual.png)

### Detección de errores (ERC - Electrical Rules Check)
Antes de pasar al diseño de la placa, es fundamental comprobar que el circuito no tenga errores lógicos (como pines de alimentación sin conectar o salidas cruzadas). 
* Haz clic en el icono del **chequeo de reglas eléctricas (ERC)** en la barra superior (símbolo de un insecto con una marca de verificación).
* Ejecuta la prueba y revisa la lista de advertencias o errores para corregirlos en el esquemático.

![Ventana de ejecución del ERC mostrando cero errores](img/esquematico_erc.png)

---

## 4. El Editor de Placas (PCB Editor)
Una vez que el esquema está completo y verificado, se procede al diseño físico de la tarjeta en el **PCB Editor**.

### Sincronización: Actualizar placa desde el esquema
Para transferir los componentes y conexiones lógicas del esquemático al editor de placas, haz clic en el botón **"Actualizar PCB desde el esquema"** (o presiona `F8`). 
* Es muy importante verificar que no existan errores o conflictos; esto indica que todos los componentes utilizados cuentan con su respectivo símbolo y huella.
* Este paso colocará los componentes agrupados, listos para ser posicionados en el área de trabajo. En esta etapa, procura evitar cruzar líneas guía innecesarias, ya que estas marcan las rutas de conexión.

![Botón y ventana de actualización de la PCB](img/pcb_actualizar.png)

### Capas principales (Layers)
En el editor de placas trabajas con diferentes capas superpuestas. Las más destacadas son:
* **F.Cu (Front Copper):** Capa de cobre frontal (pistas superiores).
* **Edge.Cuts:** Capa de recortes, donde se dibuja el contorno o la silueta física de la tarjeta.

Puedes alternar entre capas utilizando el panel derecho de selección o mediante atajos rápidos.

![Panel de gestión de capas en el lado derecho](img/pcb_capas.png)

### Personalización predeterminada del ancho de pistas
Puedes configurar previamente los grosores para el trazado de pistas. Como recomendación general, se sugieren **0.4 mm** para las pistas de ruteo y **0.8 mm** para los bordes de corte. 
* Dirígete a la parte superior izquierda, debajo de la barra de tareas, y en el menú desplegable configura los nuevos valores predeterminados.

![Ventana de personalización de ancho de pistas](img/pcb_ancho_pistas.png)

### Rutear pistas (Routing)
El ruteo consiste en trazar las conexiones físicas de cobre entre los pines de los componentes. 
* Selecciona la herramienta **Ruta de pistas** (o presiona la tecla `X`).
* Haz clic en el pin de origen y guía la pista hasta el destino respetando las reglas de diseño y el ancho adecuado. 
* **Recomendaciones:** Evita dejar pistas con ángulos rectos (90°) y trabaja siempre sobre la capa `F.Cu`, ya que ahí quedarán grabadas las pistas sobre el cobre.

![Pistas ruteadas entre diferentes componentes](img/pcb_ruteo.png)

> **¿Qué hacer si no se puede completar una conexión?** Puedes implementar un puente regresando al esquemático para añadir una resistencia con valor `0 ohms`, la cuál servirá como puente físico para pasar por encima de otras pistas. Actualiza la placa tras añadirla para importarla al diseño físico.

![Puente con una resistencia de 0 ohms sobre pistas ruteadas](img/pcb_puente_resistencia.png)

### Dibujar el contorno y polígonos (Filled Zones)
1. Selecciona la capa **Edge.Cuts** y utiliza la herramienta de polígono o rectángulo para trazar el contorno de tu placa.
2. Para crear planos de tierra o alimentación, utiliza la herramienta **Añadir zona llena** (`Ctrl + Shift + Z`). Selecciona la capa correspondiente (por ejemplo, `GND` en `B.Cu` o `F.Cu`) y dibuja el perímetro alrededor de tus componentes para rellenar los espacios vacíos de cobre.

![Contorno de la placa en Edge.Cuts y zona de relleno generada](img/pcb_contorno_zonas.png)

### Adición de texto en la placa
Puedes añadir texto identificativo (nombre, fecha, versión o etiquetas de pistas como `GND` o `V+`) directamente sobre la placa utilizando la herramienta de **Texto** (`T`). Colócalo en capas como `F.Cu` o en una capa de usuario (`User.Drawings`) para que se grave o imprima correctamente en el circuito final.

![Texto en la capa de serigrafía o diseño de la placa](img/pcb_texto.png)

### Perforación de la placa
Cuando los componentes requieran perforaciones adicionales:
1. Emplea una capa de usuario libre (por ejemplo, una capa `User` que no estés utilizando).
2. Dibuja un círculo con la herramienta correspondiente en el sitio exacto y asegúrate de asignarle un relleno sólido.
3. Para ajustar su posición exacta, selecciónalo, presiona la tecla `E` y modifica los valores de las coordenadas `X` e `Y`.
4. Si necesitas múltiples perforaciones idénticas, selecciona el círculo y presiona la combinación `Ctrl + T` para generar una matriz, configurando el origen, la orientación y el número de copias necesarias.

![Ventana para generar matriz y círculo generado](img/pcb_perforaciones_matriz.png)

### Detector de errores (DRC - Design Rules Check)
El paso final antes de exportar para fresar o fabricar la tarjeta es verificar que el diseño cumpla con los parámetros físicos (distancias mínimas, anchos y ausencia de cortos circuitos).
* Abre el **Verificador de Reglas de Diseño (DRC)** desde la barra superior.
* Ejecuta la comprobación y asegúrate de solucionar cualquier advertencia o error reportado.

![Ventana del DRC indicando que la placa está lista y sin errores](img/pcb_drc.png)

### Exportación de archivos
Una vez comprobado que el diseño está libre de errores de geometría o conexiones:
1. Dirígete al menú **Archivo > Salidas de fabricación > Gerbers** (o selecciona trazados vectoriales).
2. Selecciona el formato de salida (por ejemplo, **SVG** para procesos de corte y grabado digital).
3. Marca únicamente las capas donde añadiste pistas, etiquetas, perforaciones y contornos de corte.
4. Asegúrate de marcar la opción de ajustar la página a la placa y procede a trazar. Los archivos se guardarán directamente en la carpeta de tu proyecto listos para manufactura.
