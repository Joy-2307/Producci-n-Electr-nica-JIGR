# Guía de Inicio Rápido: Primeros pasos con KiCad

Bienvenido a esta guía básica sobre el uso de **KiCad** para el diseño de circuitos impresos (PCB). Aquí encontrarás los conceptos fundamentales y el flujo de trabajo esencial para pasar de un diagrama esquemático hasta el diseño físico de tu tarjeta, incluyendo la incorporación de librerías externas como la de Fab Lab (`fablib`).

---

## Tabla de Contenido
- [1. Introducción y Entorno General de KiCad](#1-introducción-y-entorno-general-de-kicad)
- [2. Instalación de KiCad y Configuración de la Librería Fab Lab](#2-instalación-de-kicad-y-configuración-de-la-librería-fablib)
- [3. El Editor de Esquemas (Schematic Editor)](#3-el-editor-de-esquemas-schematic-editor)
- [4. El Editor de Placas (PCB Editor)](#4-el-editor-de-placas-pcb-editor)
- [5. Verificación (DRC) y Exportación de Archivos](#5-verificación-drc-y-exportación-de-archivos)

---

## 1. Introducción y Entorno General de KiCad
Para comenzar a familiarizarnos con el software, es importante comprender la estructura del entorno de trabajo. El gestor principal de KiCad es el centro de control donde se administran y vinculan todos los archivos fuente del proyecto (esquemático, diseño de placa, archivos vectoriales SVG e historial).

### Vista General del Proyecto
En la siguiente vista a pantalla completa se aprecia el gestor de proyectos (con el proyecto **HELLOWORLD**), el cual da acceso directo a las herramientas integradas como el editor de esquemas, editor de placas y visores de fabricación.

<img src="../recursos/imgs/kicad_pantalla_completa_general.png" alt="Vista general de KiCad a pantalla completa" width="800">

---

## 2. Instalación de KiCad y Configuración de la Librería Fab Lab
Para comenzar con el desarrollo de nuestros circuitos, debemos dirigirnos al sitio oficial para obtener la versión más reciente compatible con nuestro equipo.

> 🔗 [Sitio oficial de descarga de KiCad](https://www.kicad.org/download/)

### Proceso de Descarga
1. **Selección del Sistema Operativo:** En la primera vista del sitio web, elegimos la plataforma de trabajo (Windows, macOS, Linux o Docker).
   <img src="../recursos/imgs/kicad_seleccion_so.png" alt="Pantalla de selección de sistema operativo" width="600">

2. **Selección de Espejos (Mirrors):** Al seleccionar nuestro sistema, accedemos a la versión estable actual (como la versión 10.0.6 en 64 bits). Aquí podemos elegir un servidor geográfico cercano (Asia, Europa, Norteamérica, etc.) respaldado por instituciones aliadas (CERN, GitHub, etc.) para garantizar una descarga rápida y segura.
   <img src="../recursos/imgs/kicad_espejos_descarga.png" alt="Panel de espejos de descarga" width="600">

### Instalación de la Librería `fablib`
Para trabajar con los componentes estándar de fabricación digital y laboratorios Fab Lab:
1. Abre KiCad y dirígete al **Administrador de complementos y contenidos**.
2. En la pestaña de **Bibliotecas**, busca `FABLIB`, descárgala y completa la instalación.
3. Guarda los cambios, cierra y vuelve a abrir el programa para asegurar su correcta integración.

<img src="../recursos/imgs/fablib_instalacion.png" alt="Administrador de bibliotecas con fablib" width="600">

---

## 3. El Editor de Esquemas (Schematic Editor)
El editor de esquemas es el lugar donde defines la lógica del circuito mediante símbolos y conexiones eléctricas, sin preocuparte todavía por la forma física de la placa.

### Vista del Diagrama Esquemático Completo
A continuación se muestra el circuito lógico completo del proyecto, estructurado en secciones claras como los bloques de **Entradas y Salidas** y el bloque de **Botones**, utilizando los componentes de la librería `fablib` y etiquetas de red.

<img src="../recursos/imgs/esquematico_pantalla_completa.png" alt="Diagrama esquemático completo" width="800">

### Flujo de Trabajo en el Esquemático
* **Inserción de componentes:** Presiona la tecla `A` para abrir el buscador de componentes, selecciona los elementos de `fablib` y colócalos en el lienzo.
  <img src="../recursos/imgs/esquematico_agregar_componente.png" alt="Diálogo de selección de componentes" width="600">

* **Uso de etiquetas (Labels) y conexiones:** Para conectar nodos distantes sin saturar el diseño, presiona `L` para añadir etiquetas de red con el mismo nombre, o usa la herramienta de cable (`W`).
  <img src="../recursos/imgs/esquematico_etiquetas.png" alt="Esquema con etiquetas de red" width="600">

* **Apoyo visual y organización:** Utiliza rectángulos y texto gráfico (barra lateral derecha) para documentar visualmente tu diagrama de forma estética.
  <img src="../recursos/imgs/esquematico_apoyo_visual.png" alt="Cuadros organizadores y texto descriptivo" width="600">

* **Detección de errores (ERC):** Ejecuta el chequeo de reglas eléctricas (icono de insecto con palomita en la barra superior) para asegurar que no existan pines sin conectar o salidas cruzadas.
  <img src="../recursos/imgs/esquematico_erc.png" alt="Ventana de ejecución del ERC" width="600">

---

## 4. El Editor de Placas (PCB Editor)
Una vez verificado el esquema, pasamos al diseño físico de la tarjeta.

### Vista del Editor de Placas (PCB Editor)
Esta vista de pantalla completa muestra el diseño físico final de la tarjeta con una singular **geometría en forma de corazón**, evidenciando el ruteo completo sobre la capa frontal (`F.Cu`), el contorno en `Edge.Cuts` y las zonas rellenas.

<img src="../recursos/imgs/pcb_pantalla_completa.png" alt="Editor de placas PCB en pantalla completa" width="800">

### Pasos de Diseño de la Tarjeta
1. **Actualizar PCB desde el esquema:** Presiona `F8` para transferir componentes y conexiones lógicas.
   <img src="../recursos/imgs/pcb_actualizar.png" alt="Botón de actualización de la PCB" width="600">
   <img src="../recursos/imgs/pcb_actualizar1.png" alt="Ventana de actualización de la PCB" width="600">

2. **Gestión de Capas:** Trabaja principalmente sobre la capa superior **F.Cu** (cobre frontal) y la capa **Edge.Cuts** (contorno de la tarjeta).
   <img src="../recursos/imgs/pcb_capas.png" alt="Panel de gestión de capas" width="600">

3. **Configuración y Ruteo:** 
   * Define grosores predeterminados (ej. **0.4 mm** para pistas y **0.8 mm** para contornos).
   * Traza las pistas con la herramienta Ruta (`X`), evitando ángulos rectos de 90°.
   <img src="../recursos/imgs/pcb_ancho_pistas.png" alt="Ancho de pistas" width="600">
   <img src="../recursos/imgs/pcb_ruteo.png" alt="Pistas ruteadas" width="600">

   > **¿Qué hacer si una pista se cruza?** Puedes regresar al esquemático para añadir una resistencia de `0 ohms` como puente físico, y actualizar la placa.
   > <img src="../recursos/imgs/pcb_puente_resistencia.png" alt="Puente con resistencia" width="600">

4. **Elementos Adicionales:**
   * **Texto:** Añade nombres o versiones con la herramienta `T`.
   * **Perforaciones:** Crea círculos en capas de usuario y utiliza matrices (`Ctrl + T`).
   * **Contornos y Zonas Rellenas:** Dibuja el borde en `Edge.Cuts` y añade zonas llenas (`Ctrl + Shift + Z`) asignadas a redes como `GND`, presionando la tecla `B` para actualizar los rellenos.
   <img src="../recursos/imgs/pcb_texto.png" alt="Texto en placa" width="600">
   <img src="../recursos/imgs/pcb_perforaciones_matriz.png" alt="Perforaciones y matriz" width="600">
   <img src="../recursos/imgs/pcb_contorno_zonas.png" alt="Contorno y zonas" width="600">
   <img src="../recursos/imgs/pcb_zona_rellena_panel.png" alt="Configuración de zonas rellenas" width="600">

---

## 5. Verificación (DRC) y Exportación de Archivos

### Configuración de Reglas de Diseño y DRC
Antes de fabricar, configura los parámetros de aislamiento y anchos mínimos de pista en el menú de **Reglas de Diseño -> Requerimientos** acorde a las capacidades de tu laboratorio.
* Ejecuta el **Verificador de Reglas de Diseño (DRC)** para garantizar la ausencia de cortos circuitos o errores geométricos.
<img src="../recursos/imgs/pcb_reglas_drc_config.png" alt="Configuración de reglas de diseño" width="600">
<img src="../recursos/imgs/pcb_drc.png" alt="Ventana del DRC sin errores" width="600">

### Exportación de Archivos de Fabricación
1. Ve a **Archivo > Salidas de fabricación > Gerbers** (o formato vectorial **SVG** para corte/fresado digital).
2. Selecciona las capas deseadas (pistas, contornos, perforaciones), ajusta la página y genera los trazos para manufactura.
<img src="../recursos/imgs/pcb_salidas_de_fabricacion.png" alt="Menú de salidas de fabricación" width="600">
<img src="../recursos/imgs/Captura de pantalla 2026-09-12 232851.png" alt="Configuración de archivos Gerber y SVG" width="600">
