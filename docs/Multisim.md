# Guía de Inicio Rápido: Dominando NI Multisim de Cero a Avanzado

Bienvenido a esta guía completa y detallada sobre el uso de **NI Multisim** para el diseño, simulación y validación de circuitos electrónicos analógicos, digitales y mixtos. Aquí encontrarás los conceptos fundamentales, la configuración de herramientas lógicas avanzadas, la instrumentación virtual de laboratorio y los motores de análisis de simulación necesarios para verificar el comportamiento de tus diseños antes de llevarlos a la fabricación física.

---

## Contenido
- [1. Entorno General y Pantalla Principal de Multisim](#1-entorno-general-y-pantalla-principal-de-multisim)
- [2. Simulación de Circuitos Digitales y Compuertas TTL](#2-simulación-de-circuitos-digitales-y-compuertas-lógicas)
- [3. Uso de Etiquetas de Red y Nodos de Conexión](#3-uso-de-etiquetas-de-red-y-nodos-de-conexión)
- [4. El Convertidor Lógico (Logic Converter)](#4-el-convertidor-lógico-logic-converter)
- [5. Modos de Análisis y Simulación Avanzada](#5-modos-de-análisis-y-simulación-avanzada)
- [6. Instrumentación Virtual: Generadores de Señales y Osciloscopios](#6-instrumentación-virtual-generadores-de-señales-y-osciloscopios)

---

## 1. Entorno General y Pantalla Principal de Multisim

Para comenzar con el desarrollo de nuestras simulaciones, debemos abrir la aplicación desde el buscador de nuestro equipo. Una vez iniciada, nos encontramos con el gestor y el espacio de trabajo principal.

### Vista General del Entorno y Interfaz
La pantalla principal de Multisim está estructurada para optimizar el flujo de trabajo en el diseño electrónico:
* **Lienzo de Trabajo (Workspace):** El área cuadriculada central donde colocamos, interconectamos y alimentamos los componentes de nuestros diagramas esquemáticos.
* **Barra de Menús y Herramientas Superiores:** Ubicada en la parte alta, permite gestionar archivos, editar elementos, configurar opciones de visualización y controlar el inicio, pausa o detención de las simulaciones.
* **Barra Lateral de Componentes:** Contiene los accesos directos para buscar dispositivos organizados por familias tecnológicas (fuentes, componentes básicos pasivos, semiconductores, circuitos integrados digitales TTL y CMOS, entre otros).
* **Barra Lateral Derecha (Instrumentos Virtuales):** Un panel dedicado exclusivamente a la instrumentación de banco, que incluye multímetros, osciloscopios, generadores de funciones, analizadores de redes y el convertidor lógico.

<img src="../recursos/imgs/multisim_pantalla_completa.png" alt="Vista general de Multisim a pantalla completa mostrando el lienzo y las barras de herramientas" width="800">

---

## 2. Simulación de Circuitos Digitales y Compuertas TTL

El editor de esquemas de Multisim permite implementar lógica booleana y sistemas digitales complejos utilizando familias lógicas estándar de la industria.

### Inserción de Componentes TTL
Para añadir compuertas lógicas al lienzo de trabajo:
1. Dirígete a la barra superior de herramientas y haz clic en la herramienta de componentes **TTL** (pertenecientes a la familia lógica Transistor-Transistor Logic).
2. Se abrirá una ventana de diálogo y búsqueda de componentes. En la barra de búsqueda superior, ingresa la matrícula del circuito integrado deseado (por ejemplo, `74LS08` para compuertas AND de dos entradas, `74LS32` para compuertas OR, o `74LS04` para inversores NOT).
3. **Selección de sub-compuertas del circuito integrado:** Al seleccionar un chip lógico (como el `74LS08`), notarás que el software te asigna letras complementarias (como `A`, `B`, `C` o `D`). Esto ocurre porque un circuito integrado físico real contiene en su interior múltiples compuertas independientes; Multisim te permite elegir exactamente cuál de ellas deseas colocar en tu diagrama esquemático. 
   - *Nota técnica:* Si utilizas varias compuertas de un mismo tipo pero requieres que pertenezcan a chips físicos separados, asegúrate de utilizar designadores de componentes distintos (por ejemplo, `U1A`, `U2A`).

<img src="../recursos/imgs/multisim_seleccion_subpuerta.png" alt="Diálogo de selección de sub-compuertas y matrículas de circuitos integrados TTL" width="600">

### Fuentes Digitales Interactivas
Para alimentar las entradas de nuestros circuitos digitales y probar combinaciones lógicas en tiempo real:
1. Haz clic en el icono de **Fuentes** (*Place Source*) ubicado en la barra lateral o superior.
2. En el panel de categorías, selecciona la familia **Digital Sources** y elige la opción **Interactive Digital Source**.
3. Coloca las fuentes necesarias en el espacio de trabajo. Estas funcionarán como interruptores virtuales interactivos que te permitirán alternar dinámicamente entre los estados lógicos de nivel bajo (`0` o $0\text{ V}$) y nivel alto (`1` o $5\text{ V}$) mientras la simulación se encuentra corriendo.

<img src="../recursos/imgs/multisim_fuente_digital_interactiva.png" alt="Panel de selección y colocación de fuentes digitales interactivas" width="600">

---

## 3. Uso de Etiquetas de Red y Nodos de Conexión

Para evitar saturar el diagrama esquemático con líneas de cableado largas, cruzadas y difíciles de rastrear, se emplean las **etiquetas de red (Nodos)**.

### Pasos para Etiquetar y Unificar Nodos
1. Haz clic en la terminal de un componente y arrastra el cursor para trazar un pequeño segmento de línea de conexión.
2. Haz **doble clic** sobre dicha línea (la cual adquiere por defecto un color rojo al conectarse) para abrir la ventana de propiedades de la red (*Net Properties*).
3. Asigna un nombre identificativo claro (por ejemplo, `A`, `B`, `C` o `D`) y asegúrate de marcar la opción para hacer visible el nombre del nodo directamente en el esquemático.
4. Al colocar otra etiqueta con exactamente el mismo nombre en otra sección distante del circuito, Multisim detectará la coincidencia y te preguntará si deseas unirlas al mismo nodo eléctrico; confirma la acción para interconectar las señales de manera limpia, ordenada y sin ruteo físico complejo.

<img src="../recursos/imgs/multisim_propiedades_red_nodo.png" alt="Ventana de propiedades del nodo para asignar y visualizar etiquetas de red" width="600">

### Indicadores Lógicos (*Logic Probes*)
Para comprobar de manera visual el estado de salida de un sistema digital sin necesidad de integrar componentes físicos adicionales como diodos LED, resistencias limitadoras de corriente y conexiones a tierra:
1. Dirígete al menú de **Indicadores** ubicado en la barra de herramientas superior.
2. Selecciona una punta de prueba lógica (*Probe*) y colócala directamente sobre el nodo final de salida. Al iniciar la simulación, la punta cambiará de color o se iluminará para reflejar de forma inmediata si el nivel lógico obtenido es alto (`1`) o bajo (`0`).

<img src="../recursos/imgs/multisim_puntas_prueba.png" alt="Puntas de prueba lógicas colocadas en las salidas del circuito digital" width="600">
---

## 4. El Convertidor Lógico (Logic Converter)

El **Convertidor Lógico** (*Logic Converter*) es una de las herramientas virtuales más potentes de Multisim, diseñada para automatizar y simplificar la relación matemática entre tablas de verdad, expresiones booleanas y diagramas esquemáticos.

### Configuración y Uso del Instrumento
1. Coloca el **Logic Converter** seleccionándolo desde la barra lateral derecha de instrumentos virtuales y ubícalo en una sección libre del lienzo.
2. Conecta las terminales de entrada del instrumento (etiquetadas como $A, B, C$, etc., ordenadas desde el bit más significativo hasta el menos significativo) hacia los nodos de entrada de tu circuito lógico.
3. Conecta la terminal de salida del instrumento (etiquetada como `S`) hacia la salida principal del sistema.
4. Haz doble clic sobre el icono del instrumento para abrir su panel de control interactivo. En la sección inferior encontrarás tres botones clave de conversión:
   - **`Circuito -> Tabla`:** Analiza un circuito esquemático ya armado en el lienzo y genera automáticamente su tabla de verdad completa.
   - **`Tabla -> Función`:** A partir de una tabla de verdad (ingresada de forma manual o generada por el circuito), calcula de manera instantánea la función booleana simplificada en forma sumatoria de minitérminos o productos lógicos.
   - **Generación de Esquemáticos:** Permite ingresar una expresión algebraica booleana directamente en el panel y generar de forma automática todas las compuertas y conexiones necesarias dentro del lienzo de trabajo.

<img src="../recursos/imgs/multisim_logic_converter_panel.png" alt="Interfaz y panel de control detallado del convertidor lógico" width="600">

---

## 5. Modos de Análisis y Simulación Avanzada

Multisim integra potentes motores de cálculo matemático tipo SPICE para evaluar con alta precisión el comportamiento físico, transitorio y eléctrico de los circuitos analógicos y semiconductores.

### Configuración de Análisis
Para acceder a estas herramientas especializadas, dirígete al menú superior y selecciona **Simulación > Análisis y simulación** (*Simulate > Analyses and Simulation*). Los modos principales son:

* **Análisis Transitorio (*Transient Analysis*):** 
  Estudia la evolución de las variables del circuito en función del tiempo real. Es indispensable para observar fenómenos dinámicos como los tiempos de carga y descarga exponencial en arreglos de capacitores e inductores. Se configuran el tiempo inicial ($t_i = 0\text{ s}$), el tiempo de parada (*Stop time*) en milisegundos o segundos, y las variables de salida específicas que se desean graficar.
* **Análisis de Barrido DC (*DC Sweep*):** 
  Ejecuta variaciones de voltaje o corriente punto a punto en estado estacionario. Se utiliza fundamentalmente para caracterizar dispositivos semiconductores como los transistores bipolares (BJT en configuración de emisor común), permitiendo trazar las familias de curvas características de salida al relacionar el voltaje colector-emisor ($V_{CE}$) frente a la corriente de colector ($I_C$) bajo distintos escalones de corriente de base ($I_B$).
* **Análisis de Temperatura (*Temperature Analysis*):** 
  Permite medir la sensibilidad y deriva térmica en el rendimiento de los componentes variando la temperatura de operación dentro de un rango determinado de grados centígrados, ideal para evaluar condiciones industriales extremas.

<img src="../recursos/imgs/multisim_analisis_simulacion.png" alt="Ventana de configuración de análisis y simulación avanzada" width="600">
---

## 6. Instrumentación Virtual: Generador de Señales y Osciloscopio

Para el diseño, medición y validación de circuitos analógicos que operan con corriente alterna o señales periódicas, Multisim ofrece un banco de instrumentos virtuales de alta precisión.

### Generador de Funciones y Osciloscopio
1. **Generador de Funciones:** Permite inyectar señales de estímulo de CA al circuito. Al hacer doble clic sobre su icono, puedes configurar la forma de onda (senoidal, triangular o cuadrada), ajustar la frecuencia en Hertz, la amplitud pico-pico y el nivel de offset. Asimismo, permite cargar archivos de datos externos para reproducir perfiles de señales reales del mundo real.
2. **Osciloscopio:** Conecta el Canal 1 ($CH1$) al punto de estímulo de entrada y el Canal 2 ($CH2$) a la salida del circuito (por ejemplo, posterior a un arreglo de diodos rectificadores), asegurándote de llevar las referencias de tierra de ambos canales al nodo común (`GND`).
   - **Personalización visual de cables:** Haz clic derecho sobre cada línea de conexión, selecciona **Propiedades** y cambia el color de los cables (por ejemplo, asigna azul o amarillo al canal 2). Esto facilitará enormemente la interpretación de las ondas en pantalla.
   - **Función Auto-set:** Una vez iniciada la simulación haciendo clic en **Correr** (*Run*), abre la interfaz del osciloscopio y presiona el botón **Auto-set**. El instrumento ajustará automáticamente las escalas de tiempo ($Time/Div$) y voltaje ($Volts/Div$) para estabilizar y mostrar claramente las señales superpuestas, permitiendo analizar efectos como el recorte de semiciclos en circuitos con diodos.

<img src="../recursos/imgs/multisim_osciloscopio_pantalla.png" alt="Visualización y análisis de señales de entrada y salida en el osciloscopio virtual" width="800">

??? tip "Recomendaciones de ingeniería"
    - Verifica siempre que el modo de simulación activo en la esquina superior derecha de la interfaz coincida con el tipo de prueba que deseas ejecutar (modo interactivo, transitorio o análisis DC) antes de presionar el botón de inicio.
    - El uso metódico de estas herramientas de simulación previene errores críticos de diseño y optimiza de manera sustancial el desarrollo de proyectos electrónicos previos a la manufactura de circuitos impresos.
