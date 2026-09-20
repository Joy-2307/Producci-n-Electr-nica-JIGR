# Procesamiento de SVG a RML con Mods

Este apartado constituye una continuación directa de nuestra documentación de diseño en KiCad. Una vez que hemos exportado los archivos necesarios de nuestras placas, el siguiente paso crítico en el proceso de fabricación digital con la fresadora Roland MonoFab (SRM-20) es transformar nuestros vectores en trayectorias de maquinado legibles (archivos `.rml`) utilizando la herramienta web **Mods**.

---

## 1. Verificación y Preparación previa en Inkscape

Antes de enviar cualquier diseño a la plataforma de maquinado, es fundamental asegurarnos de que los archivos vectoriales (específicamente el contorno de nuestra placa) cumplan con las condiciones geométricas adecuadas para evitar fallos físicos en el material.

### 1.1. Descarga y Sitio Oficial
Si detectas que el contorno de tu placa parece cortado o mal delimitado, se recomienda utilizar un editor de vectores. Para este propósito utilizamos **Inkscape**. Puedes acceder a su plataforma y obtener los instaladores desde su [sitio oficial de Inkscape](https://inkscape.org/){: target="_blank" }. No profundizaremos demasiado en el uso general del software, pero sí en una regla de oro para la manufactura.

### 1.2. Consideraciones Clave de Diseño Vectorial
* **Todo dentro del lienzo:** Es indispensable verificar que todos los vectores de corte y trazo se encuentren completamente dentro del área del lienzo de trabajo en Inkscape. De lo contrario, la herramienta de exportación podría omitir secciones o generar errores de geometría.
* **Manejo de tolerancias:** Es vital respetar márgenes y tolerancias adecuados en las pistas y contornos de la placa. Si los vectores están mal posicionados o demasiado justos, el cabezal de corte podría invadir zonas críticas y seccionar una pista por error.

| Vector Incorrecto (Cortado / Fuera de límites) | Vector Correcto (Alineado y dentro del lienzo) |
| :---: | :---: |
| <img src="../recursos/imgs/vector_incorrecto_ejemplo.png" alt="Ejemplo de vector cortado o mal posicionado" width="400"> | <img src="../recursos/imgs/vector_correcto_ejemplo.png" alt="Ejemplo de vector corregido dentro del lienzo" width="400"> |

---

## 2. Introducción a la Plataforma Mods

Una vez que nuestros archivos vectoriales (SVG) están limpios y correctamente acotados, pasamos a **Mods**, una herramienta web basada en nodos ampliamente utilizada en entornos Fab Lab para la manufactura digital.

### 2.1. Acceso y Selección del Programa
1. Ingresa al sitio oficial de la herramienta a través de su entorno web en [Mods Community](https://mods.cba.mit.edu/){: target="_blank" }.
2. Dirígete a la pestaña de **Programs** y dentro del buscador escribe **`srm-20mil`**.
3. Selecciona la opción correspondiente a **`mill 2d pcb`** para desplegar el diagrama de nodos diseñado específicamente para el fresado de circuitos impresos en la SRM-20.

<img src="../recursos/imgs/mods_seleccion_programa.png" alt="Búsqueda y selección del programa srm-20mil mill 2d pcb en Mods" width="800">

### 2.2. Vista General de la Interfaz de Nodos
Al cargar el programa, verás un conjunto interconectado de bloques o nodos que procesan la información de manera secuencial (desde la entrada del archivo hasta la generación del código de la máquina). A continuación, se presenta una vista general destacando con distintos colores las secciones clave en las que debemos enfocar nuestra atención durante el flujo de trabajo:

* 🔵 **Azul:** Módulo de entrada de archivos y visualización gráfica.
* 🟢 **Verde:** Configuración de unidades y selección de herramientas de corte.
* 🟠 **Naranja:** Parámetros de la herramienta, diámetros, número de pasadas y cálculo de trayectorias.
* 🟣 **Morado:** Control de origen, velocidades de avance y guardado final del archivo RML.

<img src="../recursos/imgs/mods_vista_general_nodos.png" alt="Vista general de nodos en Mods con secciones resaltadas por colores" width="800">

---

## 3. Recorrido Detallado por la Interfaz de Mods

Una vez que comprendemos la estructura general de los nodos, procederemos a desplazarnos paso a paso por cada una de las secciones operativas de la interfaz para configurar correctamente el maquinado de nuestra placa.

### 3.1. Esquina Superior Izquierda: Carga del Archivo SVG
En esta sección inicial se gestiona la entrada de nuestro diseño. 
* Encontraremos el módulo para cargar el archivo vectorial (SVG) que exportamos previamente (ya sea contorno, pistas o perforaciones).
* Es importante verificar que el archivo cargue correctamente antes de continuar con la visualización.

<img src="../recursos/imgs/mods_esquina_superior_izquierda.png" alt="Módulo de carga de archivos SVG en la esquina superior izquierda de Mods" width="600">

### 3.2. Panel de Vistas (Lado Derecho): Previsualización Gráfica
Justo al lado derecho del módulo de entrada, se despliegan distintas vistas e interpretaciones gráficas de nuestro archivo cargado. 
* **Regla fundamental:** Lo que se visualiza en color **negro** representa las zonas donde la fresa pasará removiendo material, mientras que las zonas blancas permanecerán intactas.
* Aquí podemos validar visualmente que las pistas o los contornos se rendericen de manera correcta y sin recortes extraños.

<img src="../recursos/imgs/mods_panel_vistas_derecha.png" alt="Panel de vistas previas mostrando el diseño en negro sobre blanco" width="800">

### 3.3. Esquina Inferior Izquierda: Unidades y Herramientas Predefinidas
Desplazándonos hacia la esquina inferior izquierda, configuraremos las bases métricas y operativas del trabajo:
* **Conversión de unidades:** Asegúrate de cambiar las medidas de pulgadas (`in`) a milímetros (`mm`) para trabajar bajo el sistema métrico estándar.
* **Herramientas predefinidas:** En este apartado podemos seleccionar algunas configuraciones y geometrías de corte ya preestablecidas, dependiendo de si realizaremos un proceso de contorno, trazado de pistas o perforación.

<img src="../recursos/imgs/mods_esquina_inferior_izquierda.png" alt="Configuración de unidades en mm y herramientas predefinidas en la esquina inferior izquierda" width="600">

### 3.4. Parte Central: Configuración Avanzada de Herramienta y Cálculo 3D
En la zona central de los nodos encontraremos los parámetros finos de la herramienta de corte:
* **Modificación de parámetros:** Aquí podemos ajustar de forma precisa el diámetro de la herramienta y el número de pasadas que realizará la máquina.
* **Simulación visual:** El sistema nos ofrece una estimación gráfica de cómo se comportará la herramienta sobre la superficie de la placa.
* **Cálculo de trayectorias:** Al presionar el botón de **Calculate**, la herramienta procesará las trayectorias y se abrirá automáticamente una pestaña adicional donde podremos inspeccionar la **vista interactiva en 3D** del maquinado.

<img src="../recursos/imgs/mods_centro_configuracion_herramienta.png" alt="Panel central de nodos para configurar diámetro, pasadas y cálculo de trayectorias" width="800">

<img src="../recursos/imgs/visualizacion3d.png" alt="Vista de la vizualización 3d " width="800">


### 3.5. Panel Derecho: Orígenes, Velocidades y Exportación RML
Finalmente, desplazándonos hacia la sección derecha de los nodos, controlaremos los parámetros finales de posicionamiento y ejecución:
* **Fijar el Origen:** Por defecto, estableceremos siempre **`0` en Y** y **`0` en Z**. El único valor que modificaremos es **X** en escenarios específicos donde estemos fabricando dos placas simultáneamente o requiramos un desfase en la cama de la fresadora.
* **Control de Velocidades:** 
  * Para los procesos de **pistas y contornos**, utilizaremos una velocidad de avance de **4 mm/s**.
  * Para los procesos de **perforaciones**, la velocidad se reduce drásticamente a **0.4 o 0.3 mm/s** para evitar la ruptura de las brocas delgadas.
* **Estimación de Tiempo:** En este mismo panel el sistema calculará un estimado del tiempo que le tomará a la MonoFab completar el proceso actual.
* **Guardado del Archivo:** Por último, encontraremos la opción para generar y guardar el archivo con extensión `.rml` directamente en nuestro equipo, listo para enviarse a la máquina.

<img src="../recursos/imgs/mods_panel_derecho_origen_velocidad.png" alt="Configuración de origen y velocidades" width="800">

<img src="../recursos/imgs/mods_descarga.png" alt="Guardado de archivo RML en el panel derecho" width="800">

---
