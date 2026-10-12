# Guía Completa de Inicio Rápido: Uso y Simulación en NI Multisim

Bienvenido a esta guía detallada sobre **NI Multisim**, la plataforma de simulación y diseño de circuitos electrónicos. Esta guía está diseñada para llevarte paso a paso desde el conocimiento básico del entorno hasta la ejecución de análisis avanzados (transitorios, barridos de DC y respuesta térmica), pasando por la síntesis de lógica digital y el manejo de instrumentación virtual de laboratorio.

---

## Contenido
- [1. Introducción y Entorno General de Multisim](#1-introducción-y-entorno-general-de-multisim)
- [2. Simulación de Lógica Digital y Compuertas TTL Paso a Paso](#2-simulación-de-lógica-digital-y-compuertas-ttl-paso-a-paso)
- [3. El Convertidor Lógico (Logic Converter)](#3-el-convertidor-lógico-logic-converter)
- [4. Tipos de Análisis de Simulación (Transitorio, DC Sweep y Temperatura)](#4-tipos-de-análisis-de-simulación-transitorio-dc-sweep-y-temperatura)
- [5. Instrumentación Virtual: Generadores y Osciloscopios](#5-instrumentación-virtual-generadores-y-osciloscopios)

---

## 1. Introducción y Entorno General de Multisim

NI Multisim es un entorno de simulación SPICE y captura de esquemáticos que permite analizar el comportamiento de circuitos analógicos, digitales y mixtos[cite: 1]. Su función principal es predecir cómo responderá un circuito real antes de ensamblarlo físicamente o llevarlo a una tarjeta de circuito impreso (PCB)[cite: 1].

### Búsqueda y Apertura del Programa
1. En el sistema operativo de tu equipo de cómputo, dirígete a la barra de búsqueda rápida o menú de inicio[cite: 1].
2. Escribe **Multisim**[cite: 1]. El icono de la aplicación se reconoce por líneas que se cruzan representando esquemáticos eléctricos[cite: 1].
3. Haz clic sobre el acceso directo para iniciar el software[cite: 1].

<img src="../recursos/imgs/multisim_inicio_buscador.png" alt="Búsqueda de NI Multisim en el sistema operativo" width="600">

### Exploración de la Interfaz Principal
Al abrir Multisim, te encontrarás con las siguientes áreas de trabajo principales[cite: 1]:
* **Lienzo Principal (Worksheet):** Área central cuadriculada donde se colocan y cablean los componentes[cite: 1].
* **Barra Superior de Componentes:** Permite acceder a las familias de componentes agrupadas (fuentes, componentes básicos, semiconductores, circuitos integrados TTL, etc.)[cite: 1].
* **Barra Lateral Derecha (Instrumentos):** Contiene los instrumentos virtuales de medición como voltímetros, osciloscopios, generadores de funciones y convertidores lógicos[cite: 1].
* **Barra de Control de Simulación:** Ubicada en la parte superior, incluye los botones de **Iniciar/Correr (Run)**, **Pausar (Pause)** y **Detener (Stop)**[cite: 1].

<img src="../recursos/imgs/multisim_pantalla_completa.png" alt="Vista general del entorno de trabajo de NI Multisim" width="800">

---

## 2. Simulación de Lógica Digital y Compuertas TTL Paso a Paso

Para comprender el flujo de trabajo básico, comenzaremos implementando una función de álgebra booleana mediante compuertas de la familia **TTL** (*Transistor-Transistor Logic*)[cite: 1].

<img src="../recursos/imgs/esquematico_digital_referencia.png" alt="Diagrama esquemático de lógica booleana a implementar" width="600">

### Paso 1: Selección y Colocación de Compuertas Lógicas (TTL)
1. En la barra superior de componentes, haz clic en el icono **Colocar TTL** (*Place TTL*)[cite: 1].
2. Se desplegará la ventana de búsqueda de componentes[cite: 1].
3. Para una compuerta **AND**, escribe la matrícula de la familia integrada, en este caso la `74LS08`[cite: 1].

<img src="../recursos/imgs/multisim_busqueda_74ls08.png" alt="Ventana de selección del componente 74LS08" width="600">

> **¿Por qué aparecen las opciones A, B, C y D al seleccionar una compuerta?**
> Un circuito integrado físico (como el `74LS08`) alberga en su interior 4 compuertas AND independientes[cite: 1]. Multisim te permite elegir cuál de las 4 compuertas del chip deseas usar (`A`, `B`, `C` o `D`)[cite: 1].
> - Procura seleccionar letras distintas para cada compuerta que agregues si deseas repartir las conexiones dentro del mismo integrado físico[cite: 1].
> - Si los componentes tienen nombres de chip distintos (por ejemplo `U1A`, `U2A`), significará que pertenecen a circuitos integrados físicos separados[cite: 1].

<img src="../recursos/imgs/multisim_seleccion_subpuerta.png" alt="Selección de sub-compuerta A, B, C o D dentro del chip" width="600">

4. Repite el proceso para agregar las compuertas necesarias[cite: 1]:
   - **Compuerta AND:** Matricula `74LS08`[cite: 1].
   - **Compuerta OR:** Matrícula `74LS32`[cite: 1].
   - **Compuerta NOT (Inversor):** Matrícula `74LS04`[cite: 1].

### Paso 2: Colocación de Fuentes Digitales Interactivas
Para simular entradas lógicas cuyo estado (`0` o `1`) puedas cambiar dinámicamente en tiempo de ejecución:
1. Dirígete a la barra de componentes y haz clic en el icono de **Fuentes / Tierra** (*Place Source*)[cite: 1].
2. En la lista desplegable de la izquierda, selecciona la familia **Digital Sources**[cite: 1].
3. Selecciona el componente **INTERACTIVE_DIGITAL_CONSTANT**[cite: 1].
4. Coloca cuatro de estas fuentes en el lienzo para representar las entradas lógicas (por ejemplo, $A, B, C, D$)[cite: 1].

<img src="../recursos/imgs/multisim_fuente_digital_interactiva.png" alt="Selección de la fuente digital interactiva en el menú Place Source" width="600">

### Paso 3: Cableado y Creación de Nodos / Etiquetas de Red (Labels)
En lugar de tirar líneas largas que crucen todo el diagrama, simplificaremos el esquemático usando **nodos y etiquetas de red**[cite: 1]:

1. Pasa el cursor sobre la terminal de salida de una fuente interactiva hasta que el puntero cambie de una flecha a una cruz con nodo[cite: 1].
2. Haz un clic izquierdo, arrastra una pequeña línea hacia la derecha y vuelve a hacer clic para fijar la conexión[cite: 1]. Se generará una línea de red (por defecto color rojo)[cite: 1].
3. Haz **doble clic** sobre la línea roja creada[cite: 1].
4. Se abrirá la ventana emergente de propiedades de la red (*Net Properties*)[cite: 1].
5. En el campo de texto, escribe el nombre que identificará a esa red (por ejemplo, `A`)[cite: 1]. Marca la casilla para hacer visible el nombre en el esquemático y presiona **Aceptar**[cite: 1].
6. Al colocar otra línea en la entrada de una compuerta y nombrarla igual (`A`), Multisim detectará automáticamente la coincidencia y te preguntará si deseas unir ambas líneas al mismo nodo eléctrico[cite: 1]. Confirma la opción para unificar la señal de manera limpia[cite: 1].

<img src="../recursos/imgs/multisim_propiedades_red_nodo.png" alt="Ventana de propiedades del nodo para renombrar la red" width="600">

### Paso 4: Colocación de Indicadores (Puntas de Prueba Lógicas)
Para observar el resultado lógico de salida sin necesidad de colocar un diodo LED, una resistencia y una tierra física[cite: 1]:
1. Haz clic en el menú de **Indicadores** (*Place Indicator*), ubicado en la barra superior con forma de display de 7 segmentos[cite: 1].
2. Selecciona el apartado **PROBE** (Puntas de prueba)[cite: 1].
3. Elige el color de preferencia para tu indicador lógico (por ejemplo, rojo) y presiona **Aceptar**[cite: 1].
4. Conecta el terminal de la punta de prueba al nodo final de salida de tu circuito[cite: 1].

<img src="../recursos/imgs/multisim_colocar_punta_prueba.png" alt="Selección de punta de prueba en el menú de Indicadores" width="600">

### Paso 5: Ejecución de la Simulación Digital
1. Verifica que el interruptor de modo de simulación en la esquina superior derecha esté ajustado en **Interactive**[cite: 1].
2. Haz clic en el botón de reproducción **Correr** (*Run*) o presiona la tecla `F5`[cite: 1].
3. Presiona con el cursor o la tecla de acceso rápido sobre las fuentes digitales interactivas para cambiar su valor entre `0` (0V) y `1` (5V)[cite: 1].
4. Observa cómo la punta de prueba de salida se enciende cuando la combinación de entradas produce un nivel alto (`1`) según la función booleana[cite: 1].

<img src="../recursos/imgs/multisim_simulacion_digital_activa.png" alt="Circuito digital en simulación interactiva con la punta de prueba encendida" width="800">
---

## 3. Uso del Convertidor Lógico (*Logic Converter*)

El **Convertidor Lógico** es una de las herramientas virtuales más potentes y versátiles de Multisim. Permite relacionar directamente tablas de verdad, expresiones booleanas y diagramas esquemáticos de forma automática[cite: 1].

### Localización y Conexión del Instrumento
1. En la barra lateral derecha de instrumentos virtuales, localiza el icono del **Logic Converter** (identificado con una pequeña tabla de verdad y compuertas) y colócalo en cualquier parte libre del lienzo[cite: 1].
2. Conecta las terminales de entrada del instrumento (etiquetadas desde $A$ hasta el bit menos significativo) hacia las líneas de entrada de tu circuito lógico[cite: 1].
3. Conecta la terminal de salida del instrumento (etiquetada como `S`) hacia la salida o nodo principal del sistema[cite: 1].

<img src="../recursos/imgs/multisim_logic_converter_conexion.png" alt="Conexión del convertidor lógico a un circuito digital" width="600">

### Funciones Principales del Convertidor Lógico
Haz doble clic sobre el icono del instrumento para abrir su ventana de control principal. En ella encontrarás los siguientes botones de conversión en la parte inferior[cite: 1]:

* **Del Circuito a la Tabla de Verdad (`Circuito -> Tabla`):** 
  Si tienes un circuito esquemático armado en el lienzo, al hacer clic en este botón el instrumento analizará todas las combinaciones posibles y llenará automáticamente la tabla de verdad correspondiente[cite: 1].
* **Obtención de la Función Lógica (`Tabla -> Función`):** 
  A partir de una tabla de verdad (ya sea generada desde un circuito o introducida manualmente), este botón calcula la expresión booleana en su forma canónica o simplificada[cite: 1].
* **Del Circuito a la Expresión o viceversa:** 
  Permite ingresar una ecuación booleana directamente y generar de forma automática las compuertas y conexiones necesarias en el lienzo de trabajo[cite: 1].

<img src="../recursos/imgs/multisim_logic_converter_panel.png" alt="Panel detallado del Logic Converter mostrando la tabla de verdad y opciones de conversión" width="600">

---

## 4. Tipos de Análisis de Simulación (Transitorio, DC y Temperatura)

Además de la simulación interactiva básica, Multisim cuenta con potentes motores matemáticos para realizar análisis especializados en componentes analógicos y semiconductores[cite: 1]. 

Para acceder a ellos, dirígete al menú superior y selecciona **Simulación > Análisis y simulación** (*Simulate > Analyses and Simulation*)[cite: 1].

<img src="../recursos/imgs/multisim_menu_analisis.png" alt="Menú superior de análisis y simulación en Multisim" width="600">

### 1. Análisis Transitorio (*Transient Analysis*)
* **¿Qué evalúa?** Estudia el comportamiento del circuito en función del tiempo real[cite: 1].
* **Aplicación principal:** Es indispensable para observar fenómenos temporales como los tiempos de carga y descarga exponencial en capacitores e inductores, o para analizar respuestas de frecuencia con osciloscopios[cite: 1].
* **Configuración:** En la ventana de configuración, establece el tiempo inicial (típicamente `0` segundos) y un tiempo de parada adecuado (por ejemplo, `5 ms` o `1 s` dependiendo de la constante de tiempo de tu circuito)[cite: 1]. En la pestaña de **Salida** (*Output*), selecciona la variable o nodo que deseas graficar (como el voltaje en un capacitor) y haz clic en **Correr** (*Run*)[cite: 1].

<img src="../recursos/imgs/multisim_analisis_transitorio.png" alt="Ventana de configuración del análisis transitorio y gráfica resultante" width="800">

### 2. Análisis de Barrido DC (*DC Sweep*)
* **¿Qué evalúa?** Realiza variaciones de voltaje o corriente de manera punto a punto en estado estable[cite: 1].
* **Aplicación principal:** Se utiliza fundamentalmente para caracterizar dispositivos semiconductores como los transistores bipolares (BJT en configuración de emisor común). Permite trazar las curvas características de salida relacionando el voltaje colector-emisor ($V_{CE}$) frente a la corriente de colector ($I_C$) bajo distintas corrientes de base ($I_B$)[cite: 1].
* **Configuración:** 
  1. Coloca un transistor (por ejemplo, el modelo clásico `2N2222`) junto con fuentes de corriente o voltaje independientes en la base y el colector[cite: 1].
  2. En el menú de análisis DC, define la fuente principal que fungirá como eje X (por ejemplo, el voltaje colector-emisor) y configura una fuente secundaria para realizar las familias de curvas variando la corriente de base por incrementos[cite: 1].
  3. Selecciona la corriente de colector como variable dependiente de salida y ejecuta la simulación para obtener las gráficas características[cite: 1].

<img src="../recursos/imgs/multisim_analisis_dc_sweep.png" alt="Configuración de barrido DC para curvas características de un transistor" width="800">

### 3. Análisis de Temperatura (*Temperature Analysis*)
* **¿Qué evalúa?** Permite medir la sensibilidad y variación en el rendimiento de los circuitos ante cambios en la temperatura ambiental o de operación[cite: 1].
* **Aplicación principal:** Muy útil en diseños industriales o automotrices donde los componentes sufren derivas térmicas importantes[cite: 1].
* **Configuración:** Selecciona el rango de temperatura a simular (por ejemplo, desde los $0\text{ °C}$ hasta los $150\text{ °C}$ con un número determinado de puntos de muestreo) y ejecuta el análisis transitorio o de DC asociado para observar el comportamiento superpuesto de las curvas[cite: 1].

<img src="../recursos/imgs/multisim_analisis_temperatura.png" alt="Configuración del análisis de temperatura en Multisim" width="600">
---

## 5. Instrumentación Virtual: Generadores de Señal y Osciloscopios

Para el diseño, análisis y validación de circuitos analógicos que operan con corrientes alternas, señales periódicas o transductores, Multisim incluye una barra completa de instrumentos de laboratorio virtuales de alta precisión[cite: 1].

### El Generador de Funciones (*Function Generator*)
El generador de funciones es la fuente principal de estímulo AC en el banco de trabajo virtual[cite: 1]. 
1. **Colocación:** Búscalo en la barra lateral derecha de instrumentos y colócalo en el esquemático[cite: 1]. Cuenta con terminales de salida (fase o señal y común/tierra)[cite: 1].
2. **Configuración de parámetros:** Haz doble clic sobre el instrumento para desplegar su panel de control. En él podrás configurar[cite: 1]:
   - **Forma de onda:** Selecciona entre onda **senoidal** (onda pura), **triangular** o **cuadrada**[cite: 1].
   - **Frecuencia, Amplitud y Offset:** Ajusta los valores numéricos según las especificaciones requeridas por tu práctica (por ejemplo, una frecuencia de $1\text{ kHz}$ o $60\text{ Hz}$ y una amplitud pico-pico determinada)[cite: 1].

<img src="../recursos/imgs/multisim_generador_funciones_panel.png" alt="Panel de configuración detallada del generador de funciones" width="600">

#### Inyección de señales personalizadas mediante archivos externos
Además de las formas de onda estándar, Multisim permite utilizar fuentes controladas para reproducir señales del mundo real (como bioseñales cardíacas en aplicaciones biomédicas, respuestas de motores o señales de sensores complejos)[cite: 1]:
* Al configurar fuentes avanzadas de señal, es posible cargar un archivo de datos externo con perfiles de voltaje específicos para que el circuito reaccione ante estímulos reales personalizados[cite: 1].

---

### El Osciloscopio y las Puntas de Prueba
Para visualizar de forma gráfica la evolución de las señales analógicas en el tiempo (por ejemplo, el efecto de recorte de onda provocado por diodos rectificadores):

1. **Selección del instrumento:** Puedes utilizar el osciloscopio estándar de dos canales o instrumentos avanzados como el **Osciloscopio Tektronix** integrado en el software[cite: 1].
2. **Conexión de canales:** 
   - Conecta el **Canal 1** ($CH1$) al punto de entrada o estímulo principal (salida del generador).
   - Conecta el **Canal 2** ($CH2$) al punto de salida del circuito (por ejemplo, después de un elemento semiconductor como un diodo).
   - Conecta las referencias de tierra de ambos canales al nodo común (`GND`) del circuito[cite: 1].

> 💡 **Recomendación de ruteo visual:** 
> Como por defecto todas las líneas de conexión en Multisim pueden aparecer del mismo color (generalmente rojo), se recomienda hacer **clic derecho sobre cada cable**, seleccionar **Propiedades** (*Properties*) y cambiar el color de la línea del canal 2 (por ejemplo, a azul o amarillo). Esto evitará confusiones al interpretar las formas de onda en la pantalla del osciloscopio[cite: 1].

<img src="../recursos/imgs/multisim_conexion_osciloscopio.png" alt="Conexión de canales de osciloscopio con colores personalizados" width="800">

### Operación del Osciloscopio y Función Auto-set
1. Inicia la simulación haciendo clic en **Correr** (*Run*) y haz doble clic sobre el icono del osciloscopio para abrir su monitor de visualización[cite: 1].
2. Enciende el instrumento presionando el botón de poder (*Power*)[cite: 1].
3. Utiliza el botón de ajuste automático (**Auto-set**) característico de los osciloscopios modernos. Esta función ajustará de manera inteligente la escala de tiempo ($Time/Div$) y la escala de voltaje ($Volts/Div$) para estabilizar y mostrar claramente ambas señales en pantalla[cite: 1].
4. **Análisis de resultados:** Al visualizar las señales superpuestas (por ejemplo, la onda amarilla de entrada frente a la onda azul de salida), podrás notar el comportamiento de componentes como los diodos, los cuales permiten el flujo de corriente en una sola dirección bloqueando el semiciclo negativo (recorte de señal), o invirtiendo su polaridad para bloquear el semiciclo opuesto[cite: 1].

<img src="../recursos/imgs/multisim_osciloscopio_pantalla.png" alt="Pantalla del osciloscopio virtual mostrando la señal de entrada y la señal rectificada por el diodo" width="800">

---

## 💡 Consejos Prácticos y Resolución de Incidencias Comunes

- **Errores de modo de simulación:** Si al presionar *Run* el programa indica un error de compatibilidad o la simulación no arranca, verifica que el modo superior derecho esté configurado correctamente acorde a los elementos analógicos o digitales presentes en tu lienzo (por ejemplo, modo interactivo o análisis transitorio)[cite: 1].
- **Importancia de la simulación previa:** El dominio de estas herramientas de simulación te permitirá validar algoritmos lógicos, circuitos con transistores y respuestas en frecuencia antes de invertir tiempo en la manufactura física de circuitos impresos (PCB)[cite: 1].
