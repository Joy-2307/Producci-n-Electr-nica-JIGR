# Guía de Altium Designer: Desde cero hasta el diseño de una PCB

Esta guía tiene como objetivo explicar de forma detallada el flujo de trabajo básico y las principales herramientas de **Altium Designer**, desde la creación inicial de un proyecto hasta la preparación de una tarjeta de circuito impreso para fabricación.

La documentación está desarrollada utilizando como referencia **Altium Designer 26.11.1**.

El propósito no es documentar un circuito específico, sino crear un manual reutilizable que permita recordar **qué herramienta utilizar, dónde encontrarla, qué función cumple y cómo utilizarla correctamente**.

> [!NOTE]
> Altium Designer es un programa muy amplio. Una misma operación puede realizarse desde menús superiores, barras de herramientas, paneles contextuales, clic derecho o atajos de teclado. En esta guía se dará prioridad a las rutas mediante menús, ya que son más fáciles de localizar cuando no se recuerdan los atajos.

---

## Contenido

- [1. Instalación de Altium Designer](#1-instalación-de-altium-designer)
- [2. Introducción al entorno de Altium Designer](#2-introducción-al-entorno-de-altium-designer)
- [3. Tipos de archivos utilizados por Altium Designer](#3-tipos-de-archivos-utilizados-por-altium-designer)
- [4. Creación de un proyecto PCB](#4-creación-de-un-proyecto-pcb)
- [5. Paneles principales de Altium Designer](#5-paneles-principales-de-altium-designer)
- [6. Navegación dentro del espacio de trabajo](#6-navegación-dentro-del-espacio-de-trabajo)
- [7. Configuración de unidades y cuadrícula](#7-configuración-de-unidades-y-cuadrícula)
- [8. Componentes, símbolos, footprints y modelos 3D](#8-componentes-símbolos-footprints-y-modelos-3d)
- [9. Bibliotecas en Altium Designer](#9-bibliotecas-en-altium-designer)
- [10. Importación de una biblioteca externa](#10-importación-de-una-biblioteca-externa)
- [11. Uso de SnapMagic para encontrar componentes](#11-uso-de-snapmagic-para-encontrar-componentes)
- [12. El editor de esquemas](#12-el-editor-de-esquemas)
- [13. Configuración inicial de una hoja de esquemático](#13-configuración-inicial-de-una-hoja-de-esquemático)
- [14. Inserción de componentes](#14-inserción-de-componentes)
- [15. Propiedades de los componentes](#15-propiedades-de-los-componentes)
- [16. Mover, rotar y reflejar componentes](#16-mover-rotar-y-reflejar-componentes)
- [17. Designadores y anotación automática](#17-designadores-y-anotación-automática)
- [18. Conexiones mediante Wire](#18-conexiones-mediante-wire)
- [19. Junctions y conexiones eléctricas](#19-junctions-y-conexiones-eléctricas)
- [20. Net Labels](#20-net-labels)
- [21. Ports](#21-ports)
- [22. Alimentación y tierra mediante Power Ports](#22-alimentación-y-tierra-mediante-power-ports)
- [23. Elementos gráficos y documentación del esquemático](#23-elementos-gráficos-y-documentación-del-esquemático)
- [24. Organización recomendada del esquemático](#24-organización-recomendada-del-esquemático)
- [25. Validación eléctrica del proyecto](#25-validación-eléctrica-del-proyecto)
- [26. Configuración del ERC](#26-configuración-del-erc)
- [27. Panel Messages](#27-panel-messages)
- [28. No ERC](#28-no-erc)
- [29. Comprobaciones antes de pasar al PCB](#29-comprobaciones-antes-de-pasar-al-pcb)

---

# 1. Instalación de Altium Designer

Para comenzar a trabajar es necesario instalar **Altium Designer** desde la plataforma oficial de Altium.

A diferencia de programas completamente gratuitos como KiCad, Altium Designer requiere una licencia válida, licencia educativa, prueba disponible o acceso proporcionado por una institución u organización.

El instalador normalmente se distribuye mediante un archivo cuyo nombre sigue una estructura similar a:

```text
AltiumDesignerSetup_<Version>.exe
```

## Proceso general de instalación

1. Accede al sitio oficial de Altium.
2. Inicia sesión con tu cuenta.
3. Dirígete al apartado de descargas de **Altium Designer**.
4. Selecciona la versión que deseas instalar.
5. Descarga el instalador.
6. Ejecuta el archivo descargado.
7. Acepta el acuerdo de licencia.
8. Inicia sesión cuando el instalador lo solicite.
9. Selecciona las funcionalidades que deseas instalar.
10. Selecciona las carpetas de instalación.
11. Inicia la instalación.
12. Abre Altium Designer una vez finalizado el proceso.

Altium permite instalar versiones distintas de Altium Designer de manera independiente. Esto puede ser útil cuando un proyecto debe mantenerse en una versión determinada.

<img src="../recursos/imgs/altium_descarga_instalador.png" alt="Página de descarga de Altium Designer" width="600">

### Selección de funcionalidades

Durante la instalación pueden aparecer diferentes funcionalidades adicionales.

Para un flujo normal de diseño electrónico es recomendable asegurarse de disponer, como mínimo, de las herramientas relacionadas con:

- Schematic Capture.
- PCB Design.
- Importadores y exportadores necesarios.
- Generación de archivos de fabricación.

Algunos importadores utilizados para formatos antiguos o externos pueden requerir componentes adicionales.

<img src="../recursos/imgs/altium_instalacion_features.png" alt="Selección de funcionalidades durante la instalación de Altium Designer" width="600">

> [!TIP]
> Si posteriormente descubres que falta alguna funcionalidad, no necesariamente es necesario reinstalar completamente Altium. La instalación puede modificarse para agregar características adicionales.

---

# 2. Introducción al entorno de Altium Designer

Altium Designer funciona como un entorno unificado de diseño electrónico.

Esto significa que el esquemático, la PCB, las bibliotecas, los modelos tridimensionales, las reglas eléctricas y los archivos de fabricación pueden administrarse desde el mismo programa.

Al abrir Altium Designer encontraremos una interfaz compuesta principalmente por:

- Barra de menús.
- Barra de herramientas.
- Área central de documentos.
- Paneles laterales.
- Panel `Projects`.
- Panel `Properties`.
- Panel `Components`.
- Paneles específicos dependiendo del editor activo.
- Barra inferior de estado.

<img src="../recursos/imgs/altium_pantalla_general.png" alt="Vista general de Altium Designer 26" width="800">

## Un concepto importante: la interfaz es contextual

Altium cambia muchas de sus opciones dependiendo del documento que se encuentre activo.

Por ejemplo:

- Si seleccionamos un archivo `.SchDoc`, aparecerán herramientas relacionadas con esquemáticos.
- Si seleccionamos un `.PcbDoc`, aparecerán herramientas relacionadas con diseño físico de PCB.
- Si abrimos una `.SchLib`, entraremos al editor de símbolos.
- Si abrimos una `.PcbLib`, entraremos al editor de footprints.

Por esta razón, si una herramienta descrita en esta guía no aparece, una de las primeras cosas que debemos comprobar es **qué documento se encuentra activo**.

---

# 3. Tipos de archivos utilizados por Altium Designer

Antes de comenzar es importante comprender los principales archivos que encontraremos.

## `.PrjPcb`

Es el archivo principal del proyecto PCB.

Ejemplo:

```text
MiProyecto.PrjPcb
```

No contiene físicamente todo el diseño dentro de un único archivo. Funciona principalmente como el archivo que organiza los documentos pertenecientes al proyecto y determinadas configuraciones.

---

## `.SchDoc`

Es un documento de esquemático.

Ejemplo:

```text
Principal.SchDoc
```

Contiene:

- Símbolos electrónicos.
- Pines.
- Wires.
- Net Labels.
- Ports.
- Power Ports.
- Información gráfica.
- Conectividad lógica.

Un proyecto puede contener uno o múltiples `.SchDoc`.

---

## `.PcbDoc`

Es el documento correspondiente al diseño físico de la PCB.

Ejemplo:

```text
Principal.PcbDoc
```

Aquí se encuentran:

- Footprints.
- Pads.
- Tracks.
- Vias.
- Polígonos.
- Capas.
- Contorno de la tarjeta.
- Reglas físicas.
- Información de fabricación.

---

## `.SchLib`

Es una **Schematic Library**.

Contiene símbolos utilizados en el esquemático.

```text
Componentes.SchLib
```

---

## `.PcbLib`

Es una **PCB Library**.

Contiene footprints.

```text
Componentes.PcbLib
```

---

## `.IntLib`

Es una **Integrated Library**.

```text
Componentes.IntLib
```

Puede reunir en un solo paquete la información necesaria para utilizar componentes, incluyendo símbolos y sus modelos asociados.

Es uno de los formatos más cómodos para distribuir bibliotecas externas.

---

## `.OutJob`

Es un archivo de configuración de salidas.

```text
Fabricacion.OutJob
```

Puede utilizarse posteriormente para centralizar la generación de:

- Gerber.
- NC Drill.
- Pick and Place.
- BOM.
- PDF.
- Informes.
- Otros documentos de fabricación.

Su utilización se explicará en la sección correspondiente a fabricación.

---

# 4. Creación de un proyecto PCB

Un proyecto debe crearse antes de comenzar a desarrollar el circuito.

La estructura recomendada consiste en mantener todos los archivos relacionados dentro de una misma carpeta.

Por ejemplo:

```text
MiProyecto/
│
├── MiProyecto.PrjPcb
├── Principal.SchDoc
├── MiProyecto.PcbDoc
├── Libraries/
├── Outputs/
└── Datasheets/
```

Esto facilita:

- Respaldar el proyecto.
- Moverlo entre computadoras.
- Subirlo a GitHub.
- Evitar archivos perdidos.
- Localizar bibliotecas externas.
- Localizar archivos de fabricación.

## Crear un proyecto

Desde Altium Designer crea un nuevo proyecto de tipo PCB.

Una vez creado aparecerá en el panel **Projects**.

<img src="../recursos/imgs/altium_nuevo_proyecto_pcb.png" alt="Creación de un nuevo proyecto PCB en Altium Designer" width="600">

## Panel Projects

El panel `Projects` muestra la estructura del proyecto.

Si no se encuentra visible, puede abrirse mediante:

```text
View → Panels → Projects
```

Dependiendo de la configuración de la interfaz también puede encontrarse mediante el botón de paneles ubicado en una esquina de la ventana.

<img src="../recursos/imgs/altium_panel_projects.png" alt="Panel Projects mostrando la estructura del proyecto" width="350">

---

## Añadir un esquemático

Sobre el nombre del proyecto:

1. Haz clic derecho.
2. Selecciona:

```text
Add New to Project → Schematic
```

3. Aparecerá un nuevo documento.
4. Guárdalo inmediatamente.
5. Asigna un nombre descriptivo.

Por ejemplo:

```text
Main.SchDoc
```

o:

```text
Power.SchDoc
Control.SchDoc
Inputs.SchDoc
```

---

## Añadir un documento PCB

Sobre el proyecto:

1. Haz clic derecho.
2. Selecciona:

```text
Add New to Project → PCB
```

3. Guarda el archivo.

Por ejemplo:

```text
Main.PcbDoc
```

Todavía no es necesario diseñar la placa. El documento puede permanecer vacío mientras desarrollamos el esquemático.

<img src="../recursos/imgs/altium_archivos_proyecto.png" alt="Proyecto de Altium con documentos SchDoc y PcbDoc" width="450">

---

# 5. Paneles principales de Altium Designer

Los paneles son fundamentales para trabajar eficientemente.

En general pueden abrirse desde:

```text
View → Panels
```

Algunos de los paneles que utilizaremos con mayor frecuencia son:

| Panel | Función |
|---|---|
| `Projects` | Administrar documentos del proyecto |
| `Properties` | Modificar las propiedades del objeto seleccionado |
| `Components` | Buscar y colocar componentes |
| `Messages` | Mostrar errores y advertencias |
| `PCB` | Navegar elementos del PCB |
| `PCB Filter` | Filtrar objetos mediante consultas |
| `PCB Rules And Violations` | Inspeccionar reglas y violaciones |
| `SCH Filter` | Filtrar elementos del esquemático |

---

## Panel Properties

Uno de los paneles más importantes es:

```text
Properties
```

Su contenido cambia automáticamente según lo seleccionado.

Por ejemplo:

Si seleccionas una resistencia, mostrará sus propiedades.

Si seleccionas una pista, mostrará:

- ancho;
- capa;
- net;
- coordenadas.

Si no seleccionas ningún objeto en un esquemático, mostrará las propiedades de la hoja.

<img src="../recursos/imgs/altium_panel_properties.png" alt="Panel Properties de Altium Designer" width="350">

> [!IMPORTANT]
> Cuando una opción que buscas no aparece, primero haz clic en un espacio vacío del documento. En muchas ocasiones el panel `Properties` está mostrando las propiedades del objeto seleccionado en lugar de las opciones del documento.

---

# 6. Navegación dentro del espacio de trabajo

Antes de comenzar un diseño es importante familiarizarse con la navegación.

Altium permite:

- acercar;
- alejar;
- desplazarse;
- seleccionar;
- mover objetos;
- arrastrar conexiones;
- editar propiedades.

La rueda del ratón es una de las herramientas principales para navegar.

El comportamiento exacto puede depender de las preferencias configuradas.

---

## Selección

Para seleccionar un objeto:

```text
clic izquierdo
```

Una vez seleccionado pueden aparecer:

- manejadores;
- contornos;
- información en `Properties`.

Para seleccionar múltiples objetos puede emplearse una ventana de selección o las teclas modificadoras correspondientes.

---

## Cancelar una herramienta

Una operación fundamental en Altium es:

```text
Esc
```

`Esc` permite salir progresivamente de una herramienta.

Por ejemplo:

1. Estamos colocando un Wire.
2. Presionamos `Esc`.
3. Se termina el Wire actual.
4. Podemos presionar nuevamente `Esc` para abandonar completamente la herramienta.

Dependiendo de la operación pueden requerirse uno o varios `Esc`.

---

# 7. Configuración de unidades y cuadrícula

La cuadrícula o **Grid** determina los incrementos utilizados para colocar objetos.

Es extremadamente importante tanto en el esquemático como en la PCB.

---

## Grid del esquemático

Con un `.SchDoc` abierto:

1. Haz clic en un espacio vacío.
2. Abre el panel:

```text
Properties
```

3. Busca las opciones correspondientes al Grid.

Aquí encontraremos conceptos como:

### Visible Grid

Determina la cuadrícula que podemos ver visualmente.

### Snap Grid

Determina los incrementos a los que se ajustan los objetos al moverlos.

### Electrical Snap

Ayuda a que el cursor se adhiera a puntos eléctricamente conectables, como:

- extremos de pines;
- Wires;
- puntos de conexión.

<img src="../recursos/imgs/altium_schematic_grid.png" alt="Configuración de Grid en un documento esquemático" width="450">

---

## Cambiar rápidamente el Snap Grid

Altium permite recorrer los valores de cuadrícula configurados utilizando:

```text
G
```

Esto resulta especialmente útil cuando necesitamos:

- una cuadrícula grande para organizar bloques;
- una cuadrícula más pequeña para realizar ajustes.

> [!WARNING]
> Evita reducir excesivamente el Grid del esquemático sin necesidad. Los pines de los componentes suelen estar diseñados para trabajar sobre una cuadrícula determinada. Una mala configuración puede provocar que visualmente parezca que un Wire toca un pin cuando eléctricamente no se encuentra conectado.

---

## Unidades

Altium puede trabajar principalmente con:

```text
mil
```

y:

```text
mm
```

Un `mil` corresponde a una milésima de pulgada.

En diseño PCB es común trabajar en milímetros, especialmente cuando las dimensiones mecánicas y especificaciones del fabricante se proporcionan en sistema métrico.

La unidad activa puede modificarse desde las opciones de visualización o propiedades del documento.

> [!NOTE]
> No confundir `mil` con `mm`. Son unidades completamente diferentes.

---

# 8. Componentes, símbolos, footprints y modelos 3D

Este concepto es fundamental para entender Altium Designer.

Un **componente electrónico completo** puede contener diferentes representaciones.

## Símbolo esquemático

Es la representación lógica del componente.

Ejemplo:

```text
Resistencia
```

Puede representarse como:

```text
--/\/\/\--
```

Su función es facilitar la interpretación eléctrica.

No representa necesariamente las dimensiones físicas reales.

---

## Footprint

El **footprint** representa cómo se instalará físicamente el componente sobre la PCB.

Contiene elementos como:

- Pads.
- Separaciones.
- Serigrafía.
- Contorno.
- Información mecánica.

Por ejemplo, una resistencia podría utilizar:

```text
0603
0805
1206
Axial
```

Aunque eléctricamente todas sean resistencias, físicamente son componentes distintos.

---

## Modelo 3D

El modelo 3D permite visualizar la apariencia física aproximada del componente.

Puede utilizar formatos como:

```text
.STEP
.STP
```

El modelo 3D no determina la conectividad eléctrica.

---

## Relación entre los tres

Podemos imaginar la estructura de un componente como:

```text
COMPONENTE
│
├── Símbolo esquemático
│
├── Footprint PCB
│
├── Modelo 3D
│
└── Parámetros
    ├── Valor
    ├── Fabricante
    ├── Número de parte
    └── Descripción
```

> [!IMPORTANT]
> Que un componente aparezca correctamente en el esquemático **no significa que esté listo para pasar al PCB**.

Debe contar con un footprint correctamente asociado.

---

# 9. Bibliotecas en Altium Designer

Las bibliotecas permiten almacenar componentes reutilizables.

Entre los principales formatos encontraremos:

```text
.SchLib
.PcbLib
.IntLib
```

---

## Schematic Library

Archivo:

```text
*.SchLib
```

Contiene principalmente símbolos de esquemático.

---

## PCB Library

Archivo:

```text
*.PcbLib
```

Contiene footprints.

Puede incluir también información tridimensional asociada.

---

## Integrated Library

Archivo:

```text
*.IntLib
```

Una biblioteca integrada permite empaquetar componentes y sus modelos asociados de una manera más cómoda para distribución.

Por esta razón, cuando descargamos una biblioteca externa es bastante común encontrar:

```text
Componente.IntLib
```

---

# 10. Importación de una biblioteca externa

Si disponemos de una biblioteca `.IntLib`, podemos instalarla directamente en Altium.

## Método mediante archivo

1. Descarga la biblioteca.
2. Descomprime el archivo si se encuentra dentro de un `.ZIP`.
3. Localiza:

```text
*.IntLib
```

4. Abre el archivo con Altium Designer.

En muchas situaciones puede hacerse:

```text
doble clic sobre el archivo .IntLib
```

También puede arrastrarse hacia Altium Designer.

Altium puede ofrecer opciones como:

```text
Install Library
```

o:

```text
Extract Sources
```

---

## Install Library

Esta es la opción adecuada cuando solamente queremos utilizar los componentes.

Selecciona:

```text
Install Library
```

La biblioteca quedará disponible entre las bibliotecas basadas en archivos instaladas.

---

## Extract Sources

Esta opción extrae los archivos fuente utilizados para construir la biblioteca.

Es útil cuando:

- queremos editar el símbolo;
- queremos modificar el footprint;
- queremos inspeccionar la biblioteca;
- queremos desarrollar una versión personalizada.

Para utilizar simplemente el componente normalmente no será necesario extraer los fuentes.

<img src="../recursos/imgs/altium_intlib_install.png" alt="Ventana para instalar o extraer una biblioteca IntLib" width="600">

---

## Comprobar que la biblioteca fue instalada

Abre:

```text
View → Panels → Components
```

Dentro del panel `Components`, utiliza el selector de fuente o biblioteca.

Busca la biblioteca recién instalada.

Posteriormente busca uno de sus componentes.

<img src="../recursos/imgs/altium_components_panel.png" alt="Panel Components mostrando una biblioteca instalada" width="450">

---

# 11. Uso de SnapMagic para encontrar componentes

En muchos proyectos encontraremos componentes que no aparecen directamente en las bibliotecas disponibles.

En estos casos puede utilizarse **SnapMagic**.

SnapMagic permite buscar componentes electrónicos y, cuando existe un modelo disponible, descargar información como:

- símbolo esquemático;
- footprint;
- modelo 3D;
- información paramétrica.

> [!IMPORTANT]
> Una biblioteca descargada de Internet nunca debe utilizarse ciegamente. Antes de fabricar una PCB debemos comprobar manualmente las dimensiones y la correspondencia entre pines y pads utilizando el datasheet oficial del componente.

---

## Buscar un componente

La forma más segura de encontrar un dispositivo es utilizar su:

```text
Manufacturer Part Number
```

o número exacto de parte.

Por ejemplo, en lugar de buscar:

```text
regulador 5V
```

conviene buscar:

```text
<Número exacto del fabricante>
```

Esto reduce el riesgo de seleccionar:

- otro encapsulado;
- otra variante;
- otra distribución de pines.

<img src="../recursos/imgs/altium_snapmagic_search.png" alt="Búsqueda de un componente mediante SnapMagic" width="700">

---

## Seleccionar formato para Altium

Dentro de la página del componente:

1. Comprueba que el dispositivo sea exactamente el correcto.
2. Revisa fabricante.
3. Revisa número de parte.
4. Comprueba encapsulado.
5. Selecciona el formato compatible con:

```text
Altium Designer
```

6. Descarga los archivos.

<img src="../recursos/imgs/altium_snapmagic_download.png" alt="Descarga de componente para Altium desde SnapMagic" width="600">

---

## Importar un `.IntLib` de SnapMagic

Si el archivo descargado contiene:

```text
*.IntLib
```

realiza el siguiente procedimiento:

1. Descomprime el archivo.
2. Localiza el `.IntLib`.
3. Haz doble clic sobre él o arrástralo a Altium.
4. Selecciona:

```text
Install Library
```

5. Abre:

```text
View → Panels → Components
```

6. Busca el componente.
7. Comprueba símbolo.
8. Comprueba footprint.

<img src="../recursos/imgs/altium_snapmagic_import.png" alt="Biblioteca de SnapMagic instalada dentro de Altium Designer" width="600">

---

## Si SnapMagic entrega un archivo `.lia`

Algunas bibliotecas antiguas pueden encontrarse en formato:

```text
.lia
```

Este formato procede del ecosistema P-CAD.

Altium puede importarlo mediante su correspondiente **P-CAD Importer**.

Si Altium no reconoce el archivo, revisa que el importador se encuentre instalado desde las opciones de instalación/extensiones.

Para proyectos nuevos es preferible utilizar el formato nativo de Altium cuando se encuentre disponible.

---

# 12. El editor de esquemas

El **Schematic Editor** permite representar la lógica eléctrica del circuito.

Aquí definiremos:

- componentes;
- conexiones;
- alimentación;
- señales;
- nombres de redes;
- referencias;
- bloques funcionales.

Todavía no estamos definiendo por dónde pasarán físicamente las pistas.

<img src="../recursos/imgs/altium_schematic_view.png" alt="Vista general del Schematic Editor de Altium Designer" width="800">

---

# 13. Configuración inicial de una hoja de esquemático

Antes de comenzar a colocar componentes conviene configurar la hoja.

Con el `.SchDoc` abierto:

1. Haz clic en un lugar vacío.
2. Abre:

```text
View → Panels → Properties
```

3. El panel mostrará las opciones del documento.

Desde aquí pueden controlarse opciones relacionadas con:

- tamaño de hoja;
- unidades;
- cuadrícula;
- snapping;
- plantillas.

<img src="../recursos/imgs/altium_schematic_document_properties.png" alt="Propiedades de una hoja de esquemático" width="450">

---

## Tamaño de hoja

El tamaño de la hoja no modifica eléctricamente el circuito.

Sin embargo, utilizar un tamaño adecuado facilita mantener el esquemático limpio.

Para diseños pequeños puede utilizarse una hoja estándar.

Para proyectos grandes puede ser preferible:

- utilizar una hoja mayor;
- dividir el circuito en múltiples `.SchDoc`.

---

# 14. Inserción de componentes

Los componentes pueden colocarse principalmente desde el panel:

```text
Components
```

Para abrirlo:

```text
View → Panels → Components
```

<img src="../recursos/imgs/altium_place_component.png" alt="Panel Components utilizado para colocar un componente" width="500">

---

## Buscar un componente

Dentro del panel:

1. Selecciona la biblioteca correspondiente.
2. Utiliza el campo de búsqueda.
3. Introduce el nombre o número de parte.
4. Selecciona el componente.

Antes de colocarlo, revisa la información disponible.

Especialmente:

- nombre;
- descripción;
- footprint;
- fabricante;
- número de parte.

---

## Colocar el componente

Selecciona el componente y utiliza la opción:

```text
Place
```

También puede ser posible:

- hacer doble clic;
- arrastrar el componente hacia la hoja.

Una vez que el componente aparezca unido al cursor:

1. Muévelo a la posición deseada.
2. Oriéntalo correctamente.
3. Haz clic izquierdo para colocarlo.
4. Presiona `Esc` cuando termines.

---

# 15. Propiedades de los componentes

Selecciona un componente.

El panel:

```text
Properties
```

mostrará sus propiedades.

Entre las más importantes encontraremos:

### Designator

Identificación única del componente.

Ejemplos:

```text
R1
R2
C1
U1
D1
J1
```

---

### Comment

Descripción o valor asociado.

Por ejemplo:

```text
10k
100nF
LM358
```

---

### Parameters

Información adicional como:

- fabricante;
- número de parte;
- descripción;
- voltaje;
- tolerancia;
- documentación.

---

### Models

Aquí pueden encontrarse modelos asociados, especialmente el footprint.

> [!IMPORTANT]
> Antes de transferir un componente al PCB debemos comprobar que tenga un footprint asociado.

---

# 16. Mover, rotar y reflejar componentes

Durante la colocación podemos modificar la orientación.

## Rotar

Mientras el componente está unido al cursor:

```text
Space
```

permite rotarlo.

Las rotaciones normalmente se realizan en incrementos de:

```text
90°
```

<img src="../recursos/imgs/altium_component_rotate.png" alt="Rotación de un componente durante su colocación" width="500">

---

## Reflejar

Durante la colocación pueden utilizarse:

```text
X
```

o:

```text
Y
```

para reflejar el componente respecto a determinados ejes.

---

## Editar durante la colocación

Mientras un objeto se encuentra en proceso de colocación puede utilizarse:

```text
Tab
```

para acceder a sus propiedades antes de colocarlo definitivamente.

Esta función resulta extremadamente útil en Altium.

La lógica general es:

```text
Seleccionar herramienta
        ↓
Objeto unido al cursor
        ↓
Presionar Tab
        ↓
Modificar propiedades
        ↓
Regresar a la colocación
```

---

# 17. Designadores y anotación automática

Cada componente debe tener un identificador único.

Por ejemplo:

```text
R1
R2
R3
```

No deberían existir dos componentes con:

```text
R1
```

dentro del mismo alcance en el que los designadores deban ser únicos.

Altium puede asignarlos automáticamente mediante la herramienta de **Annotation**.

---

## Anotar el esquemático

Dirígete a:

```text
Tools → Annotation → Annotate Schematics
```

Se abrirá la ventana de anotación.

<img src="../recursos/imgs/altium_annotate_schematics.png" alt="Ventana Annotate Schematics" width="700">

La herramienta analiza los componentes y propone designadores.

Por ejemplo:

```text
R? → R1
R? → R2
R? → R3

C? → C1
C? → C2

U? → U1
```

---

## Procedimiento recomendado

1. Coloca los componentes.
2. Organízalos.
3. Abre:

```text
Tools → Annotation → Annotate Schematics
```

4. Configura el alcance.
5. Genera la lista de cambios propuesta.
6. Revisa los cambios.
7. Aplícalos.
8. Comprueba que todos los componentes tengan designadores únicos.

> [!TIP]
> Es recomendable realizar una anotación ordenada antes de transferir el diseño al PCB. Esto facilita identificar físicamente cada componente posteriormente.

---

# 18. Conexiones mediante Wire

Una de las diferencias más importantes que debe aprender un usuario nuevo es:

> **Una línea gráfica no es lo mismo que un Wire.**

Para realizar una conexión eléctrica se utiliza:

```text
Place → Wire
```

Altium también dispone de objetos gráficos como:

```text
Place → Line
```

pero una `Line` sirve únicamente para dibujo.

**No genera conectividad eléctrica.**

---

## Colocar un Wire

1. Selecciona:

```text
Place → Wire
```

2. Acerca el cursor al extremo eléctrico de un pin.
3. Haz clic.
4. Mueve el cursor hacia el siguiente punto.
5. Haz clic para crear esquinas cuando sea necesario.
6. Llega hasta el pin de destino.
7. Haz clic para finalizar la conexión.
8. Presiona `Esc` para terminar.
9. Presiona nuevamente `Esc` si deseas abandonar completamente la herramienta.

<img src="../recursos/imgs/altium_schematic_wire.png" alt="Conexión de componentes mediante Wire" width="600">

---

## Cómo comprobar una conexión

No basta con que las líneas parezcan tocarse.

Debemos comprobar que:

- el Wire llegó al hotspot eléctrico del pin;
- no existe un pequeño espacio;
- no se utilizó una `Line`;
- el Wire se encuentra realmente unido a la red.

> [!WARNING]
> Uno de los errores más peligrosos para principiantes es dibujar conexiones utilizando objetos gráficos. El esquemático puede parecer perfectamente conectado mientras eléctricamente los componentes permanecen separados.

---

# 19. Junctions y conexiones eléctricas

Cuando varios Wires se unen puede utilizarse un **Junction** para indicar claramente la unión eléctrica.

Visualmente suele representarse mediante un punto.

Ejemplo:

```text
        |
        |
--------●--------
        |
        |
```

El punto indica que las líneas pertenecen a una misma conexión.

---

## Cruce sin conexión

Dos líneas también pueden cruzarse sin pertenecer a la misma red.

Por esta razón debemos evitar esquemas ambiguos.

Preferiblemente:

- utiliza Junctions donde realmente exista una unión;
- evita cruces innecesarios;
- utiliza Net Labels cuando el cableado se vuelva complejo.

<img src="../recursos/imgs/altium_schematic_junction.png" alt="Ejemplo de Junction en un esquemático" width="500">

---

# 20. Net Labels

Las **Net Labels** permiten asignar nombres a redes.

Son especialmente útiles para evitar llenar el esquemático con cables largos.

Para colocar una:

```text
Place → Net Label
```

---

## Procedimiento

1. Crea un Wire corto desde el pin.
2. Selecciona:

```text
Place → Net Label
```

3. Presiona:

```text
Tab
```

4. En `Properties`, escribe el nombre en:

```text
Net Name
```

5. Regresa al modo de colocación.
6. Coloca la etiqueta sobre el Wire.
7. Verifica que el hotspot de la etiqueta quede conectado.

<img src="../recursos/imgs/altium_net_label.png" alt="Uso de Net Labels en Altium Designer" width="600">

---

## Ejemplo

Tenemos dos puntos separados.

Primer punto:

```text
MCU -------- DATA
```

Segundo punto:

```text
DATA -------- SENSOR
```

Al utilizar la misma Net Label:

```text
DATA
```

Altium entiende que pertenecen a la misma red según el alcance de conectividad configurado.

---

## Nombres recomendados

Utiliza nombres claros.

Por ejemplo:

```text
SDA
SCL
TX
RX
RESET
MOTOR_EN
LED_STATUS
5V
3V3
GND
```

Evita nombres ambiguos como:

```text
A
B
X1
TEMP2
```

cuando no indiquen claramente la función.

---

# 21. Ports

Los **Ports** también permiten identificar y conectar señales, especialmente cuando el diseño utiliza múltiples hojas.

Se colocan mediante:

```text
Place → Port
```

Los Ports son particularmente útiles en diseños:

- jerárquicos;
- con múltiples hojas;
- divididos en bloques funcionales.

Por ejemplo:

```text
Power.SchDoc
      │
      └── 5V

Main.SchDoc
      │
      └── 5V
```

Sin embargo, la forma en que Ports y Net Labels conectan entre diferentes hojas depende de la estructura del proyecto y de la configuración del alcance de los identificadores de red.

> [!IMPORTANT]
> No debes asumir que cualquier Net Label con el mismo nombre conecta automáticamente todas las hojas. Para diseños de múltiples hojas es necesario comprender la configuración de conectividad y jerarquía utilizada por el proyecto.

---

# 22. Alimentación y tierra mediante Power Ports

Para representar redes como:

```text
GND
VCC
5V
3V3
12V
```

pueden utilizarse **Power Ports**.

La herramienta se encuentra en:

```text
Place → Power Port
```

<img src="../recursos/imgs/altium_power_port.png" alt="Colocación de Power Ports en Altium Designer" width="500">

---

## Colocar GND

1. Selecciona:

```text
Place → Power Port
```

2. Presiona `Tab` si necesitas modificar las propiedades.
3. Configura el nombre de la red:

```text
GND
```

4. Selecciona el estilo gráfico deseado.
5. Coloca el Power Port sobre el Wire o pin correspondiente.

---

## Lo verdaderamente importante es el nombre

Es fundamental comprender que el símbolo visual no determina por sí mismo la conexión.

Por ejemplo, podemos tener distintos estilos gráficos.

Lo que realmente determina la red es:

```text
Net Name
```

Por tanto:

```text
GND
```

debe conectarse con otros Power Ports llamados:

```text
GND
```

---

## Ejemplo

```text
          5V
          │
       ┌──┴──┐
       │ MCU │
       └──┬──┘
          │
         GND
```

---

## Redes globales de alimentación

En configuraciones normales, los Power Ports se utilizan para crear redes de alimentación disponibles a través del proyecto.

Esto hace que sea posible evitar líneas de alimentación que atraviesen todo el esquemático.

> [!WARNING]
> No cambies únicamente el dibujo del Power Port suponiendo que eso cambia la señal. Siempre comprueba el nombre eléctrico de la red.

---

# 23. Elementos gráficos y documentación del esquemático

Además de objetos eléctricos, Altium permite colocar elementos gráficos.

Estos sirven para mejorar la documentación y organización.

Entre ellos pueden encontrarse:

- Lines.
- Rectangles.
- Text Strings.
- Text Frames.
- elementos gráficos adicionales.

---

## Texto

Puede añadirse texto para describir bloques.

Ejemplos:

```text
ALIMENTACIÓN
```

```text
ENTRADAS DIGITALES
```

```text
MICROCONTROLADOR
```

```text
SENSORES
```

El texto es informativo y no crea conectividad eléctrica.

<img src="../recursos/imgs/altium_schematic_text.png" alt="Texto descriptivo colocado en un esquemático" width="500">

---

## Rectángulos

Los rectángulos pueden utilizarse para agrupar visualmente bloques.

Ejemplo:

```text
┌─────────────────────────────┐
│       ALIMENTACIÓN          │
│                             │
│    Regulador                │
│    Capacitores              │
│    Conector                 │
│                             │
└─────────────────────────────┘
```

---

## Line frente a Wire

Este punto merece repetirse:

```text
Wire = conexión eléctrica
```

```text
Line = elemento gráfico
```

Nunca utilices `Line` para representar una conexión eléctrica.

---

# 24. Organización recomendada del esquemático

Un esquemático debe diseñarse para que una persona pueda comprenderlo.

No solamente para que Altium pueda interpretarlo.

---

## Divide el circuito en bloques

Por ejemplo:

```text
POWER
```

```text
MICROCONTROLLER
```

```text
INPUTS
```

```text
OUTPUTS
```

```text
COMMUNICATION
```

```text
SENSORS
```

---

## Flujo visual recomendado

Siempre que sea posible:

```text
ENTRADAS → PROCESAMIENTO → SALIDAS
```

y:

```text
ALIMENTACIÓN
      ↓
   CIRCUITO
      ↓
     GND
```

Esto facilita enormemente la lectura.

---

## Evita cables extremadamente largos

En lugar de:

```text
Componente ------------------------------ Componente
```

utiliza Net Labels cuando sea apropiado.

---

## Mantén nombres consistentes

Evita mezclar:

```text
+5V
5V
VCC5
VCC_5V
```

si todos representan exactamente la misma alimentación.

Selecciona una convención.

Por ejemplo:

```text
5V
3V3
GND
```

---

## Mantén el Grid

No coloques arbitrariamente objetos fuera de la cuadrícula para intentar que visualmente se vean mejor.

La conectividad debe tener prioridad sobre pequeños ajustes estéticos.

---

# 25. Validación eléctrica del proyecto

Una vez terminado el esquemático debemos comprobarlo antes de transferirlo al PCB.

Altium dispone de un sistema de validación del proyecto.

Con el proyecto activo utiliza:

```text
Project → Validate PCB Project <NombreDelProyecto>
```

También puede realizarse desde el panel `Projects` mediante las opciones disponibles al hacer clic derecho sobre el proyecto.

<img src="../recursos/imgs/altium_validate_project.png" alt="Validación de un proyecto PCB en Altium Designer" width="600">

---

## ¿Qué comprueba la validación?

Dependiendo de la configuración puede detectar problemas como:

- designadores duplicados;
- conexiones incompatibles;
- Wires flotantes;
- Net Labels flotantes;
- redes con problemas;
- componentes incompletos;
- conflictos eléctricos;
- problemas relacionados con pines;
- errores de documentación lógica.

---

# 26. Configuración del ERC

Las comprobaciones eléctricas dependen de las opciones configuradas para el proyecto.

Abre:

```text
Project → Project Options
```

Dentro encontraremos apartados importantes como:

```text
Error Reporting
```

y:

```text
Connection Matrix
```

<img src="../recursos/imgs/altium_project_options_error_reporting.png" alt="Configuración Error Reporting de Project Options" width="700">

---

## Error Reporting

Permite determinar cómo debe tratarse cada tipo de problema.

Por ejemplo:

```text
Fatal Error
Error
Warning
No Report
```

No todos los proyectos necesitan exactamente la misma configuración.

---

## Connection Matrix

La matriz de conexión determina qué tipos de conexiones entre pines deben considerarse correctas, advertencias o errores.

Por ejemplo, una conexión entre:

```text
Output → Output
```

puede representar un conflicto.

Mientras:

```text
Passive → Passive
```

puede ser perfectamente válida.

<img src="../recursos/imgs/altium_connection_matrix.png" alt="Connection Matrix dentro de Project Options" width="700">

---

> [!WARNING]
> No soluciones un ERC simplemente cambiando todos los errores a `No Report`.

El ERC existe precisamente para detectar errores reales.

Primero debe comprenderse la causa.

Solo debemos modificar una regla cuando sabemos que el comportamiento es intencional.

---

# 27. Panel Messages

Después de ejecutar la validación, los problemas pueden visualizarse en:

```text
View → Panels → Messages
```

El panel muestra:

- errores;
- advertencias;
- documento;
- descripción;
- objeto implicado.

<img src="../recursos/imgs/altium_messages_panel.png" alt="Panel Messages mostrando errores del proyecto" width="700">

---

## Localizar un error

Una de las funciones más útiles del panel consiste en hacer doble clic sobre el problema.

Altium puede llevarnos directamente al objeto involucrado.

Flujo recomendado:

```text
Validate PCB Project
        ↓
Messages
        ↓
Seleccionar error
        ↓
Localizar objeto
        ↓
Corregir
        ↓
Validar nuevamente
```

---

## Limpiar mensajes no corrige los errores

Eliminar mensajes del panel solamente limpia la visualización.

No modifica el diseño.

Si volvemos a ejecutar:

```text
Validate PCB Project
```

los errores que continúen presentes volverán a aparecer.

---

# 28. No ERC

Existen situaciones donde una condición detectada por el ERC es intencional.

En esos casos puede utilizarse una directiva:

```text
No ERC
```

Su propósito es indicarle al sistema que una condición determinada ha sido revisada y debe ignorarse.

---

## Cuándo utilizar No ERC

Ejemplos razonables pueden incluir determinados pines intencionalmente no conectados.

Sin embargo, debemos utilizarlo únicamente cuando:

1. conocemos el motivo de la advertencia;
2. sabemos que la condición es intencional;
3. sabemos que el circuito es eléctricamente correcto.

---

## Procedimiento recomendado

Nunca utilizar esta secuencia:

```text
Aparece error
      ↓
No entiendo el error
      ↓
Coloco No ERC
```

Utilizar:

```text
Aparece error
      ↓
Analizo el problema
      ↓
Compruebo datasheet y diseño
      ↓
Confirmo que es intencional
      ↓
Coloco No ERC
```

> [!CAUTION]
> `No ERC` no corrige un circuito. Solamente indica al verificador que no debe reportar una condición determinada.

---

# 29. Comprobaciones antes de pasar al PCB

Antes de actualizar el documento PCB es recomendable realizar una revisión completa.

## Componentes

Comprobar que:

- todos los componentes necesarios estén colocados;
- no existan componentes duplicados accidentalmente;
- todos tengan designadores únicos;
- todos tengan valores correctos.

---

## Conectividad

Comprobar:

- Wires.
- Junctions.
- Net Labels.
- Ports.
- Power Ports.
- GND.
- Alimentaciones.

---

## Footprints

Para cada componente físico debemos comprobar:

```text
Símbolo → Footprint
```

No solamente que exista un footprint, sino que sea **el footprint correcto**.

---

## Correspondencia entre pines y pads

Este punto es crítico.

Supongamos que el símbolo tiene:

```text
Pin 1 = GND
Pin 2 = VCC
Pin 3 = OUT
```

El footprint debe corresponder físicamente con:

```text
Pad 1 = GND
Pad 2 = VCC
Pad 3 = OUT
```

Si el footprint utiliza una numeración incorrecta, la PCB puede quedar eléctricamente mal aunque Altium no conozca la intención real del fabricante.

---

## Comparar contra el datasheet

Antes de aceptar un componente externo:

1. Descarga el datasheet oficial.
2. Localiza el pinout.
3. Comprueba numeración.
4. Comprueba orientación.
5. Comprueba dimensiones.
6. Comprueba footprint recomendado.
7. Compara contra el componente utilizado en Altium.

Esto es especialmente importante con componentes obtenidos de:

- SnapMagic;
- bibliotecas externas;
- repositorios;
- componentes creados por terceros.

---

## Validación final del esquemático

Ejecuta nuevamente:

```text
Project → Validate PCB Project <Nombre>
```

Posteriormente revisa:

```text
Messages
```

El objetivo no debe ser simplemente conseguir:

```text
0 Errors
```

sino comprender por qué cualquier advertencia restante puede considerarse aceptable.

---

## Estado esperado antes de continuar

Antes de comenzar el diseño físico deberíamos tener:

```text
Proyecto PCB
│
├── .PrjPcb
│
├── Esquemático
│   ├── componentes
│   ├── conexiones
│   ├── etiquetas
│   ├── alimentación
│   └── designadores
│
├── Footprints asignados
│
├── Validación realizada
│
└── .PcbDoc creado
```

Una vez cumplidos estos puntos estamos listos para transferir la información del esquemático hacia el PCB mediante:

```text
Design → Update PCB Document
```

Este proceso no consiste simplemente en copiar los componentes.

Altium comparará la información lógica del proyecto con el documento PCB y generará una serie de **Engineering Change Orders (ECO)** que deberán validarse y ejecutarse.

A partir de este punto comienza el proceso de diseño físico de la tarjeta.

---

# Continuación

La siguiente parte de la documentación comprende:

```text
Esquemático
      ↓
Update PCB Document
      ↓
Engineering Change Order
      ↓
PCB
      ↓
Board Shape
      ↓
Origen
      ↓
Grid
      ↓
Layer Stack
      ↓
Design Rules
      ↓
Placement
      ↓
Routing
      ↓
Vias
      ↓
Polygons
      ↓
DRC
      ↓
Fabricación
```

En esta etapa aprenderemos a convertir la representación lógica del circuito en una tarjeta físicamente fabricable.

# Parte 2: Diseño físico de la PCB en Altium Designer

Una vez terminado y validado el esquemático, el siguiente paso consiste en transformar la representación lógica del circuito en una **tarjeta de circuito impreso físicamente fabricable**.

En esta etapa dejaremos de trabajar únicamente con símbolos y conexiones lógicas para comenzar a definir elementos físicos como:

- dimensiones de la tarjeta;
- posición de componentes;
- capas de cobre;
- separación entre objetos;
- anchura de pistas;
- tamaños de vías;
- planos de tierra;
- restricciones mecánicas;
- reglas de diseño;
- ruteo.

El flujo general será:

```text
Esquemático terminado
        ↓
Update PCB Document
        ↓
Engineering Change Order
        ↓
PCB Editor
        ↓
Board Shape
        ↓
Origen y Grid
        ↓
Layer Stack
        ↓
Placement
        ↓
Design Rules
        ↓
Routing
        ↓
Vias
        ↓
Polygon Pours
        ↓
Revisión
```

---

## Contenido

- [30. Transferencia del esquemático al PCB](#30-transferencia-del-esquemático-al-pcb)
- [31. Engineering Change Order (ECO)](#31-engineering-change-order-eco)
- [32. Errores durante la actualización del PCB](#32-errores-durante-la-actualización-del-pcb)
- [33. Mantener sincronizados el esquemático y la PCB](#33-mantener-sincronizados-el-esquemático-y-la-pcb)
- [34. Vista general del PCB Editor](#34-vista-general-del-pcb-editor)
- [35. Modos de visualización del PCB](#35-modos-de-visualización-del-pcb)
- [36. Definición del Board Shape](#36-definición-del-board-shape)
- [37. Crear el Board Shape desde objetos](#37-crear-el-board-shape-desde-objetos)
- [38. Importar un contorno desde DXF o DWG](#38-importar-un-contorno-desde-dxf-o-dwg)
- [39. Configuración del origen de la PCB](#39-configuración-del-origen-de-la-pcb)
- [40. Configuración de unidades](#40-configuración-de-unidades)
- [41. Configuración del Grid](#41-configuración-del-grid)
- [42. Grid Manager y cuadrículas personalizadas](#42-grid-manager-y-cuadrículas-personalizadas)
- [43. Panel View Configuration](#43-panel-view-configuration)
- [44. Capas principales de una PCB](#44-capas-principales-de-una-pcb)
- [45. Layer Stack Manager](#45-layer-stack-manager)
- [46. Capas mecánicas y documentación](#46-capas-mecánicas-y-documentación)
- [47. Keepouts](#47-keepouts)
- [48. Colocación de componentes](#48-colocación-de-componentes)
- [49. Líneas de conexión o Ratsnest](#49-líneas-de-conexión-o-ratsnest)
- [50. Mover, rotar y cambiar componentes de cara](#50-mover-rotar-y-cambiar-componentes-de-cara)
- [51. Recomendaciones para el Placement](#51-recomendaciones-para-el-placement)
- [52. Rooms](#52-rooms)
- [53. Introducción a las Design Rules](#53-introducción-a-las-design-rules)
- [54. Rules Editor y Constraint Manager](#54-rules-editor-y-constraint-manager)
- [55. Regla de Clearance](#55-regla-de-clearance)
- [56. Regla de Width](#56-regla-de-width)
- [57. Routing Via Style](#57-routing-via-style)
- [58. Crear reglas específicas para determinadas redes](#58-crear-reglas-específicas-para-determinadas-redes)
- [59. Prioridad de reglas](#59-prioridad-de-reglas)
- [60. Net Classes](#60-net-classes)
- [61. Importación y exportación de reglas](#61-importación-y-exportación-de-reglas)
- [62. Comprobaciones antes de comenzar a rutear](#62-comprobaciones-antes-de-comenzar-a-rutear)
- [63. Interactive Routing](#63-interactive-routing)
- [64. Modos de esquina durante el ruteo](#64-modos-de-esquina-durante-el-ruteo)
- [65. Modos de resolución de obstáculos](#65-modos-de-resolución-de-obstáculos)
- [66. Cambiar el ancho de una pista](#66-cambiar-el-ancho-de-una-pista)
- [67. Cambiar de capa durante el ruteo](#67-cambiar-de-capa-durante-el-ruteo)
- [68. Vías](#68-vías)
- [69. Modificar pistas existentes](#69-modificar-pistas-existentes)
- [70. Ruteo de alimentación](#70-ruteo-de-alimentación)
- [71. Polygon Pour](#71-polygon-pour)
- [72. Crear un plano de tierra](#72-crear-un-plano-de-tierra)
- [73. Repour de polígonos](#73-repour-de-polígonos)
- [74. Polygon Cutout](#74-polygon-cutout)
- [75. Orden y prioridad de polígonos](#75-orden-y-prioridad-de-polígonos)
- [76. Shelve Polygons](#76-shelve-polygons)
- [77. Auto Route](#77-auto-route)
- [78. Recomendaciones antes de utilizar el AutoRouter](#78-recomendaciones-antes-de-utilizar-el-autorouter)
- [79. Estado esperado al finalizar esta etapa](#79-estado-esperado-al-finalizar-esta-etapa)

---

# 30. Transferencia del esquemático al PCB

Altium Designer permite transferir directamente la información del esquemático hacia el documento PCB.

No es necesario generar manualmente un archivo intermedio de Netlist para realizar este proceso.

La herramienta principal se encuentra en el **Schematic Editor**.

Con un `.SchDoc` abierto, dirígete a:

```text
Design → Update PCB Document <NombrePCB>.PcbDoc
```

Por ejemplo:

```text
Design → Update PCB Document Main.PcbDoc
```

<img src="../recursos/imgs/altium_update_pcb_document.png" alt="Opción Update PCB Document desde el editor de esquemáticos" width="650">

---

## ¿Qué información se transfiere?

Durante este proceso Altium compara el esquemático con la PCB.

Entre los datos que pueden transferirse se encuentran:

- componentes;
- footprints;
- designadores;
- nets;
- conexiones entre pads;
- clases;
- determinadas reglas;
- información del proyecto.

Por ejemplo, si en el esquemático tenemos:

```text
R1
R2
C1
U1
```

con sus respectivos footprints, Altium intentará crear esos mismos componentes físicamente dentro del documento PCB.

---

## El esquemático es la fuente lógica principal

Es recomendable considerar el esquemático como la fuente principal de la información eléctrica.

Si necesitamos agregar:

```text
R5
```

el procedimiento correcto generalmente será:

```text
Editar esquemático
        ↓
Agregar R5
        ↓
Conectarla
        ↓
Asignar footprint
        ↓
Validar proyecto
        ↓
Update PCB Document
```

No conviene simplemente colocar componentes directamente en el PCB si estos forman parte del circuito lógico, ya que posteriormente puede complicarse la sincronización.

---

# 31. Engineering Change Order (ECO)

Después de seleccionar:

```text
Design → Update PCB Document
```

Altium abrirá una ventana denominada:

```text
Engineering Change Order
```

o:

```text
ECO
```

<img src="../recursos/imgs/altium_engineering_change_order.png" alt="Ventana Engineering Change Order de Altium Designer" width="800">

Esta ventana contiene una lista de todos los cambios que Altium pretende realizar en la PCB.

Por ejemplo:

```text
Add Component R1
Add Component R2
Add Component U1
Add Net GND
Add Net 5V
Add Net SDA
Add Net SCL
```

---

## Validate Changes

Antes de ejecutar los cambios debemos utilizar:

```text
Validate Changes
```

Altium comprobará si las modificaciones propuestas pueden realizarse.

Cuando una operación es válida normalmente aparecerá una indicación positiva en la columna correspondiente.

El flujo recomendado es:

```text
Update PCB Document
        ↓
Engineering Change Order
        ↓
Validate Changes
        ↓
Revisar resultados
        ↓
Execute Changes
```

---

## Execute Changes

Cuando todas las modificaciones importantes hayan sido validadas, utiliza:

```text
Execute Changes
```

Altium aplicará los cambios sobre la PCB.

<img src="../recursos/imgs/altium_eco_validate_execute.png" alt="ECO después de Validate Changes y Execute Changes" width="800">

Una vez terminado el proceso podemos cerrar la ventana.

---

# 32. Errores durante la actualización del PCB

Si `Validate Changes` muestra errores, no debemos continuar ignorándolos.

Dos de los problemas más comunes son:

### Footprint inexistente

El componente existe en el esquemático pero no tiene un modelo PCB válido.

Ejemplo:

```text
U1
 ├── Symbol ✓
 └── Footprint ✗
```

La solución consiste en regresar al componente y asignarle el footprint correcto.

---

### Los pads no corresponden con los pines

Supongamos que el símbolo utiliza:

```text
Pin 1
Pin 2
Pin 3
```

pero el footprint contiene:

```text
Pad A
Pad B
Pad C
```

Altium no puede establecer correctamente la correspondencia.

La relación debe ser coherente:

```text
Pin 1 → Pad 1
Pin 2 → Pad 2
Pin 3 → Pad 3
```

---

## Procedimiento cuando falla un ECO

Utiliza siempre esta secuencia:

```text
ECO falla
    ↓
Cerrar ventana
    ↓
Abrir Messages
    ↓
Identificar componente o Net
    ↓
Corregir esquemático / biblioteca
    ↓
Validar proyecto
    ↓
Update PCB Document
    ↓
Validate Changes
```

> [!WARNING]
> No modifiques manualmente la numeración de pads o pines únicamente para conseguir que desaparezca el error. Primero compara el símbolo y el footprint contra el datasheet oficial.

---

# 33. Mantener sincronizados el esquemático y la PCB

La PCB no se actualiza automáticamente cada vez que modificamos el esquemático.

Por ejemplo, después de haber comenzado el diseño PCB podemos regresar al esquemático y:

- agregar un componente;
- eliminarlo;
- cambiar una Net Label;
- cambiar un footprint;
- modificar una conexión.

Después debemos volver a ejecutar:

```text
Design → Update PCB Document
```

Altium calculará únicamente las diferencias necesarias.

---

## Ejemplo

Estado inicial:

```text
R1
R2
C1
U1
```

Añadimos:

```text
C2
```

Cuando ejecutamos nuevamente el ECO, Altium debería proponer principalmente cambios relacionados con:

```text
Add C2
Add/Modify Nets asociadas
```

y no reconstruir completamente la PCB.

---

## Recomendación

Cada vez que realices una modificación importante en el esquemático:

```text
Guardar
   ↓
Validar
   ↓
Update PCB
   ↓
Validate Changes
   ↓
Execute Changes
   ↓
Guardar PCB
```

Esto ayuda a evitar que ambos documentos evolucionen de forma independiente.

---

# 34. Vista general del PCB Editor

El archivo:

```text
*.PcbDoc
```

se abre dentro del **PCB Editor**.

Aquí se realizará el diseño físico de la tarjeta.

<img src="../recursos/imgs/altium_pcb_editor_general.png" alt="Vista general del PCB Editor de Altium Designer" width="900">

Entre los elementos principales encontraremos:

- espacio de diseño;
- Board Shape;
- componentes;
- pads;
- connection lines;
- pistas;
- vías;
- polígonos;
- capas;
- panel `Properties`;
- panel `PCB`;
- panel `View Configuration`;
- pestañas de capas.

---

# 35. Modos de visualización del PCB

Altium dispone de tres modos principales para visualizar y trabajar con la PCB.

## Board Planning Mode

Atajo:

```text
1
```

Se utiliza principalmente para trabajar con:

- Board Shape;
- regiones de la PCB;
- rigid-flex;
- planificación mecánica.

También puede accederse mediante:

```text
View → Board Planning Mode
```

---

## 2D Layout Mode

Atajo:

```text
2
```

Es el modo principal para:

- colocar componentes;
- rutear;
- colocar vías;
- dibujar polígonos;
- trabajar con capas;
- modificar objetos.

```text
View → 2D Layout Mode
```

---

## 3D Layout Mode

Atajo:

```text
3
```

Permite visualizar físicamente la tarjeta.

```text
View → 3D Layout Mode
```

Es especialmente útil para comprobar:

- orientación de componentes;
- modelos 3D;
- conectores;
- interferencias mecánicas;
- dimensiones generales.

<img src="../recursos/imgs/altium_pcb_2d_3d.png" alt="Comparación de los modos 2D y 3D del PCB" width="800">

---

# 36. Definición del Board Shape

El **Board Shape** determina el contorno físico de la tarjeta.

No debe confundirse con una simple línea gráfica.

El Board Shape le indica a Altium cuáles son los límites reales de la PCB.

---

## Definirlo manualmente

Cambia a:

```text
View → Board Planning Mode
```

o presiona:

```text
1
```

Posteriormente utiliza:

```text
Design → Redefine Board Shape
```

<img src="../recursos/imgs/altium_redefine_board_shape.png" alt="Herramienta Redefine Board Shape" width="650">

---

## Dibujar el contorno

Después de ejecutar el comando:

1. Haz clic en el primer vértice.
2. Mueve el cursor.
3. Haz clic para establecer el siguiente vértice.
4. Continúa alrededor de la tarjeta.
5. Coloca todos los vértices necesarios.
6. Finaliza con clic derecho o `Esc`.

Altium cerrará el contorno.

---

## Cambiar el modo de las esquinas

Durante la definición del contorno puedes utilizar:

```text
Shift + Space
```

para cambiar entre diferentes estilos.

Entre ellos pueden encontrarse:

- 45°;
- 90°;
- arcos;
- cualquier ángulo.

---

## Editar posteriormente el Board Shape

En Board Planning Mode puede utilizarse:

```text
Design → Edit Board Shape
```

según el modo de diseño utilizado.

Esto permite modificar vértices y dimensiones existentes.

---

> [!IMPORTANT]
> El Board Shape debe representar las dimensiones reales de la PCB que será fabricada.

No debe dibujarse únicamente con fines estéticos.

---

# 37. Crear el Board Shape desde objetos

En diseños mecánicos es frecuente definir primero el contorno mediante:

- Lines;
- Tracks sin Net;
- Arcs.

Después podemos utilizar esos objetos para generar el Board Shape.

---

## Procedimiento

1. Cambia al modo:

```text
2D Layout Mode
```

2. Dibuja o importa un contorno completamente cerrado.
3. Selecciona únicamente los objetos que forman ese contorno.
4. Dirígete a:

```text
Design → Board Shape → Define Board Shape from Selected Objects
```

Altium utilizará los objetos seleccionados para definir el contorno físico.

<img src="../recursos/imgs/altium_board_shape_selected_objects.png" alt="Creación del Board Shape a partir de objetos seleccionados" width="700">

---

## Condición importante

El contorno debe ser coherente y cerrado.

Ejemplo correcto:

```text
┌─────────────┐
│             │
│             │
│             │
└─────────────┘
```

Ejemplo problemático:

```text
┌─────────────┐
│
│
│
└─────────────
```

---

# 38. Importar un contorno desde DXF o DWG

En algunos proyectos el diseño mecánico puede haberse realizado previamente en:

- AutoCAD;
- SolidWorks;
- Fusion;
- otro programa CAD.

Podemos importar el contorno mediante:

```text
File → Import → DXF/DWG
```

---

## Procedimiento general

1. Prepara el archivo mecánico.
2. Verifica sus unidades.
3. Asegúrate de que el contorno se encuentre cerrado.
4. Abre el `.PcbDoc`.
5. Selecciona:

```text
File → Import → DXF/DWG
```

6. Selecciona el archivo.
7. Configura unidades y escala.
8. Selecciona la capa de destino.
9. Importa los objetos.
10. Selecciona el contorno importado.
11. Utiliza:

```text
Design → Board Shape → Define Board Shape from Selected Objects
```

---

> [!WARNING]
> Uno de los errores más comunes al importar DXF/DWG es utilizar unidades incorrectas.

Una tarjeta de:

```text
50 mm × 50 mm
```

puede terminar siendo enorme o extremadamente pequeña si se confunden:

```text
mm
```

con:

```text
inch
```

o:

```text
mil
```

---

# 39. Configuración del origen de la PCB

Altium dispone de un origen absoluto y de un origen relativo configurable por el usuario.

Para la mayoría de proyectos es conveniente colocar el origen relativo en una esquina conocida del Board Shape.

Una opción habitual es:

```text
esquina inferior izquierda
```

---

## Establecer el origen

Selecciona:

```text
Edit → Origin → Set
```

Después:

1. acerca el cursor a la esquina deseada;
2. utiliza el snapping para posicionarte exactamente;
3. haz clic.

<img src="../recursos/imgs/altium_set_origin.png" alt="Configuración del origen relativo de la PCB" width="600">

El punto seleccionado pasará a representar:

```text
X = 0
Y = 0
```

para las coordenadas relativas.

---

## ¿Por qué establecer un origen?

Facilita:

- posicionamiento exacto;
- mediciones;
- dimensiones;
- exportaciones;
- comparación con dibujos mecánicos;
- colocación mediante coordenadas.

---

# 40. Configuración de unidades

En el PCB Editor podemos trabajar en:

```text
mm
```

o:

```text
mil
```

Para alternar rápidamente entre unidades puede utilizarse:

```text
Q
```

También puede utilizarse:

```text
View → Toggle Units
```

según el contexto.

---

## Recomendación

En diseños modernos suele resultar conveniente trabajar en:

```text
mm
```

especialmente cuando:

- el fabricante proporciona especificaciones métricas;
- los componentes tienen dimensiones métricas;
- el diseño mecánico se realizó en milímetros.

Sin embargo, algunos footprints antiguos y determinados estándares se encuentran definidos originalmente en mil.

---

> [!NOTE]
> Cambiar las unidades no modifica físicamente el tamaño de los objetos.

Simplemente cambia la manera en que Altium muestra y permite introducir las dimensiones.

---

# 41. Configuración del Grid

La cuadrícula determina los puntos preferentes sobre los que se colocan y desplazan los objetos.

Una cuadrícula adecuada facilita:

- alinear componentes;
- mantener coordenadas limpias;
- dibujar geometrías precisas;
- rutear de manera organizada.

---

## Configuración rápida

Con el `.PcbDoc` activo, presiona:

```text
G
```

para abrir las opciones rápidas relacionadas con el Snap Grid.

<img src="../recursos/imgs/altium_pcb_grid_popup.png" alt="Menú rápido del Snap Grid al presionar G" width="450">

---

## Valores grandes y pequeños

No existe un único Grid correcto para todas las operaciones.

Por ejemplo:

Para placement puede ser útil:

```text
1 mm
0.5 mm
```

Mientras que para ajustes pequeños podríamos utilizar:

```text
0.25 mm
0.1 mm
```

Los valores adecuados dependen del diseño.

---

## No utilizar grids extremadamente pequeños innecesariamente

Trabajar siempre con:

```text
0.001 mm
```

por ejemplo, puede producir coordenadas difíciles de manejar sin aportar ninguna ventaja real.

Es preferible utilizar una cuadrícula coherente con la precisión necesaria.

---

# 42. Grid Manager y cuadrículas personalizadas

Altium permite crear más de una cuadrícula.

Haz clic sobre un espacio vacío de la PCB y abre:

```text
Properties
```

Busca:

```text
Grid Manager
```

<img src="../recursos/imgs/altium_grid_manager.png" alt="Grid Manager de Altium Designer" width="650">

---

## Global Board Snap Grid

Es la cuadrícula general de la PCB.

Puede modificarse para establecer:

- tamaño;
- origen;
- comportamiento de snap.

---

## Cartesian Grid

Puede añadirse una cuadrícula cartesiana personalizada.

Es útil para zonas donde necesitamos otra separación.

Por ejemplo:

```text
PCB general → 1 mm

Zona de componentes pequeños → 0.25 mm
```

---

## Polar Grid

También pueden crearse:

```text
Polar Grids
```

Estas resultan útiles para diseños circulares.

Por ejemplo:

```text
LEDs distribuidos alrededor de un círculo
```

o:

```text
componentes alrededor de un encoder
```

---

## Prioridad

Si existen varias cuadrículas superpuestas, Altium utiliza un sistema de prioridad.

Esto permite que una cuadrícula local tenga preferencia sobre la cuadrícula global dentro de determinada región.

---

# 43. Panel View Configuration

Uno de los paneles más importantes del PCB Editor es:

```text
View Configuration
```

Puede abrirse mediante:

```text
View → Panels → View Configuration
```

o mediante:

```text
L
```

<img src="../recursos/imgs/altium_view_configuration.png" alt="Panel View Configuration del PCB Editor" width="400">

---

## Layers & Colors

Esta sección permite controlar:

- visibilidad de capas;
- colores;
- capas mecánicas;
- elementos del sistema.

Podemos ocultar una capa sin eliminarla.

---

## View Options

Permite controlar:

- visibilidad de objetos;
- transparencia;
- Single Layer Mode;
- masking;
- dimming.

---

## Single Layer Mode

Cuando una PCB tiene muchas capas puede resultar difícil identificar qué estamos editando.

El Single Layer Mode permite resaltar únicamente la capa activa.

Puede recorrerse mediante:

```text
Shift + S
```

Dependiendo de las preferencias configuradas, recorrerá distintos modos de visualización.

---

# 44. Capas principales de una PCB

Una PCB no está formada por una única superficie.

Altium representa las diferentes capas que intervienen en su fabricación.

---

## Top Layer

```text
Top Layer
```

Capa superior de cobre.

Puede contener:

- pistas;
- pads;
- polígonos;
- regiones de cobre.

---

## Bottom Layer

```text
Bottom Layer
```

Capa inferior de cobre.

En una PCB de dos capas normalmente podemos rutear utilizando tanto:

```text
Top Layer
```

como:

```text
Bottom Layer
```

---

## Internal Layers

En tarjetas multicapa pueden existir capas internas.

Por ejemplo:

```text
Top Layer
----------------
Dielectric
----------------
Mid Layer 1
----------------
Dielectric
----------------
Mid Layer 2
----------------
Dielectric
----------------
Bottom Layer
```

---

## Top Overlay

Corresponde generalmente a la serigrafía superior.

Puede contener:

- designadores;
- textos;
- logos;
- indicadores;
- contornos de componentes.

---

## Bottom Overlay

Equivalente de serigrafía para la cara inferior.

---

## Top Solder

Define información relacionada con la máscara de soldadura superior.

La máscara de soldadura es la capa protectora que normalmente vemos coloreada sobre la PCB.

---

## Bottom Solder

Máscara de soldadura inferior.

---

## Top Paste

Se utiliza principalmente para definir aperturas de pasta de soldadura para componentes SMD.

Es importante durante la fabricación de:

```text
stencils
```

---

## Bottom Paste

Equivalente para componentes SMD colocados sobre la cara inferior.

---

## Multi-Layer

No representa una capa física única de cobre.

Se utiliza para objetos que atraviesan varias capas, por ejemplo:

- pads through-hole;
- vías pasantes.

---

## Mechanical Layers

Se utilizan para información mecánica y documentación.

Su función se estudiará más adelante.

---

## Keep-Out Layer

Se utiliza para establecer restricciones espaciales sobre determinadas zonas.

---

# 45. Layer Stack Manager

La estructura física de la PCB se configura mediante:

```text
Design → Layer Stack Manager
```

<img src="../recursos/imgs/altium_layer_stack_manager.png" alt="Layer Stack Manager en Altium Designer" width="900">

El **Layer Stack Manager** permite definir la construcción vertical de la tarjeta.

---

## PCB de dos capas

Una PCB básica podría tener:

```text
Top Solder Mask
Top Copper
Dielectric
Bottom Copper
Bottom Solder Mask
```

Además de las capas de serigrafía correspondientes.

---

## PCB multicapa

Por ejemplo:

```text
Top Copper
Dielectric
Inner Copper 1
Dielectric
Inner Copper 2
Dielectric
Bottom Copper
```

---

## Información que puede configurarse

Dependiendo del proyecto, pueden definirse:

- cantidad de capas;
- nombre de capas;
- grosor de cobre;
- material dieléctrico;
- espesor;
- constante dieléctrica;
- máscaras;
- impedancia;
- tipos de vías.

---

> [!IMPORTANT]
> La estructura real debe coincidir con una construcción que el fabricante pueda producir.

En proyectos profesionales no debemos inventar arbitrariamente:

- espesores;
- materiales;
- stacks;
- valores de impedancia.

Debemos consultar las capacidades del fabricante.

---

# 46. Capas mecánicas y documentación

Las **Mechanical Layers** pueden utilizarse para representar información que no necesariamente forma parte del circuito eléctrico.

Ejemplos:

- dimensiones;
- contornos mecánicos;
- información de ensamblaje;
- cuerpos;
- rutas de fresado;
- datos de fabricación.

Pueden administrarse desde:

```text
View Configuration
```

---

## Nombres descriptivos

Cuando sea posible es mejor utilizar nombres claros.

Por ejemplo:

```text
Board Shape
Assembly
Dimensions
Route Tool Path
```

en lugar de depender únicamente de:

```text
Mechanical 1
Mechanical 2
Mechanical 3
```

---

# 47. Keepouts

Un **Keepout** define una zona o frontera que determinados objetos no deben atravesar.

Puede utilizarse para impedir:

- pistas;
- vías;
- componentes;
- cobre.

---

## Keep-Out Layer

Una opción consiste en utilizar objetos sobre:

```text
Keep-Out Layer
```

Por ejemplo:

```text
┌─────────────────────────┐
│                         │
│       ÁREA VÁLIDA       │
│                         │
└─────────────────────────┘
```

---

## Keepouts locales

También pueden existir restricciones específicas sobre determinadas capas.

Esto puede resultar útil, por ejemplo, debajo de:

- antenas;
- tornillos;
- sensores;
- conectores;
- mecanismos.

---

## Ejemplo: antena

Supongamos que utilizamos un módulo inalámbrico cuya antena requiere una zona sin cobre.

Podemos establecer:

```text
ANTENA
┌──────────────┐
│   KEEP OUT   │
│              │
└──────────────┘
```

para impedir que determinadas pistas o planos invadan esa zona.

---

> [!IMPORTANT]
> Las restricciones mecánicas de un componente deben obtenerse de su datasheet.

---

# 48. Colocación de componentes

Después de ejecutar el ECO, los componentes aparecerán en el PCB.

Normalmente todavía no estarán correctamente distribuidos.

El proceso de decidir dónde estará cada componente se denomina:

```text
Placement
```

<img src="../recursos/imgs/altium_initial_component_placement.png" alt="Componentes transferidos al PCB antes del placement" width="800">

---

## Objetivo del Placement

Un buen placement debe considerar:

- conectividad;
- longitud de pistas;
- alimentación;
- señales críticas;
- interferencias;
- accesibilidad;
- disipación;
- tamaño;
- fabricación;
- orientación;
- montaje.

---

## No comenzar a rutear inmediatamente

Un error muy común es:

```text
Transferir componentes
        ↓
Rutear inmediatamente
```

Es preferible:

```text
Transferir
      ↓
Definir Board Shape
      ↓
Configurar reglas
      ↓
Organizar componentes
      ↓
Revisar connections
      ↓
Rutear
```

---

# 49. Líneas de conexión o Ratsnest

Después de transferir el esquemático veremos líneas delgadas entre pads.

Estas líneas representan conexiones eléctricas todavía no ruteadas.

Son conocidas comúnmente como:

```text
Ratsnest
```

o:

```text
Connection Lines
```

---

## Ejemplo

```text
U1 o--------------------o R1
    \
     \
      \-----------------o C1
```

Estas líneas no son pistas físicas.

Simplemente indican:

> Estos pads deben conectarse.

---

## Durante el placement

Al mover un componente, las connection lines se actualizan.

Podemos utilizarlas para intentar reducir:

- cruces;
- distancias;
- rutas complicadas.

<img src="../recursos/imgs/altium_connection_lines.png" alt="Connection Lines utilizadas para organizar componentes" width="700">

---

# 50. Mover, rotar y cambiar componentes de cara

## Mover

Selecciona un componente y arrástralo.

También puedes utilizar las opciones disponibles en:

```text
Edit → Move
```

---

## Rotar

Mientras estás moviendo el componente:

```text
Space
```

lo rotará.

El incremento de rotación depende de la configuración, siendo normalmente:

```text
90°
```

---

## Rotar en sentido contrario

Durante determinados procesos interactivos:

```text
Shift + Space
```

permite rotar en dirección contraria.

---

## Cambiar de Top a Bottom

Mientras estás moviendo el componente presiona:

```text
L
```

Esto cambia el componente a la cara opuesta de la placa.

Por ejemplo:

```text
Top Layer
    ↓ L
Bottom Layer
```

Altium ajustará correctamente sus elementos asociados.

---

> [!WARNING]
> Para cambiar un componente entre caras utiliza `L`.

No utilices `X` o `Y` como sustituto, ya que reflejar geométricamente un objeto no es necesariamente lo mismo que mover correctamente un componente entre Top y Bottom.

---

# 51. Recomendaciones para el Placement

No existe una distribución universal correcta, pero existen buenas prácticas generales.

---

## Coloca primero los elementos mecánicamente restringidos

Por ejemplo:

- conectores;
- botones;
- LEDs visibles;
- USB;
- switches;
- sensores;
- potenciómetros;
- agujeros;
- displays.

Estos componentes suelen tener posiciones determinadas por la carcasa o interacción con el usuario.

---

## Después coloca los circuitos principales

Por ejemplo:

- microcontrolador;
- reguladores;
- drivers;
- amplificadores;
- transceptores.

---

## Capacitores de desacoplo

Los capacitores de desacoplo deben colocarse cerca de los pines de alimentación correspondientes.

Por ejemplo:

```text
VCC ── C ── GND
      ↑
   cerca del
      MCU
```

No deberían ubicarse arbitrariamente lejos únicamente porque exista espacio.

---

## Mantén bloques funcionales juntos

Por ejemplo:

```text
┌─────────────────┐
│    POWER        │
│                 │
│ Regulador       │
│ Capacitores     │
│ Inductor        │
└─────────────────┘

┌─────────────────┐
│ MICROCONTROLADOR│
│                 │
│ MCU             │
│ Crystal         │
│ Decoupling      │
└─────────────────┘
```

---

## Revisa la orientación

La orientación debe facilitar:

- ruteo;
- montaje;
- lectura;
- acceso.

---

# 52. Rooms

Después de transferir componentes pueden aparecer regiones asociadas a grupos de componentes denominadas:

```text
Rooms
```

Un Room es una zona de colocación que puede utilizarse para agrupar o restringir componentes.

<img src="../recursos/imgs/altium_room.png" alt="Room generado alrededor de componentes en Altium Designer" width="700">

---

## ¿Debo conservar los Rooms?

Depende del proyecto.

En diseños con:

- múltiples canales;
- bloques repetitivos;
- restricciones específicas;

pueden resultar muy útiles.

En proyectos pequeños pueden no ser necesarios.

---

## No confundir Room con Board Shape

Un Room:

```text
define una región lógica o de placement
```

El Board Shape:

```text
define el límite físico de la tarjeta
```

Son conceptos diferentes.

---

# 53. Introducción a las Design Rules

Las **Design Rules** son una de las características más importantes de Altium Designer.

En lugar de depender de que recordemos manualmente cada separación o dimensión, podemos indicarle al programa las restricciones que debe respetar.

Por ejemplo:

```text
Pistas mínimas = 0.20 mm
Clearance mínimo = 0.20 mm
Via = 0.60 / 0.30 mm
```

Altium utilizará estas reglas durante:

- ruteo;
- placement;
- comprobaciones;
- DRC.

---

## Las reglas deben venir del proceso de fabricación

Antes de definir valores consulta:

- fabricante;
- laboratorio;
- fresadora;
- proceso de producción.

Por ejemplo, una empresa puede especificar:

```text
Minimum Track Width
Minimum Clearance
Minimum Via Hole
Minimum Annular Ring
Minimum Copper to Edge
```

Debemos diseñar dentro de esas capacidades.

---

# 54. Rules Editor y Constraint Manager

En Altium Designer 26 existen **dos métodos diferentes** para administrar restricciones.

Cuál aparece depende de cómo fue creado el proyecto.

---

## Método 1: PCB Rules and Constraints Editor

Si el proyecto utiliza el sistema tradicional encontraremos:

```text
Design → Rules
```

Esto abre:

```text
PCB Rules and Constraints Editor
```

<img src="../recursos/imgs/altium_design_rules.png" alt="PCB Rules and Constraints Editor" width="850">

---

## Método 2: Constraint Manager

Si al crear el proyecto se habilitó:

```text
Constraint Management
```

encontraremos:

```text
Design → Constraint Manager
```

<img src="../recursos/imgs/altium_constraint_manager.png" alt="Constraint Manager de Altium Designer 26" width="850">

---

## ¿Cómo saber cuál utiliza nuestro proyecto?

Abre el PCB y revisa:

```text
Design
```

Si aparece:

```text
Constraint Manager
```

el proyecto utiliza el sistema nuevo.

Si aparece:

```text
Rules
```

utiliza el editor tradicional.

---

> [!IMPORTANT]
> Por esta razón, dos usuarios con Altium Designer 26 pueden abrir el menú `Design` y encontrar opciones diferentes.

No significa necesariamente que alguno tenga una instalación incorrecta.

---

## Constraint Manager

El Constraint Manager presenta una interfaz parecida a una tabla.

Puede contener vistas como:

```text
Clearances
Physical
Electrical
All Rules
```

Permite asociar restricciones directamente con:

- Nets;
- Net Classes;
- componentes;
- otros objetos.

---

## PCB Rules and Constraints Editor

El sistema tradicional utiliza reglas con:

```text
Scope
```

y:

```text
Constraints
```

Conceptualmente:

```text
¿A quién aplica?
        +
¿Qué debe cumplir?
```

---

# 55. Regla de Clearance

El **Clearance** define la separación mínima permitida entre objetos eléctricos.

Por ejemplo:

```text
Track       Track
──────      ──────
      ↔
   Clearance
```

---

## Ejemplo

Podríamos establecer:

```text
0.20 mm
```

Esto significa que los objetos sujetos a esa regla deben mantener la separación indicada.

---

## Sistema tradicional

Abre:

```text
Design → Rules
```

Busca la categoría relacionada con:

```text
Electrical → Clearance
```

Selecciona o crea una regla.

<img src="../recursos/imgs/altium_clearance_rule.png" alt="Regla Clearance en Altium Designer" width="800">

---

## Scope

Una regla general puede aplicarse a:

```text
All
```

Es decir:

```text
Todos contra todos
```

Después podemos crear reglas específicas para casos especiales.

---

# 56. Regla de Width

La regla:

```text
Routing → Width
```

controla el ancho de las pistas.

Normalmente permite especificar:

```text
Minimum
Preferred
Maximum
```

Por ejemplo:

```text
Minimum:   0.20 mm
Preferred: 0.30 mm
Maximum:   0.60 mm
```

<img src="../recursos/imgs/altium_width_rule.png" alt="Configuración de Routing Width" width="800">

---

## ¿Por qué existen tres valores?

Esto permite que durante el ruteo Altium conozca:

- el valor mínimo permitido;
- el valor preferido;
- el máximo permitido.

Podemos cambiar de ancho dentro de ese rango cuando sea necesario.

---

## No utilizar el mismo ancho para todo automáticamente

Una señal lógica puede requerir poca corriente.

Una alimentación de motor puede requerir mucha más.

Por ejemplo:

```text
GPIO     → pista normal
5V       → pista mayor
MOTOR+   → pista mucho mayor
```

El ancho debe determinarse en función de factores como:

- corriente;
- temperatura;
- espesor de cobre;
- longitud;
- caída de tensión;
- capacidad del fabricante.

---

# 57. Routing Via Style

La regla:

```text
Routing Via Style
```

determina las dimensiones de las vías que se colocan durante el ruteo.

Una vía posee, entre otras dimensiones:

```text
Diámetro exterior
Diámetro del agujero
```

Ejemplo:

```text
Via diameter: 0.60 mm
Hole size:    0.30 mm
```

<img src="../recursos/imgs/altium_via_style_rule.png" alt="Configuración de Routing Via Style" width="800">

---

## No elegir valores arbitrarios

El fabricante establece límites como:

```text
Minimum Drill Size
Minimum Via Diameter
Minimum Annular Ring
```

Por tanto, nuestra regla debe cumplir sus capacidades.

---

# 58. Crear reglas específicas para determinadas redes

Una gran ventaja de Altium es poder aplicar diferentes reglas a distintas redes.

Por ejemplo:

```text
Todas las señales:
0.25 mm

POWER:
0.60 mm

MOTOR:
1.00 mm
```

---

## Regla general

Podríamos tener:

```text
Width_Default
```

con Scope:

```text
All
```

---

## Regla específica

Después podemos crear:

```text
Width_Power
```

que solamente se aplique a determinadas redes.

Por ejemplo:

```text
InNet('5V')
```

o mediante una Net Class.

---

## Resultado

```text
GPIO → 0.25 mm
SDA  → 0.25 mm
SCL  → 0.25 mm

5V   → 0.60 mm
GND  → 0.60 mm
```

---

# 59. Prioridad de reglas

Cuando varias reglas del mismo tipo pueden afectar a un objeto, Altium debe decidir cuál utilizar.

Para ello existe la:

```text
Priority
```

---

## Ejemplo

Tenemos:

```text
Width_Default
Scope = All
```

y:

```text
Width_5V
Scope = InNet('5V')
```

La regla específica para `5V` debe tener prioridad adecuada sobre la regla general.

Conceptualmente:

```text
Regla específica
      ↓
tiene prioridad
      ↓
Regla general
```

---

> [!WARNING]
> Crear una regla específica no garantiza por sí solo que se utilice.

Siempre debemos comprobar:

- Scope;
- prioridad;
- si la regla está habilitada.

---

# 60. Net Classes

Una **Net Class** permite agrupar redes.

Por ejemplo:

```text
POWER
├── 12V
├── 5V
├── 3V3
└── GND
```

Después podemos crear una única regla para:

```text
POWER
```

en lugar de crear cuatro reglas independientes.

---

## Otros ejemplos

```text
MOTORS
├── MOTOR1+
├── MOTOR1-
├── MOTOR2+
└── MOTOR2-
```

o:

```text
COMMUNICATION
├── SDA
├── SCL
├── TX
└── RX
```

---

## Ventaja

Si posteriormente agregamos:

```text
1V8
```

a la clase:

```text
POWER
```

puede heredar las restricciones configuradas para esa clase.

---

# 61. Importación y exportación de reglas

Altium permite reutilizar reglas entre diferentes proyectos.

Esto resulta especialmente útil cuando un fabricante o laboratorio siempre utiliza los mismos límites.

---

## Exportar reglas

En un proyecto que utilice el editor tradicional:

1. Abre:

```text
Design → Rules
```

2. En el árbol de reglas haz clic derecho.
3. Selecciona:

```text
Export Rules
```

4. Selecciona las reglas.
5. Guarda el archivo.

El formato utilizado es:

```text
*.rul
```

Por ejemplo:

```text
Reglas_Fabricante.rul
```

---

## Importar reglas

1. Abre:

```text
Design → Rules
```

2. Haz clic derecho dentro del árbol de reglas.
3. Selecciona:

```text
Import Rules
```

4. Selecciona:

```text
Reglas_Fabricante.rul
```

5. Selecciona las reglas que deseas importar.
6. Confirma.

<img src="../recursos/imgs/altium_import_rules.png" alt="Importación de reglas RUL en Altium Designer" width="700">

---

> [!IMPORTANT]
> Después de importar reglas debemos revisarlas.

No debemos asumir que:

```text
archivo .rul importado = configuración correcta
```

Debemos comprobar:

- unidades;
- valores;
- Scope;
- prioridades;
- reglas duplicadas;
- fabricante para el que fueron creadas.

---

# 62. Comprobaciones antes de comenzar a rutear

Antes de colocar la primera pista comprueba:

### Board Shape

```text
✓ dimensiones correctas
```

### Origen

```text
✓ posición conocida
```

### Placement

```text
✓ componentes organizados
```

### Footprints

```text
✓ correctos
```

### Capas

```text
✓ stack configurado
```

### Rules

```text
✓ Clearance
✓ Width
✓ Via Style
```

### Connection Lines

```text
✓ corresponden con el esquemático
```

---

# 63. Interactive Routing

El proceso manual de crear pistas se denomina:

```text
Interactive Routing
```

Podemos iniciar una pista desde el menú:

```text
Route → Interactive Routing
```

También se utiliza habitualmente el atajo:

```text
Ctrl + W
```

según la configuración de atajos del entorno.

<img src="../recursos/imgs/altium_interactive_routing.png" alt="Interactive Routing de Altium Designer" width="800">

---

## Procedimiento

1. Activa la capa de cobre deseada.
2. Inicia `Interactive Routing`.
3. Haz clic sobre un pad.
4. Sigue una Connection Line.
5. Haz clic para fijar segmentos.
6. Continúa hasta el pad destino.
7. Haz clic sobre el pad final.
8. Finaliza el ruteo.

---

## Connection Line

Mientras ruteamos veremos la conexión pendiente.

Una vez completada correctamente:

```text
Connection Line desaparece
```

porque la Net ya dispone de una conexión física.

---

## No dibujar pistas con Line

Al igual que en el esquemático:

```text
objeto gráfico ≠ conexión eléctrica
```

Utiliza siempre las herramientas específicas de routing para realizar conexiones eléctricas.

---

# 64. Modos de esquina durante el ruteo

Mientras estamos ruteando podemos presionar:

```text
Shift + Space
```

para recorrer diferentes modos de esquina.

Entre ellos pueden encontrarse configuraciones como:

- 45°;
- 90°;
- arcos;
- Any Angle.

---

## Recomendación general

Para PCBs convencionales resulta común utilizar segmentos a:

```text
45°
```

Ejemplo:

```text
───────╲
        ╲
         ───────
```

en lugar de:

```text
───────┐
       │
       └───────
```

cuando sea posible y adecuado.

---

# 65. Modos de resolución de obstáculos

Durante el Interactive Routing Altium puede reaccionar de diferentes formas al encontrarse con objetos existentes.

Utiliza:

```text
Shift + R
```

para recorrer los modos disponibles.

---

## Walkaround Obstacles

Altium intenta rodear el obstáculo.

Conceptualmente:

```text
────────┐
        │ OBSTÁCULO
        └────────
```

---

## Push Obstacles

Intenta desplazar pistas existentes para crear espacio respetando las reglas.

---

## Ignore Obstacles

Permite ignorar determinados conflictos durante el ruteo.

> [!WARNING]
> `Ignore Obstacles` puede crear violaciones de reglas.

Debe utilizarse únicamente cuando sabemos exactamente lo que estamos haciendo.

---

## Recomendación

Para un usuario principiante es preferible trabajar principalmente con:

```text
Walkaround
```

y posteriormente experimentar con:

```text
Push
```

---

# 66. Cambiar el ancho de una pista

Durante el ruteo, el ancho utilizado debería provenir de nuestras reglas.

Altium puede trabajar con:

```text
Rule Minimum
Rule Preferred
Rule Maximum
User Choice
```

Durante Interactive Routing puede utilizarse:

```text
3
```

para recorrer determinados modos de selección de ancho.

---

## Modificar propiedades durante el ruteo

Presiona:

```text
Tab
```

Altium pausará temporalmente el proceso interactivo y mostrará las propiedades correspondientes.

Podremos revisar opciones como:

- Width;
- Via;
- layer;
- routing settings.

---

> [!TIP]
> `Tab` es uno de los atajos más importantes de Altium.

Durante muchas herramientas interactivas significa:

> Pausa la colocación y déjame configurar el objeto.

---

# 67. Cambiar de capa durante el ruteo

Una PCB de dos caras permite utilizar:

```text
Top Layer
```

y:

```text
Bottom Layer
```

Cuando una pista necesita cambiar de una cara a otra es necesario utilizar una **vía**.

---

## Cambio interactivo

Durante el ruteo podemos utilizar:

```text
Ctrl + Shift + rueda del ratón
```

para cambiar a otra capa de señal disponible.

Altium insertará automáticamente una vía utilizando la regla:

```text
Routing Via Style
```

<img src="../recursos/imgs/altium_routing_change_layer.png" alt="Cambio de capa mediante una vía durante Interactive Routing" width="700">

---

## Conceptualmente

```text
TOP
─────────────●
             │
             │ VIA
             │
             ●─────────────
BOTTOM
```

---

# 68. Vías

Una **Via** es una conexión metalizada que permite comunicar capas de cobre.

---

## Through Via

Una vía pasante atraviesa toda la PCB.

Por ejemplo:

```text
Top
 │
 ●
 │
Dielectric
 │
 ●
 │
Bottom
```

Es común en PCBs sencillas de dos capas.

---

## Partes de una vía

Una vía posee principalmente:

```text
Diameter
Hole Size
```

Ejemplo:

```text
Diameter = 0.60 mm
Hole     = 0.30 mm
```

---

## Colocar una vía manualmente

También puede utilizarse:

```text
Place → Via
```

Sin embargo, durante el ruteo suele ser más conveniente dejar que Altium inserte automáticamente la vía al cambiar de capa.

---

## No abusar de las vías

Cada vía:

- ocupa espacio;
- añade una perforación;
- aumenta complejidad;
- puede afectar señales;
- puede incrementar coste en procesos específicos.

No significa que debamos evitarlas completamente, sino utilizarlas de manera justificada.

---

# 69. Modificar pistas existentes

El diseño inicial rara vez será perfecto.

Altium permite modificar pistas posteriormente.

---

## Seleccionar segmento

Haz clic sobre un segmento.

El panel:

```text
Properties
```

mostrará información como:

- Net;
- Layer;
- Width;
- coordenadas.

---

## Mover un segmento

Puede arrastrarse interactivamente.

Altium intentará reajustar las conexiones según las opciones de routing configuradas.

---

## Eliminar una pista

Selecciona los segmentos deseados y utiliza:

```text
Delete
```

La Connection Line correspondiente reaparecerá si la Net queda nuevamente sin conexión.

---

## Backspace durante Interactive Routing

Mientras estás creando una pista:

```text
Backspace
```

permite eliminar el último segmento colocado.

Esto resulta muy útil cuando cometemos un error antes de terminar completamente la ruta.

---

# 70. Ruteo de alimentación

Las redes de alimentación requieren especial atención.

Por ejemplo:

```text
12V
5V
3V3
GND
MOTOR+
MOTOR-
```

No deberían tratarse automáticamente igual que una señal de baja corriente.

---

## Anchos diferentes

Podemos utilizar reglas específicas:

```text
Signals = 0.25 mm

Power = 0.50 mm

High Current = 1.00 mm
```

Estos valores son únicamente ilustrativos.

Los valores reales deben calcularse y verificarse según el proyecto.

---

## Tierra

GND puede rutearse mediante pistas, pero resulta muy común utilizar un:

```text
Polygon Pour
```

para crear una superficie extensa de cobre conectada a tierra.

---

# 71. Polygon Pour

Un **Polygon Pour** es una región de cobre que Altium rellena automáticamente respetando:

- Board Shape;
- clearances;
- pads;
- pistas;
- otras redes;
- keepouts;
- reglas.

Se utiliza frecuentemente para:

```text
GND
```

aunque también puede utilizarse para:

```text
VCC
Power
High Current
Shielding
```

---

## Diferencia respecto a una pista

Una pista representa:

```text
──────────────
```

Una región de cobre puede ocupar:

```text
████████████████████
████████████████████
████████████████████
```

---

# 72. Crear un plano de tierra

Para crear un polígono de tierra:

1. Activa la capa deseada.

Por ejemplo:

```text
Bottom Layer
```

2. Selecciona:

```text
Place → Polygon Pour
```

3. Antes o durante la colocación abre sus propiedades.
4. Asigna la Net:

```text
GND
```

5. Dibuja el perímetro.
6. Finaliza el polígono.
7. Realiza un Repour si es necesario.

<img src="../recursos/imgs/altium_polygon_pour_gnd.png" alt="Polygon Pour conectado a GND" width="800">

---

## Muy importante: asignar la Net

Un polígono de GND debe tener:

```text
Net = GND
```

No basta con dibujarlo sobre zonas cercanas a tierra.

---

## Clearance automático

Cuando el polígono se rellena, Altium respetará las reglas correspondientes.

Por ejemplo:

```text
████████   ← GND
████████
████        ─────  ← pista de otra Net
████████
```

dejará un espacio alrededor de objetos que pertenecen a otras redes.

---

# 73. Repour de polígonos

Después de modificar:

- pistas;
- componentes;
- vías;
- reglas;
- contorno;

un polígono puede requerir recalcularse.

A este proceso se le denomina:

```text
Repour
```

---

## Repour Selected

Para recalcular únicamente determinados polígonos:

```text
Tools → Polygon Pours → Repour Selected
```

---

## Repour All

Para recalcular todos:

```text
Tools → Polygon Pours → Repour All
```

<img src="../recursos/imgs/altium_repour_all.png" alt="Opciones de Repour de Polygon Pours" width="600">

---

## ¿Cuándo hacer Repour?

Es recomendable hacerlo después de cambios importantes y antes de ejecutar el DRC final.

Flujo:

```text
Modificar PCB
     ↓
Repour All
     ↓
DRC
```

---

# 74. Polygon Cutout

En ocasiones queremos que un polígono exista en prácticamente toda una zona excepto en una región determinada.

Podemos crear un:

```text
Polygon Pour Cutout
```

Mediante:

```text
Place → Polygon Pour Cutout
```

---

## Ejemplo

Plano general:

```text
██████████████████████
██████████████████████
██████████████████████
```

Con Cutout:

```text
██████████████████████
██████          ██████
██████  CUTOUT  ██████
██████          ██████
██████████████████████
```

---

## Procedimiento

1. Selecciona:

```text
Place → Polygon Pour Cutout
```

2. Dibuja la zona que debe quedar vacía.
3. Finaliza la forma.
4. Ejecuta:

```text
Repour
```

El cobre desaparecerá del área definida.

---

## Usos comunes

- zona de antena;
- aislamiento;
- requerimientos mecánicos;
- separación de circuitos;
- zonas sensibles.

---

# 75. Orden y prioridad de polígonos

Cuando existen varios polígonos sobre una misma capa, el orden en el que se rellenan puede ser importante.

Altium dispone de:

```text
Polygon Manager
```

mediante:

```text
Tools → Polygon Pours → Polygon Manager
```

<img src="../recursos/imgs/altium_polygon_manager.png" alt="Polygon Pour Manager" width="800">

---

## Desde el Polygon Manager podemos

- visualizar polígonos;
- renombrarlos;
- cambiar prioridades;
- hacer Repour;
- Shelve;
- modificar el Pour Order.

---

## Ejemplo

Supongamos:

```text
Polygon GND
```

y dentro:

```text
Polygon 5V
```

Puede ser necesario configurar el orden adecuado para que ambos se comporten correctamente.

---

# 76. Shelve Polygons

Durante el ruteo, los polígonos pueden dificultar visualmente el trabajo.

En lugar de eliminarlos podemos:

```text
Shelve
```

un Polygon Pour.

Esto lo retira temporalmente de determinadas operaciones y de la visualización correspondiente sin destruir su definición.

---

## Flujo práctico

```text
Polygon creado
     ↓
Shelve
     ↓
Rutear PCB
     ↓
Restore / Repour
     ↓
Revisar resultado
```

---

## ¿Por qué hacerlo?

Puede facilitar la visualización de:

- connection lines;
- pistas;
- vías;
- pads.

Especialmente en tarjetas densas.

---

# 77. Auto Route

Altium incluye un sistema de ruteo automático denominado:

```text
Situs Topological AutoRouter
```

Sus opciones pueden encontrarse en:

```text
Route → Auto Route
```

<img src="../recursos/imgs/altium_autoroute_menu.png" alt="Menú Auto Route de Altium Designer" width="600">

---

## Auto Route All

Puede utilizarse:

```text
Route → Auto Route → All
```

para intentar rutear automáticamente las conexiones pendientes.

Altium abrirá las opciones de estrategia del AutoRouter.

---

## Configuración

Entre los parámetros que pueden influir se encuentran:

- capas disponibles;
- direcciones preferidas;
- uso de vías;
- estrategias;
- pasadas de limpieza;
- reglas del diseño.

---

## No es una herramienta mágica

El AutoRouter no sustituye:

- buen placement;
- reglas correctas;
- conocimiento eléctrico;
- revisión manual.

Un mal placement producirá normalmente un mal resultado incluso utilizando un AutoRouter.

---

# 78. Recomendaciones antes de utilizar el AutoRouter

Antes de utilizar:

```text
Route → Auto Route
```

debemos tener correctamente configurados:

```text
Board Shape
Layer Stack
Placement
Clearance
Width
Via Style
Routing Layers
```

---

## Utilizar primero como herramienta de prueba

En proyectos educativos puede ser útil para:

- observar rutas posibles;
- comprobar si el placement tiene suficiente espacio;
- experimentar;
- comparar con el ruteo manual.

---

## No aceptar automáticamente el resultado

Después del AutoRoute debemos revisar:

- cantidad de vías;
- longitud de pistas;
- ángulos;
- rutas innecesarias;
- alimentación;
- retorno de corriente;
- zonas críticas;
- densidad;
- violaciones.

---

## Guardar antes de probar

Antes de ejecutar un AutoRoute puede ser conveniente guardar el proyecto.

De esta forma podemos comparar:

```text
PCB antes
```

contra:

```text
PCB después
```

y deshacer cambios si el resultado no resulta conveniente.

---

## Routing manual frente a AutoRoute

### Routing manual

Ventajas:

- mayor control;
- decisiones eléctricas conscientes;
- mejor tratamiento de señales críticas;
- mejor aprendizaje.

Desventajas:

- requiere más tiempo;
- requiere experiencia.

---

### AutoRoute

Ventajas:

- rapidez inicial;
- útil para experimentar;
- puede ayudar en determinadas redes o diseños.

Desventajas:

- no comprende completamente la intención eléctrica;
- depende enormemente del placement;
- puede producir rutas poco elegantes;
- puede utilizar demasiadas vías;
- siempre requiere revisión.

---

> [!TIP]
> Para aprender diseño PCB es recomendable realizar al menos los primeros proyectos mediante **Interactive Routing manual**.

Esto permite comprender realmente:

- cómo circulan las conexiones;
- por qué aparecen conflictos;
- cómo funcionan las capas;
- por qué se necesitan vías;
- cómo influyen las reglas.

---

# 79. Estado esperado al finalizar esta etapa

Al terminar esta segunda etapa deberíamos tener una PCB aproximadamente en el siguiente estado:

```text
PROYECTO
│
├── Esquemático validado
│
├── PCB sincronizada mediante ECO
│
├── Board Shape definido
│
├── Origen configurado
│
├── Unidades configuradas
│
├── Grid configurado
│
├── Layer Stack configurado
│
├── Componentes colocados
│
├── Reglas configuradas
│   │
│   ├── Clearance
│   ├── Width
│   └── Via Style
│
├── Pistas ruteadas
│
├── Vías colocadas
│
├── Polygon Pours
│
└── PCB físicamente definida
```

<img src="../recursos/imgs/altium_pcb_routed_complete.png" alt="PCB completamente colocada y ruteada antes de las verificaciones finales" width="900">

---

## Pero todavía no está lista para fabricar

Que todas las pistas estén conectadas **no significa que la PCB esté terminada**.

Todavía debemos comprobar:

```text
¿Existen conexiones pendientes?
```

```text
¿Existen violaciones de reglas?
```

```text
¿Los polígonos están actualizados?
```

```text
¿Los componentes caben físicamente?
```

```text
¿Los agujeros son correctos?
```

```text
¿La serigrafía invade pads?
```

```text
¿Los modelos 3D están orientados correctamente?
```

```text
¿El fabricante puede producir nuestras vías?
```

```text
¿El Board Shape es correcto?
```

```text
¿Las reglas utilizadas corresponden con el fabricante?
```

---

# Continuación

La siguiente etapa será la preparación y validación final del diseño.

El flujo será:

```text
PCB ruteada
     ↓
Revisión de conexiones
     ↓
DRC
     ↓
Corrección de violaciones
     ↓
Repour final
     ↓
DRC final
     ↓
Revisión 2D
     ↓
Revisión 3D
     ↓
Serigrafía
     ↓
Dimensiones y agujeros
     ↓
Fabrication Outputs
     ↓
Gerber / Gerber X2
     ↓
NC Drill
     ↓
Output Job
     ↓
Verificación de archivos
     ↓
ZIP de fabricación
```

Esta última etapa es especialmente importante, ya que determina si el diseño que observamos correctamente dentro de Altium puede convertirse realmente en una tarjeta física sin introducir errores durante la exportación.

# Parte 3: Validación, revisión y archivos de fabricación en Altium Designer

Una PCB completamente ruteada todavía **no está necesariamente lista para fabricarse**.

Antes de enviar los archivos a producción debemos comprobar que:

- no existan conexiones pendientes;
- todas las reglas de diseño se cumplan;
- los polígonos estén actualizados;
- las dimensiones sean correctas;
- los agujeros sean correctos;
- los componentes tengan orientación adecuada;
- la serigrafía sea legible;
- no exista serigrafía sobre pads;
- el contorno físico sea correcto;
- los archivos Gerber representen correctamente las capas;
- los archivos de perforación correspondan con los agujeros reales;
- todos los archivos utilicen el mismo origen y sistema de coordenadas.

El flujo general de esta última etapa será:

```text
PCB ruteada
     ↓
Guardar proyecto
     ↓
Repour All
     ↓
Comprobar conexiones pendientes
     ↓
PCB Health Check
     ↓
Batch DRC
     ↓
Corregir violaciones
     ↓
Preparar serigrafía
     ↓
Revisión 2D
     ↓
Revisión 3D
     ↓
Verificar agujeros y contorno
     ↓
Configurar OutJob
     ↓
Generar Gerber / Gerber X2
     ↓
Generar NC Drill
     ↓
Verificar archivos CAM
     ↓
Crear paquete de fabricación
     ↓
Enviar al fabricante
```

---

## Contenido

- [80. Preparación final antes de verificar la PCB](#80-preparación-final-antes-de-verificar-la-pcb)
- [81. Guardar y sincronizar el proyecto](#81-guardar-y-sincronizar-el-proyecto)
- [82. Actualizar todos los Polygon Pours](#82-actualizar-todos-los-polygon-pours)
- [83. Comprobar conexiones pendientes](#83-comprobar-conexiones-pendientes)
- [84. PCB Health Check](#84-pcb-health-check)
- [85. DRC Online y Batch DRC](#85-drc-online-y-batch-drc)
- [86. Configuración del Design Rule Checker](#86-configuración-del-design-rule-checker)
- [87. Ejecutar un Batch DRC](#87-ejecutar-un-batch-drc)
- [88. Interpretar las violaciones del DRC](#88-interpretar-las-violaciones-del-drc)
- [89. Clearance Constraint](#89-clearance-constraint)
- [90. Width Constraint](#90-width-constraint)
- [91. Short-Circuit Constraint](#91-short-circuit-constraint)
- [92. Un-Routed Net Constraint](#92-un-routed-net-constraint)
- [93. Via y Hole Size](#93-via-y-hole-size)
- [94. Silk to Solder Mask Clearance](#94-silk-to-solder-mask-clearance)
- [95. Board Outline Clearance](#95-board-outline-clearance)
- [96. Component Clearance](#96-component-clearance)
- [97. Cuándo puede ignorarse una violación](#97-cuándo-puede-ignorarse-una-violación)
- [98. Revisión y preparación de la serigrafía](#98-revisión-y-preparación-de-la-serigrafía)
- [99. Silkscreen Preparation](#99-silkscreen-preparation)
- [100. Designators y textos de la PCB](#100-designators-y-textos-de-la-pcb)
- [101. Marcas de polaridad y Pin 1](#101-marcas-de-polaridad-y-pin-1)
- [102. Revisión de agujeros](#102-revisión-de-agujeros)
- [103. Agujeros metalizados y no metalizados](#103-agujeros-metalizados-y-no-metalizados)
- [104. Mounting Holes](#104-mounting-holes)
- [105. Revisión del Board Shape](#105-revisión-del-board-shape)
- [106. Revisión 2D final](#106-revisión-2d-final)
- [107. Revisión 3D](#107-revisión-3d)
- [108. Navegación en 3D](#108-navegación-en-3d)
- [109. Qué revisar en la vista 3D](#109-qué-revisar-en-la-vista-3d)
- [110. Modelos 3D ausentes o incorrectos](#110-modelos-3d-ausentes-o-incorrectos)
- [111. DRC final después de los cambios](#111-drc-final-después-de-los-cambios)
- [112. Introducción a los archivos de fabricación](#112-introducción-a-los-archivos-de-fabricación)
- [113. Fabrication Outputs disponibles](#113-fabrication-outputs-disponibles)
- [114. Gerber RS-274X](#114-gerber-rs-274x)
- [115. Gerber X2](#115-gerber-x2)
- [116. Gerber convencional o Gerber X2](#116-gerber-convencional-o-gerber-x2)
- [117. Generar archivos directamente desde el PCB](#117-generar-archivos-directamente-desde-el-pcb)
- [118. Configuración de Gerber Setup](#118-configuración-de-gerber-setup)
- [119. Selección de capas Gerber](#119-selección-de-capas-gerber)
- [120. Extensiones habituales de archivos Gerber](#120-extensiones-habituales-de-archivos-gerber)
- [121. Board Outline en los archivos de fabricación](#121-board-outline-en-los-archivos-de-fabricación)
- [122. Generación de Gerber X2](#122-generación-de-gerber-x2)
- [123. Archivos de perforación NC Drill](#123-archivos-de-perforación-nc-drill)
- [124. Configuración de NC Drill Setup](#124-configuración-de-nc-drill-setup)
- [125. Plated y Non-Plated Drill Files](#125-plated-y-non-plated-drill-files)
- [126. Agujeros ranurados o Slots](#126-agujeros-ranurados-o-slots)
- [127. Importancia del origen y las coordenadas](#127-importancia-del-origen-y-las-coordenadas)
- [128. Crear un Output Job](#128-crear-un-output-job)
- [129. Estructura de un OutJob](#129-estructura-de-un-outjob)
- [130. Añadir Gerbers al OutJob](#130-añadir-gerbers-al-outjob)
- [131. Añadir NC Drill al OutJob](#131-añadir-nc-drill-al-outjob)
- [132. Añadir DRC al OutJob](#132-añadir-drc-al-outjob)
- [133. Folder Structure y ubicación de salidas](#133-folder-structure-y-ubicación-de-salidas)
- [134. Generar todas las salidas desde el OutJob](#134-generar-todas-las-salidas-desde-el-outjob)
- [135. Organización recomendada de archivos](#135-organización-recomendada-de-archivos)
- [136. Verificación de Gerbers con CAMtastic](#136-verificación-de-gerbers-con-camtastic)
- [137. Quick Load de los archivos de fabricación](#137-quick-load-de-los-archivos-de-fabricación)
- [138. Qué comprobar en el visor CAM](#138-qué-comprobar-en-el-visor-cam)
- [139. Verificación de archivos de perforación](#139-verificación-de-archivos-de-perforación)
- [140. Errores comunes antes de fabricar](#140-errores-comunes-antes-de-fabricar)
- [141. Crear el archivo ZIP para fabricación](#141-crear-el-archivo-zip-para-fabricación)
- [142. Qué archivos enviar al fabricante](#142-qué-archivos-enviar-al-fabricante)
- [143. Archivos opcionales para ensamblaje](#143-archivos-opcionales-para-ensamblaje)
- [144. Checklist final de fabricación](#144-checklist-final-de-fabricación)
- [145. Flujo completo de Altium Designer](#145-flujo-completo-de-altium-designer)

---

# 80. Preparación final antes de verificar la PCB

Antes de ejecutar el DRC final conviene realizar una serie de operaciones básicas.

No debemos utilizar el DRC como sustituto de una revisión visual.

El orden recomendado es:

```text
Guardar
   ↓
Repour All
   ↓
Revisar conexiones
   ↓
Revisar placement
   ↓
Revisar serigrafía
   ↓
DRC
```

---

# 81. Guardar y sincronizar el proyecto

Antes de iniciar las verificaciones finales:

1. Guarda el `.PcbDoc`.
2. Guarda los `.SchDoc`.
3. Guarda el `.PrjPcb`.
4. Comprueba que esquemático y PCB continúan sincronizados.

Si realizaste modificaciones recientes en el esquemático, utiliza:

```text
Design → Update PCB Document
```

y revisa el ECO.

El objetivo es evitar validar una PCB que ya no corresponda con el esquemático actual.

---

## Recomendación antes de fabricar

Puedes realizar una última actualización:

```text
Schematic
    ↓
Design → Update PCB Document
    ↓
Validate Changes
    ↓
Execute Changes
```

Si el ECO no propone cambios inesperados, es una buena señal de que ambos documentos están sincronizados.

---

# 82. Actualizar todos los Polygon Pours

Antes del DRC debemos recalcular todos los polígonos.

Utiliza:

```text
Tools → Polygon Pours → Repour All
```

<img src="../recursos/imgs/altium_final_repour_all.png" alt="Repour All antes del DRC final" width="650">

Esto recalculará todos los planos teniendo en cuenta:

- tracks;
- pads;
- vias;
- keepouts;
- clearances;
- Board Shape;
- nuevas reglas.

---

## Por qué es importante

Supongamos que movimos una pista:

```text
ANTES

████████████
████ ───────
████████████
```

pero el polígono todavía conserva su geometría anterior.

Después del Repour:

```text
Polygon
   ↓
se recalcula
   ↓
respeta posición actual
```

---

> [!IMPORTANT]
> Ejecutar el DRC con polígonos desactualizados puede dificultar la revisión del diseño.

---

# 83. Comprobar conexiones pendientes

Antes del DRC revisa visualmente si todavía existen:

```text
Connection Lines
```

o líneas del Ratsnest.

Si una línea continúa visible significa generalmente que existe una conexión eléctrica pendiente.

---

## Una PCB terminada debería aproximarse a:

```text
Unrouted connections = 0
```

salvo que el diseño tenga alguna condición intencional especial.

---

## No confundir plano con conexión

Cuando utilizamos un Polygon Pour de `GND`, una conexión puede desaparecer después del Repour porque el pad quedó conectado al plano.

Por eso siempre debemos hacer:

```text
Repour All
```

antes de decidir si una red continúa sin conectar.

---

# 84. PCB Health Check

Altium Designer 26 dispone también de una herramienta llamada:

```text
PCB Health Check
```

Su propósito es detectar determinados problemas internos del documento PCB que no necesariamente constituyen una violación convencional del DRC.

---

## Acceso

Con el `.PcbDoc` abierto:

1. Haz clic sobre un espacio vacío.
2. Abre:

```text
View → Panels → Properties
```

3. Busca la pestaña:

```text
Health Check
```

<img src="../recursos/imgs/altium_pcb_health_check.png" alt="PCB Health Check dentro del panel Properties" width="600">

---

## Ejecutar las comprobaciones

Dentro de la sección Health Check:

1. Revisa las categorías disponibles.
2. Activa las comprobaciones que deseas ejecutar.
3. Selecciona:

```text
Check All
```

---

## Diferencia entre Health Check y DRC

No son equivalentes.

### DRC

Comprueba principalmente el cumplimiento de:

```text
Design Rules
```

### Health Check

Busca posibles problemas estructurales o internos del documento que pueden provocar dificultades posteriormente.

Por tanto:

```text
Health Check ≠ DRC
```

y resulta conveniente utilizar ambos.

---

# 85. DRC Online y Batch DRC

Altium puede comprobar las reglas de dos maneras principales.

## Online DRC

Se ejecuta mientras trabajamos.

Puede detectar inmediatamente problemas como:

- Clearance;
- Width;
- rutas conflictivas.

Es muy útil durante el diseño.

---

## Batch DRC

Analiza la PCB completa cuando lo solicitamos.

Esta es la comprobación que debemos ejecutar siempre antes de generar los archivos finales de fabricación.

---

## Flujo recomendado

```text
Durante el diseño
      ↓
Online DRC

Antes de fabricar
      ↓
Batch DRC
```

---

> [!IMPORTANT]
> Que no veamos marcadores rojos mientras diseñamos no significa que la PCB haya superado una comprobación completa.

Siempre ejecuta un Batch DRC final.

---

# 86. Configuración del Design Rule Checker

Con el `.PcbDoc` activo abre:

```text
Tools → Design Rule Check
```

Aparecerá:

```text
Design Rule Checker
```

<img src="../recursos/imgs/altium_design_rule_checker.png" alt="Ventana Design Rule Checker de Altium Designer" width="900">

---

## Rules to Check

Dentro de la ventana selecciona:

```text
Rules to Check
```

Aquí encontraremos los diferentes tipos de reglas.

Cada tipo puede disponer de columnas para:

```text
Online
Batch
```

---

## Online

Determina si el tipo de regla será comprobado mientras trabajamos.

---

## Batch

Determina si será incluido cuando ejecutemos:

```text
Run Design Rule Check
```

---

## Recomendación

Antes de fabricar, revisa que todas las reglas importantes estén habilitadas para:

```text
Batch
```

No desactives reglas solamente para conseguir un reporte limpio.

---

# 87. Ejecutar un Batch DRC

Una vez configuradas las reglas:

1. Abre:

```text
Tools → Design Rule Check
```

2. Revisa:

```text
Rules to Check
```

3. Revisa:

```text
Report Options
```

4. Si deseas conservar un reporte, activa:

```text
Create Report File
```

5. Ejecuta:

```text
Run Design Rule Check
```

<img src="../recursos/imgs/altium_run_drc.png" alt="Botón Run Design Rule Check ejecutando la verificación completa" width="800">

---

## Resultado

Después de finalizar aparecerán las violaciones detectadas.

Pueden visualizarse desde:

```text
Messages
```

o:

```text
PCB Rules And Violations
```

---

## Panel Messages

Abrir mediante:

```text
View → Panels → Messages
```

---

## PCB Rules And Violations

Abrir mediante:

```text
View → Panels → PCB Rules And Violations
```

<img src="../recursos/imgs/altium_pcb_rules_violations.png" alt="Panel PCB Rules And Violations mostrando errores" width="500">

---

# 88. Interpretar las violaciones del DRC

Cuando aparece una violación debemos determinar:

```text
¿Qué regla se incumplió?
```

```text
¿Qué objetos están involucrados?
```

```text
¿Cuál era el valor requerido?
```

```text
¿Cuál es el valor real?
```

---

## Localizar una violación

Desde `Messages` o `PCB Rules And Violations`:

1. selecciona la violación;
2. haz doble clic;
3. Altium centrará la vista sobre el problema.

Esto facilita pasar de:

```text
Clearance Constraint violation
```

a:

```text
estas dos pistas concretas están demasiado cerca
```

---

## Información típica

Una violación puede mostrar algo similar a:

```text
Actual Clearance: 0.15 mm

Required Clearance: 0.20 mm
```

Esto significa que debemos:

- separar los objetos;
- modificar la geometría;
- o comprobar si la regla aplicada es realmente correcta.

---

# 89. Clearance Constraint

Una de las violaciones más comunes es:

```text
Clearance Constraint
```

Indica que dos objetos están más cerca de lo permitido.

Por ejemplo:

```text
Track A    Track B
──────     ──────
       ↔
    0.15 mm
```

cuando la regla exige:

```text
0.20 mm
```

---

## Solución

Puedes:

- mover una pista;
- rerutear;
- mover una vía;
- modificar placement;
- revisar el Scope de la regla.

---

> [!WARNING]
> No reduzcas automáticamente el Clearance hasta que desaparezca el error.

La separación mínima debe corresponder con la capacidad del fabricante y los requisitos eléctricos del diseño.

---

# 90. Width Constraint

Una violación:

```text
Width Constraint
```

indica que una pista utiliza una anchura fuera de los límites permitidos.

Por ejemplo:

```text
Regla:
Minimum = 0.20 mm

Pista:
Width = 0.15 mm
```

---

## Corregir

Selecciona el segmento y abre:

```text
Properties
```

Revisa:

```text
Width
```

También puedes rerutear la conexión utilizando el ancho correcto.

---

# 91. Short-Circuit Constraint

Una violación:

```text
Short-Circuit Constraint
```

es especialmente importante.

Significa que objetos pertenecientes a redes diferentes se encuentran eléctricamente unidos.

Ejemplo:

```text
5V
───────┐
       ├──────
───────┘
GND
```

Esto podría representar un cortocircuito real.

---

## Procedimiento

No ignores esta violación.

1. Localiza el punto exacto.
2. Identifica ambas Nets.
3. Comprueba el esquemático.
4. Revisa si el contacto es accidental.
5. Corrige pistas, pads, polígonos o footprint según corresponda.

---

# 92. Un-Routed Net Constraint

Una violación:

```text
Un-Routed Net Constraint
```

indica que existe una conexión que todavía no cuenta con una ruta física completa.

---

## Causas comunes

- pista incompleta;
- vía que no continúa;
- plano sin actualizar;
- pad aislado;
- cambio en el esquemático;
- polígono sin conexión.

---

## Procedimiento

Primero ejecuta:

```text
Tools → Polygon Pours → Repour All
```

Luego vuelve a ejecutar el DRC.

Si continúa apareciendo, localiza la conexión.

---

# 93. Via y Hole Size

El DRC también puede detectar problemas relacionados con:

```text
Routing Via Style
```

```text
Hole Size
```

Por ejemplo:

```text
Via Diameter = 0.50 mm
Hole = 0.40 mm
```

puede dejar un anillo de cobre insuficiente dependiendo de las reglas.

---

## Elementos relacionados

Una vía posee:

```text
┌───────────────┐
│     cobre     │
│    ┌─────┐    │
│    │hole │    │
│    └─────┘    │
│     cobre     │
└───────────────┘
```

La diferencia entre el diámetro exterior y el agujero determina el área de cobre disponible alrededor del taladro.

---

# 94. Silk to Solder Mask Clearance

Esta regla comprueba la separación entre:

```text
Silkscreen
```

y:

```text
Solder Mask Openings
```

Por ejemplo, un designador como:

```text
R14
```

puede estar colocado encima de un pad.

Esto puede provocar que durante la fabricación parte del texto sea eliminado.

---

## Solución

Mover el texto o utilizar:

```text
Tools → Silkscreen Preparation
```

que estudiaremos posteriormente.

---

# 95. Board Outline Clearance

Esta regla controla la separación entre objetos y el borde físico de la PCB.

Puede detectar elementos demasiado cercanos a:

```text
Board Shape
```

---

## Ejemplo

```text
BORDE
│
│  ← 0.10 mm → VIA
│
```

cuando la regla requiere:

```text
0.30 mm
```

---

## Por qué importa

Durante el fresado o separación del panel existe una tolerancia mecánica.

El cobre demasiado cerca del borde puede:

- quedar expuesto;
- dañarse;
- cortarse;
- causar problemas de fabricación.

---

# 96. Component Clearance

La regla:

```text
Component Clearance
```

puede detectar componentes demasiado cercanos físicamente.

Cuando existen modelos 3D adecuados, Altium puede tenerlos en cuenta para realizar comprobaciones tridimensionales.

---

## Ejemplo

Dos conectores pueden parecer separados correctamente en 2D:

```text
[CON1]     [CON2]
```

pero sus cuerpos físicos pueden interferir:

```text
      \___/
      choque
```

Por eso la revisión 3D resulta importante.

---

# 97. Cuándo puede ignorarse una violación

No todas las advertencias representan necesariamente un error de diseño.

Sin embargo, debemos utilizar la siguiente lógica:

```text
Violación
   ↓
Comprender causa
   ↓
Comprobar intención
   ↓
Comprobar datasheet
   ↓
Comprobar fabricante
   ↓
Solo entonces decidir
```

---

## Nunca utilizar

```text
Hay error
   ↓
No sé qué significa
   ↓
Lo ignoro
```

---

## Si una excepción es intencional

Puede:

- ajustarse el Scope de la regla;
- crearse una regla específica;
- utilizarse el sistema de excepciones o waivers disponible;
- documentarse la razón.

Lo importante es que la excepción sea consciente y justificable.

---

# 98. Revisión y preparación de la serigrafía

La serigrafía corresponde principalmente a:

```text
Top Overlay
```

y:

```text
Bottom Overlay
```

Puede contener:

- designadores;
- nombres;
- polaridades;
- logos;
- números de versión;
- indicadores;
- texto de montaje.

---

## Una buena serigrafía debe ser legible

Debemos evitar:

```text
R1 colocado encima del pad
```

```text
texto fuera de la tarjeta
```

```text
texto debajo de otro componente
```

```text
designadores superpuestos
```

```text
texto demasiado pequeño
```

---

# 99. Silkscreen Preparation

Altium Designer incluye una herramienta específica para ayudar a preparar la serigrafía.

Utiliza:

```text
Tools → Silkscreen Preparation
```

<img src="../recursos/imgs/altium_silkscreen_preparation.png" alt="Ventana Silkscreen Preparation en Altium Designer" width="750">

---

## All / Selected

Permite decidir si la herramienta trabajará con:

```text
All
```

todos los objetos,

o:

```text
Selected
```

únicamente los objetos seleccionados.

---

## Overlay Layers

Permite seleccionar:

```text
Top Overlay
Bottom Overlay
```

según corresponda.

---

## Use Design Rules

Si está habilitado, Altium puede utilizar las reglas relacionadas con:

```text
Silk to Solder Mask Clearance
```

y:

```text
Board Outline Clearance
```

---

## Move Text

Permite intentar mover automáticamente textos y designadores que interfieren con elementos prohibidos.

---

## Clip

Algunos elementos gráficos pueden recortarse para respetar el Clearance.

---

## Delete Silkscreen Outside Board Shape

Permite eliminar objetos de serigrafía que hayan quedado completamente fuera del contorno de la PCB.

---

> [!WARNING]
> No ejecutes esta herramienta y aceptes ciegamente el resultado.

Después debes inspeccionar manualmente:

- designadores;
- polaridades;
- logos;
- textos importantes.

---

# 100. Designators y textos de la PCB

Los designadores permiten identificar físicamente los componentes.

Por ejemplo:

```text
R1
C5
U2
D3
J1
```

---

## Qué debería poder hacer una persona

Al observar la PCB debería ser posible relacionar:

```text
R14
```

con:

```text
R14 del esquemático
```

sin tener que adivinar.

---

## Revisión recomendada

Comprueba que:

- el texto sea legible;
- el tamaño sea fabricable;
- no esté sobre un pad;
- no esté debajo de un componente si necesitas verlo;
- no invada el borde;
- no se superponga con otro texto.

---

# 101. Marcas de polaridad y Pin 1

Algunos componentes requieren orientación específica.

Ejemplos:

- LEDs;
- diodos;
- capacitores electrolíticos;
- circuitos integrados;
- conectores;
- transistores.

---

## Es recomendable incluir indicadores claros

Por ejemplo:

```text
+
```

para un capacitor polarizado.

O:

```text
●
```

para indicar:

```text
Pin 1
```

en determinados circuitos integrados.

---

> [!IMPORTANT]
> La orientación visible en serigrafía debe corresponder con la orientación real del footprint y con el datasheet.

---

# 102. Revisión de agujeros

Antes de generar NC Drill debemos comprobar todos los agujeros.

Entre ellos pueden existir:

- agujeros de pads through-hole;
- vías;
- mounting holes;
- slots;
- agujeros mecánicos.

---

## Para cada agujero revisa

```text
Hole Size
```

```text
Plated / Non-Plated
```

```text
Position X/Y
```

```text
Shape
```

---

# 103. Agujeros metalizados y no metalizados

Un agujero puede ser:

```text
Plated
```

o:

```text
Non-Plated
```

---

## Plated Through Hole

Posee metalización en las paredes internas.

Se utiliza normalmente para:

- componentes THT;
- vias;
- conexiones eléctricas entre capas.

---

## Non-Plated Through Hole

No tiene metalización interior.

Se utiliza frecuentemente para:

- tornillos;
- postes;
- guías;
- sujeción mecánica.

---

## Visualmente

```text
PTH
Cobre
  │
  ▼
 ┌───┐
 │ ○ │ ← pared metalizada
 └───┘
```

```text
NPTH
 ┌───┐
 │ ○ │ ← agujero mecánico
 └───┘
```

---

# 104. Mounting Holes

Un agujero de montaje puede crearse mediante un Pad configurado adecuadamente o mediante un componente específico de mounting hole.

Para un agujero puramente mecánico normalmente debemos comprobar:

```text
Plated = Off
```

cuando realmente deseamos un agujero no metalizado.

---

## Comprobar diámetro real

No basta con saber el diámetro del tornillo.

Debemos considerar:

- holgura;
- tolerancia;
- cabeza;
- washer;
- soporte;
- especificaciones mecánicas.

---

## Ejemplo

Un tornillo:

```text
M3
```

no implica automáticamente:

```text
Hole = 3.00 mm
```

El diámetro requerido dependerá de la tolerancia mecánica deseada.

---

# 105. Revisión del Board Shape

Antes de fabricar revisa nuevamente:

```text
Board Shape
```

---

## Comprueba

- ancho total;
- alto total;
- esquinas;
- recortes;
- posiciones;
- radios;
- agujeros;
- relación con la carcasa.

---

## Dimensiones

Utiliza herramientas de medición cuando sea necesario.

La PCB debe coincidir con el diseño mecánico real.

---

> [!CAUTION]
> Un PCB eléctricamente perfecto puede ser completamente inútil si no entra en la carcasa.

---

# 106. Revisión 2D final

Presiona:

```text
2
```

para entrar en:

```text
2D Layout Mode
```

Realiza una inspección capa por capa.

---

## Top Layer

Comprueba:

- pistas;
- pads;
- polígonos;
- vias;
- clearances.

---

## Bottom Layer

Realiza la misma comprobación.

---

## Top Overlay

Comprueba serigrafía.

---

## Bottom Overlay

Comprueba orientación de textos si existe ensamblaje por la cara inferior.

---

## Solder Mask

Comprueba aperturas alrededor de pads.

---

## Mechanical Layers

Comprueba información mecánica relevante.

---

## Single Layer Mode

Puedes utilizar:

```text
Shift + S
```

para recorrer diferentes modos de visualización de una sola capa.

Esto ayuda enormemente a analizar diseños complejos.

---

# 107. Revisión 3D

Después de la revisión 2D cambia a:

```text
3
```

o utiliza:

```text
View → 3D Layout Mode
```

<img src="../recursos/imgs/altium_final_3d_view.png" alt="Vista 3D final de la PCB" width="900">

La PCB será representada tridimensionalmente utilizando:

- Board Shape;
- Layer Stack;
- pads;
- holes;
- modelos 3D;
- componentes.

---

# 108. Navegación en 3D

Algunas operaciones útiles son:

## Cambiar a 3D

```text
3
```

## Volver a 2D

```text
2
```

---

## Rotar

Mantén:

```text
Shift
```

y aparecerá la esfera de orientación.

Después utiliza:

```text
Shift + Right Drag
```

para rotar la vista.

---

## Desplazar

Puedes utilizar:

```text
Right Drag
```

---

## Zoom

Entre las opciones disponibles se encuentran:

```text
Ctrl + Mouse Wheel
```

o:

```text
Page Up
Page Down
```

---

## Vista superior

Puede utilizarse:

```text
0
```

en el teclado principal para regresar a una vista superior.

---

## View Configuration

El panel:

```text
View → Panels → View Configuration
```

o:

```text
L
```

permite configurar la visualización 3D.

---

# 109. Qué revisar en la vista 3D

La vista 3D no debe utilizarse únicamente para obtener una imagen bonita.

Tiene una función de revisión.

---

## Orientación

Comprueba:

- conectores;
- ICs;
- LEDs;
- diodos;
- capacitores;
- switches.

---

## Alturas

Comprueba que componentes altos no interfieran con:

- carcasa;
- tapa;
- otras PCB;
- mecanismos.

---

## Conectores

Comprueba que:

- estén mirando hacia el exterior correcto;
- sean accesibles;
- no estén bloqueados.

---

## Agujeros

Comprueba la relación entre agujeros y componentes.

---

## Componentes inferiores

Gira la PCB y comprueba:

```text
Bottom Side
```

si existen componentes en esa cara.

---

# 110. Modelos 3D ausentes o incorrectos

Si un componente aparece como:

```text
footprint sin cuerpo
```

probablemente no tenga modelo 3D asociado.

Esto no significa necesariamente que el footprint eléctrico sea incorrecto.

Sin embargo, dificulta la comprobación mecánica.

---

## Casos posibles

```text
Symbol ✓
Footprint ✓
3D Model ✗
```

La PCB puede ser eléctricamente válida.

---

## Otro caso

```text
Symbol ✓
Footprint ✓
3D Model ✓
```

pero el modelo aparece:

- desplazado;
- rotado;
- invertido;
- flotando.

Entonces debemos corregir su posición dentro del footprint.

---

# 111. DRC final después de los cambios

Después de corregir:

- serigrafía;
- placement;
- agujeros;
- polígonos;
- pistas;

debemos ejecutar nuevamente:

```text
Tools → Polygon Pours → Repour All
```

y posteriormente:

```text
Tools → Design Rule Check
```

seguido de:

```text
Run Design Rule Check
```

---

## Estado deseado

Idealmente:

```text
DRC Violations = 0
```

Si existen excepciones deliberadas deben estar:

- entendidas;
- justificadas;
- documentadas.

---

# 112. Introducción a los archivos de fabricación

Altium no envía el `.PcbDoc` directamente a todos los fabricantes.

Tradicionalmente se generan archivos estandarizados que describen:

- cobre;
- máscara;
- serigrafía;
- contorno;
- perforaciones.

Los más comunes son:

```text
Gerber
```

y:

```text
NC Drill
```

---

## Conceptualmente

```text
Altium PCB
    ↓
Fabrication Outputs
    ↓
Gerber + Drill
    ↓
CAM del fabricante
    ↓
PCB física
```

---

# 113. Fabrication Outputs disponibles

Altium puede generar diferentes formatos.

Entre ellos:

```text
Gerber
Gerber X2
NC Drill
ODB++
IPC-2581
Board Stack Report
```

Para una introducción general a fabricación nos centraremos principalmente en:

```text
Gerber
```

y:

```text
NC Drill
```

ya que son ampliamente utilizados.

---

# 114. Gerber RS-274X

El formato Gerber tradicional utilizado actualmente suele referirse a:

```text
RS-274X
```

Cada archivo representa determinada información de fabricación.

Por ejemplo:

```text
Top Copper
```

se almacena en un archivo.

```text
Bottom Copper
```

en otro.

```text
Top Solder Mask
```

en otro.

---

## Conceptualmente

```text
PCB
│
├── Top Copper       → archivo Gerber
├── Bottom Copper    → archivo Gerber
├── Top Mask         → archivo Gerber
├── Bottom Mask      → archivo Gerber
├── Top Silkscreen   → archivo Gerber
├── Bottom Silkscreen→ archivo Gerber
└── Board Outline    → archivo Gerber
```

---

# 115. Gerber X2

Gerber X2 es una evolución de Gerber que incorpora información adicional sobre la función de los datos.

Esto ayuda a reducir ambigüedades.

Por ejemplo, un archivo puede incluir información que permite identificar que corresponde a:

```text
Top Copper
```

en lugar de depender únicamente del nombre del archivo.

---

## Ventaja conceptual

Gerber clásico:

```text
archivo.gtl
```

El fabricante interpreta:

```text
.gtl = Top Layer
```

Gerber X2:

```text
archivo
+
atributos internos
+
información funcional
```

---

# 116. Gerber convencional o Gerber X2

La respuesta depende principalmente del fabricante.

Utiliza:

```text
Gerber X2
```

si el fabricante lo admite y lo solicita o recomienda.

Utiliza:

```text
Gerber RS-274X
```

cuando necesites máxima compatibilidad con procesos tradicionales.

---

> [!IMPORTANT]
> Consulta siempre la documentación del fabricante.

No generes un formato simplemente porque sea más moderno.

---

## NC Drill sigue siendo importante

Aunque Gerber X2 incorpora más información de fabricación, es recomendable generar también los archivos:

```text
NC Drill
```

salvo que el fabricante especifique expresamente otro flujo.

---

# 117. Generar archivos directamente desde el PCB

Altium permite generar Gerbers directamente sin utilizar un OutJob.

Con el `.PcbDoc` abierto:

```text
File → Fabrication Outputs → Gerber Files
```

Para Gerber X2:

```text
File → Fabrication Outputs → Gerber X2 Files
```

<img src="../recursos/imgs/altium_file_fabrication_outputs.png" alt="Menú File Fabrication Outputs" width="700">

---

## Ventaja

Es rápido.

---

## Desventaja

Para proyectos que se generarán repetidamente es más recomendable utilizar:

```text
OutJob
```

porque mantiene las configuraciones de salida centralizadas y reproducibles.

---

# 118. Configuración de Gerber Setup

Al seleccionar:

```text
File → Fabrication Outputs → Gerber Files
```

aparecerá:

```text
Gerber Setup
```

<img src="../recursos/imgs/altium_gerber_setup.png" alt="Ventana Gerber Setup en Altium Designer" width="900">

---

## Units

Selecciona:

```text
Millimeters
```

o:

```text
Inches
```

según los requisitos de fabricación.

Si trabajaste todo el proyecto en sistema métrico resulta lógico utilizar:

```text
Millimeters
```

si el fabricante lo admite.

---

## Decimal / Precision

Determina la resolución utilizada en las coordenadas.

Una mayor precisión permite representar coordenadas con más resolución.

---

> [!IMPORTANT]
> La máxima precisión posible no siempre debe seleccionarse arbitrariamente.

Comprueba qué formato acepta tu fabricante.

---

## Outputs

Altium permite utilizar estilos de nomenclatura como:

```text
*.gbr
```

para todas las capas,

o extensiones específicas:

```text
.gtl
.gbl
.gto
...
```

---

# 119. Selección de capas Gerber

Dentro de:

```text
Layers to Plot
```

debemos seleccionar las capas que realmente necesita el fabricante.

---

## Para una PCB de dos capas

Normalmente debemos considerar:

```text
Top Layer
Bottom Layer
Top Solder
Bottom Solder
Top Overlay
Bottom Overlay
Board Outline
```

---

## Paste Mask

También podemos encontrar:

```text
Top Paste
Bottom Paste
```

Estas capas se utilizan principalmente para fabricar:

```text
Stencil
```

para aplicación de pasta de soldadura en ensamblaje SMD.

Para fabricar únicamente la PCB desnuda normalmente no son esenciales, aunque algunos paquetes de fabricación las incluyen.

---

## Si no existen componentes en Bottom

Podemos tener:

```text
Bottom Overlay
```

vacío.

No siempre es necesario generar una capa vacía.

---

## PCB multicapa

También deben incluirse todas las capas internas correspondientes.

Por ejemplo:

```text
Top Layer
Mid Layer 1
Mid Layer 2
Bottom Layer
```

---

# 120. Extensiones habituales de archivos Gerber

Cuando utilizamos extensiones tradicionales podemos encontrar nombres como:

| Extensión | Contenido habitual |
|---|---|
| `.GTL` | Top Copper / Top Layer |
| `.GBL` | Bottom Copper / Bottom Layer |
| `.GTS` | Top Solder Mask |
| `.GBS` | Bottom Solder Mask |
| `.GTO` | Top Overlay / Silkscreen |
| `.GBO` | Bottom Overlay / Silkscreen |
| `.GTP` | Top Paste |
| `.GBP` | Bottom Paste |
| `.GKO` | Board Outline en algunos flujos |
| `.GM1`, `.GM2` | Mechanical Layers en determinados flujos |

---

> [!NOTE]
> Estas extensiones son convenciones comunes, no una regla universal.

Altium también puede generar archivos con:

```text
.gbr
```

y nombres descriptivos.

Por eso debemos revisar el contenido y no depender únicamente de la extensión.

---

# 121. Board Outline en los archivos de fabricación

El fabricante necesita conocer el contorno físico de la PCB.

Por tanto, el paquete debe contener una representación inequívoca del:

```text
Board Outline
```

---

## En Gerber X2

Las versiones actuales del diálogo pueden disponer de una salida específica:

```text
Board Outline
```

generada a partir del Board Shape.

---

## En un flujo Gerber convencional

Puede utilizarse una capa mecánica dedicada al contorno cuando sea necesario.

Por ejemplo:

```text
Board Shape
```

o una Mechanical Layer destinada exclusivamente al perfil.

---

## Lo importante

Debe existir **un único contorno claro y cerrado**.

No debemos enviar:

```text
dos contornos diferentes
```

y esperar que el fabricante determine cuál es correcto.

---

## Revisar también los cutouts

Si la PCB contiene recortes internos:

```text
┌─────────────────────┐
│                     │
│      ┌───────┐      │
│      │CUTOUT │      │
│      └───────┘      │
│                     │
└─────────────────────┘
```

debemos verificar que aparezcan correctamente en el archivo de contorno.

---

# 122. Generación de Gerber X2

Con el `.PcbDoc` activo selecciona:

```text
File → Fabrication Outputs → Gerber X2 Files
```

Aparecerá:

```text
Gerber X2 Setup
```

---

## Configura

- unidades;
- precisión;
- capas;
- Board Outline;
- nombres de archivos.

<img src="../recursos/imgs/altium_gerber_x2_setup.png" alt="Gerber X2 Setup de Altium Designer" width="900">

---

## Board Outline

En el diálogo Gerber X2 actual puede aparecer una entrada específica:

```text
Board Outline
```

Esta información puede generarse directamente desde la geometría del Board Shape.

Esto reduce la necesidad de depender únicamente de una Mechanical Layer para representar el contorno.

---

# 123. Archivos de perforación NC Drill

Los Gerbers describen principalmente geometría de capas.

Las perforaciones se proporcionan mediante:

```text
NC Drill
```

Los archivos utilizan información que indica al fabricante:

```text
qué diámetro perforar
```

y:

```text
en qué coordenadas
```

---

## Incluyen agujeros como

- vias;
- pads through-hole;
- mounting holes;
- otros taladros.

---

## Ruta

Desde el PCB:

```text
File → Fabrication Outputs → NC Drill Files
```

<img src="../recursos/imgs/altium_nc_drill_menu.png" alt="Opción NC Drill Files dentro de Fabrication Outputs" width="650">

---

# 124. Configuración de NC Drill Setup

Al seleccionar NC Drill aparecerá:

```text
NC Drill Setup
```

<img src="../recursos/imgs/altium_nc_drill_setup.png" alt="Ventana NC Drill Setup de Altium Designer" width="850">

---

## Units

Debe ser coherente con el paquete de fabricación.

Por ejemplo, si los Gerbers están configurados en:

```text
Millimeters
```

conviene que NC Drill también utilice:

```text
Millimeters
```

---

## Format

Define la precisión de las coordenadas.

---

> [!IMPORTANT]
> Gerber y NC Drill deben configurarse de manera coherente.

No deberíamos tener, por ejemplo:

```text
Gerber → origen relativo
Drill  → origen completamente diferente
```

porque los agujeros podrían aparecer desplazados respecto a los pads.

---

## Coordinate Position

Dependiendo del flujo de fabricación podemos trabajar con:

```text
Absolute Origin
```

o:

```text
Relative Origin
```

Lo importante es utilizar la misma referencia para todos los archivos asociados.

---

# 125. Plated y Non-Plated Drill Files

NC Drill permite diferenciar agujeros:

```text
Plated
```

de:

```text
Non-Plated
```

Puede habilitarse la opción correspondiente para generar archivos separados.

---

## Ventaja

El fabricante puede identificar claramente:

```text
PTH
```

y:

```text
NPTH
```

---

## Ejemplo conceptual

```text
MiPCB-Plated.txt
```

```text
MiPCB-NonPlated.txt
```

Los nombres exactos dependerán de la configuración de salida.

---

# 126. Agujeros ranurados o Slots

Algunos componentes utilizan agujeros alargados.

Ejemplo:

```text
────────
(      )
────────
```

en lugar de un agujero circular:

```text
○
```

---

## Casos comunes

- conectores;
- terminales;
- switches;
- componentes mecánicos.

---

## Antes de fabricar

Comprueba que Altium identifique correctamente:

```text
Round
Rectangular
Slot
```

según corresponda.

Los archivos NC Drill pueden separar diferentes tipos de agujeros.

---

# 127. Importancia del origen y las coordenadas

Este punto es crítico.

Supongamos que el Gerber utiliza:

```text
Origen = esquina inferior izquierda
```

pero el NC Drill utiliza:

```text
Origen = centro de la hoja
```

El resultado podría ser:

```text
Copper:
┌──────────────┐
│  ○      ○    │
└──────────────┘

Drill:
               ○
                    ○
```

es decir, perforaciones completamente desplazadas.

---

## Regla

Todos los outputs de fabricación deben compartir una referencia coherente.

---

# 128. Crear un Output Job

Aunque podemos generar cada archivo manualmente, el método más organizado consiste en utilizar un:

```text
Output Job
```

archivo:

```text
*.OutJob
```

---

## Crear uno

Desde el panel `Projects`:

1. haz clic derecho sobre el proyecto;
2. selecciona:

```text
Add New to Project → Output Job File
```

3. guarda el archivo.

Por ejemplo:

```text
Fabrication.OutJob
```

<img src="../recursos/imgs/altium_create_outjob.png" alt="Creación de un Output Job File" width="650">

---

# 129. Estructura de un OutJob

Un OutJob puede contener diferentes categorías.

Por ejemplo:

```text
Validation Outputs
```

```text
Documentation Outputs
```

```text
Assembly Outputs
```

```text
Fabrication Outputs
```

```text
Report Outputs
```

```text
Export Outputs
```

---

## Ejemplo

```text
Fabrication.OutJob
│
├── Validation
│   └── Design Rules Check
│
├── Fabrication
│   ├── Gerber Files
│   └── NC Drill Files
│
└── Output Container
    └── Folder Structure
```

---

# 130. Añadir Gerbers al OutJob

Dentro del OutJob localiza:

```text
Fabrication Outputs
```

Selecciona:

```text
Add New Fabrication Output
```

y posteriormente:

```text
Gerber Files
```

o:

```text
Gerber X2 Files
```

Selecciona como fuente:

```text
[PCB Document]
```

cuando resulte conveniente.

<img src="../recursos/imgs/altium_outjob_add_gerber.png" alt="Añadir Gerber Files dentro de un OutJob" width="800">

---

## Configurar

Haz doble clic sobre:

```text
Gerber Files
```

Se abrirá nuevamente:

```text
Gerber Setup
```

Configura:

- Units;
- Decimal;
- Layers;
- Board Outline;
- opciones adicionales.

---

## Ventaja de `[PCB Document]`

Si el proyecto contiene una sola PCB, utilizar:

```text
[PCB Document]
```

puede hacer el OutJob más reutilizable.

Si existen múltiples `.PcbDoc`, selecciona explícitamente la tarjeta correcta.

---

# 131. Añadir NC Drill al OutJob

Dentro de:

```text
Fabrication Outputs
```

selecciona:

```text
Add New Fabrication Output
```

después:

```text
NC Drill Files
```

y selecciona:

```text
[PCB Document]
```

<img src="../recursos/imgs/altium_outjob_add_ncdrill.png" alt="Añadir NC Drill al OutJob" width="800">

---

## Configura

Haz doble clic.

Configura:

- Units;
- Format;
- Coordinate Position;
- separación PTH/NPTH cuando corresponda.

---

# 132. Añadir DRC al OutJob

Una ventaja importante del OutJob es que podemos incluir una validación antes de generar los outputs.

Dentro de:

```text
Validation Outputs
```

añade:

```text
Design Rules Check
```

<img src="../recursos/imgs/altium_outjob_add_drc.png" alt="Design Rules Check dentro de Validation Outputs" width="800">

---

## Objetivo

El flujo se convierte en:

```text
Generar outputs
      ↓
DRC
      ↓
Fabrication outputs
```

Esto añade una capa adicional de seguridad al proceso.

---

> [!NOTE]
> El DRC ejecutado desde el OutJob utiliza la configuración de comprobación definida para el PCB.

Por eso debemos configurar previamente correctamente:

```text
Tools → Design Rule Check
```

---

# 133. Folder Structure y ubicación de salidas

Los outputs del OutJob deben asociarse a un contenedor.

Para archivos de fabricación es habitual utilizar:

```text
Folder Structure
```

---

## Concepto

Tenemos:

```text
Gerber
NC Drill
```

pero todavía debemos indicar:

```text
¿Dónde se guardarán?
```

---

## Output Container

Selecciona:

```text
Folder Structure
```

y habilita en ese contenedor los outputs que quieras generar.

Cuando un output queda correctamente conectado al contenedor, Altium representa visualmente la relación.

<img src="../recursos/imgs/altium_outjob_folder_structure.png" alt="Gerber y NC Drill conectados al Folder Structure" width="900">

---

## Ruta recomendada

Podemos utilizar:

```text
Outputs/Fabrication/
```

o:

```text
Fabrication/
```

dentro de la carpeta del proyecto.

---

## Usar rutas relativas

Cuando sea posible resulta recomendable utilizar:

```text
Use relative path
```

Esto facilita mover el proyecto entre diferentes computadoras.

---

# 134. Generar todas las salidas desde el OutJob

Después de configurar:

```text
Gerber
NC Drill
DRC
Folder Structure
```

podemos generar el paquete.

---

## Procedimiento

1. Guarda el proyecto.
2. Guarda el `.OutJob`.
3. Ejecuta `Repour All`.
4. Ejecuta un DRC final.
5. Abre el `.OutJob`.
6. Verifica que las salidas necesarias estén habilitadas.
7. Selecciona el contenedor correspondiente.
8. Ejecuta la generación.

---

## Resultado

Altium creará los archivos en la ubicación configurada.

---

# 135. Organización recomendada de archivos

Una estructura limpia puede ser:

```text
MiProyecto/
│
├── MiProyecto.PrjPcb
│
├── Main.SchDoc
│
├── Main.PcbDoc
│
├── Fabrication.OutJob
│
│
├── Libraries/
│
├── Datasheets/
│
└── Outputs/
    │
    ├── Fabrication/
    │   ├── Gerber/
    │   └── Drill/
    │
    ├── Assembly/
    │
    └── Documentation/
```

---

## Otra opción

Para un envío concreto:

```text
Outputs/
└── Rev_A/
    ├── Gerber/
    ├── Drill/
    ├── BOM/
    └── Assembly/
```

---

## Ventaja

Evita mezclar:

```text
archivos antiguos
```

con:

```text
archivos actuales
```

---

# 136. Verificación de Gerbers con CAMtastic

Nunca debemos asumir que:

```text
Altium generó los archivos
```

significa automáticamente:

```text
los archivos están correctos
```

Debemos abrirlos nuevamente como si fuéramos el fabricante.

Altium incluye:

```text
CAMtastic
```

para trabajar con archivos CAM.

---

## Crear un documento CAM

Utiliza:

```text
File → New → CAM Document
```

Se abrirá un documento CAM vacío.

<img src="../recursos/imgs/altium_new_cam_document.png" alt="Nuevo CAM Document para revisar Gerbers" width="650">

---

# 137. Quick Load de los archivos de fabricación

Con el CAM Document activo selecciona:

```text
File → Import → Quick Load
```

<img src="../recursos/imgs/altium_cam_quick_load.png" alt="Quick Load de archivos Gerber y NC Drill en CAMtastic" width="750">

---

## Selecciona la carpeta

Indica la carpeta que contiene:

- Gerbers;
- NC Drill;
- archivos CAM relacionados.

Altium intentará detectar automáticamente los archivos.

---

## Resultado

Cada archivo aparecerá como una capa diferente dentro del documento CAM.

---

# 138. Qué comprobar en el visor CAM

Esta es una de las revisiones más importantes de todo el proceso.

---

## Top Copper

Comprueba:

- pistas;
- pads;
- polígonos;
- conexiones.

---

## Bottom Copper

Comprueba lo mismo.

---

## Solder Mask

Comprueba que los pads tengan aperturas correctas.

---

## Silkscreen

Comprueba:

- designadores;
- textos;
- polaridades;
- ausencia de texto sobre pads.

---

## Board Outline

Comprueba que exista:

```text
un solo contorno
```

correcto y cerrado.

---

## Cutouts

Comprueba recortes internos.

---

## Drill

Superpone visualmente el archivo de perforaciones sobre el cobre.

Los agujeros deben coincidir con:

```text
centros de pads
```

y:

```text
vias
```

---

# 139. Verificación de archivos de perforación

Los agujeros son uno de los errores de fabricación más costosos de corregir después.

Comprueba:

```text
drill sobre pad
```

```text
via correctamente centrada
```

```text
mounting hole correcto
```

```text
slot correcto
```

---

## Ejemplo correcto

```text
   PAD
┌─────────┐
│    ○    │
└─────────┘
     ↑
   drill
```

---

## Ejemplo incorrecto

```text
   PAD
┌─────────┐
│         │    ○
└─────────┘
             drill
```

Si observas algo similar, **no envíes el paquete a fabricación**.

Comprueba inmediatamente:

- origen;
- unidades;
- formato;
- Coordinate Position.

---

# 140. Errores comunes antes de fabricar

## Gerber sin Bottom Layer

Una PCB de dos capas puede quedar incompleta.

---

## No incluir Board Outline

El fabricante no puede determinar correctamente la geometría final.

---

## Dos contornos diferentes

Puede provocar interpretaciones incorrectas.

---

## Drill desplazado

Normalmente indica diferencias de origen o configuración.

---

## Confundir Top Paste con Top Solder

Son capas diferentes.

```text
Paste ≠ Solder
```

---

## Serigrafía sobre pads

Parte de la información puede desaparecer durante fabricación.

---

## Footprint incorrecto

Este problema ya no puede solucionarse mediante Gerber.

Si el footprint tiene dimensiones incorrectas, la PCB fabricada también las tendrá.

---

## Pinout incorrecto

Una PCB puede superar perfectamente el DRC y aun así estar eléctricamente mal si el símbolo o footprint tiene una numeración incorrecta.

---

## Invertir un conector

Especialmente peligroso con:

- headers;
- USB;
- JST;
- terminal blocks;
- conectores vistos desde caras diferentes.

---

## Agujeros incorrectos

Un agujero demasiado pequeño puede impedir insertar el componente.

---

# 141. Crear el archivo ZIP para fabricación

Muchos fabricantes permiten subir directamente un archivo:

```text
.zip
```

con todos los archivos necesarios.

---

## Crear carpeta limpia

No comprimas toda la carpeta del proyecto.

Crea una carpeta específica como:

```text
FABRICATION_REV_A/
```

---

## Coloca únicamente los outputs correspondientes

Por ejemplo:

```text
FABRICATION_REV_A/
│
├── Board.GTL
├── Board.GBL
├── Board.GTS
├── Board.GBS
├── Board.GTO
├── Board.GBO
├── Board.GKO
├── Board-Plated.txt
└── Board-NonPlated.txt
```

Los nombres concretos dependerán de tu configuración.

---

## Después comprime

```text
FABRICATION_REV_A.zip
```

---

# 142. Qué archivos enviar al fabricante

Para una PCB convencional de dos capas, el conjunto puede incluir aproximadamente:

```text
Top Copper
Bottom Copper

Top Solder Mask
Bottom Solder Mask

Top Silkscreen
Bottom Silkscreen

Board Outline

NC Drill
```

---

## Si existe stencil

Añade:

```text
Top Paste
```

y/o:

```text
Bottom Paste
```

---

## PCB multicapa

Añade todas las capas internas.

---

> [!IMPORTANT]
> La lista definitiva debe compararse siempre contra los requisitos del fabricante específico.

---

# 143. Archivos opcionales para ensamblaje

Si el fabricante también ensamblará los componentes, Gerber y NC Drill no son suficientes.

Podrían solicitar:

```text
BOM
```

y:

```text
Pick and Place
```

también denominado:

```text
Centroid File
```

---

## BOM

Contiene información como:

```text
Designator
Quantity
Value
Manufacturer
Manufacturer Part Number
```

---

## Pick and Place

Contiene aproximadamente:

```text
Designator
X
Y
Rotation
Layer
```

Esto indica a la máquina de ensamblaje dónde colocar cada componente.

---

## Importante

Fabricar la PCB y ensamblarla son procesos diferentes.

```text
PCB FABRICATION
      ≠
PCB ASSEMBLY
```

---

# 144. Checklist final de fabricación

Antes de enviar el archivo ZIP realiza esta comprobación.

## Esquemático

- [ ] El proyecto está validado.
- [ ] No existen errores eléctricos desconocidos.
- [ ] Los designadores son únicos.
- [ ] Todos los componentes tienen footprints correctos.
- [ ] Los pin numbers coinciden con los pad numbers.
- [ ] Se compararon componentes críticos contra sus datasheets.

---

## Sincronización

- [ ] Schematic y PCB están sincronizados.
- [ ] El último ECO fue ejecutado correctamente.
- [ ] No existen cambios pendientes inesperados.

---

## PCB

- [ ] Board Shape correcto.
- [ ] Dimensiones correctas.
- [ ] Origen definido.
- [ ] Layer Stack correcto.
- [ ] Componentes correctamente colocados.
- [ ] Conectores orientados correctamente.
- [ ] Polaridades revisadas.
- [ ] Pin 1 revisado.
- [ ] Footprints revisados.

---

## Routing

- [ ] Todas las Nets están ruteadas.
- [ ] No existen Connection Lines pendientes.
- [ ] Anchos de pista correctos.
- [ ] Alimentación dimensionada correctamente.
- [ ] Vias dentro de especificaciones.
- [ ] No existen cortocircuitos.
- [ ] Polygon Pours actualizados.

---

## Reglas

- [ ] Clearance configurado.
- [ ] Width configurado.
- [ ] Via Style configurado.
- [ ] Board Clearance configurado.
- [ ] Reglas del fabricante verificadas.

---

## DRC

- [ ] Se ejecutó `Repour All`.
- [ ] Se ejecutó Batch DRC.
- [ ] Se revisaron todas las violaciones.
- [ ] No existen errores desconocidos.
- [ ] Las excepciones están justificadas.

---

## Serigrafía

- [ ] Designators legibles.
- [ ] Textos dentro del Board Shape.
- [ ] No existe serigrafía sobre pads.
- [ ] Polaridades visibles.
- [ ] Pin 1 identificable.
- [ ] Versión de PCB correcta.

---

## Mecánica

- [ ] Agujeros correctos.
- [ ] PTH/NPTH correctos.
- [ ] Slots correctos.
- [ ] Mounting Holes correctos.
- [ ] Conectores accesibles.
- [ ] Revisión 3D realizada.
- [ ] No existen interferencias evidentes.

---

## Gerber

- [ ] Top Copper.
- [ ] Bottom Copper.
- [ ] Todas las capas internas necesarias.
- [ ] Top Solder.
- [ ] Bottom Solder.
- [ ] Top Overlay.
- [ ] Bottom Overlay si corresponde.
- [ ] Board Outline.
- [ ] Paste layers si corresponden.

---

## NC Drill

- [ ] Archivos generados.
- [ ] Unidades correctas.
- [ ] Origen correcto.
- [ ] PTH y NPTH correctamente definidos.
- [ ] Slots incluidos.

---

## Verificación CAM

- [ ] Gerbers abiertos en un visor CAM.
- [ ] Board Outline correcto.
- [ ] Copper correcto.
- [ ] Solder Mask correcta.
- [ ] Silkscreen correcta.
- [ ] Drill alineado.
- [ ] Cutouts correctos.
- [ ] No existen capas inesperadas.

---

## Paquete final

- [ ] Solo contiene archivos necesarios.
- [ ] No contiene Gerbers de revisiones antiguas.
- [ ] Tiene nombre de revisión.
- [ ] El ZIP fue creado correctamente.
- [ ] Se revisaron los requisitos del fabricante.

---

# 145. Flujo completo de Altium Designer

Con las tres partes de esta documentación podemos representar el proceso completo de creación de una PCB en Altium Designer de la siguiente forma:

```text
INSTALAR ALTIUM
       ↓
CREAR PROYECTO
       ↓
CREAR .SchDoc
       ↓
CONFIGURAR GRID
       ↓
BUSCAR COMPONENTES
       ↓
INSTALAR / IMPORTAR LIBRERÍAS
       ↓
COLOCAR COMPONENTES
       ↓
CONFIGURAR DESIGNATORS
       ↓
CONECTAR CON WIRES
       ↓
NET LABELS
       ↓
PORTS
       ↓
POWER PORTS
       ↓
GND / VCC
       ↓
ORGANIZAR ESQUEMÁTICO
       ↓
VALIDATE PCB PROJECT
       ↓
CORREGIR ERC
       ↓
COMPROBAR FOOTPRINTS
       ↓
COMPROBAR PIN ↔ PAD
       ↓
CREAR .PcbDoc
       ↓
DESIGN → UPDATE PCB DOCUMENT
       ↓
ENGINEERING CHANGE ORDER
       ↓
VALIDATE CHANGES
       ↓
EXECUTE CHANGES
       ↓
DEFINIR BOARD SHAPE
       ↓
DEFINIR ORIGEN
       ↓
CONFIGURAR GRID
       ↓
CONFIGURAR LAYER STACK
       ↓
COLOCAR COMPONENTES
       ↓
CONFIGURAR DESIGN RULES
       ↓
CLEARANCE
       ↓
WIDTH
       ↓
VIA STYLE
       ↓
NET CLASSES
       ↓
ROUTING MANUAL
       ↓
CAMBIO DE CAPA
       ↓
VIAS
       ↓
POLYGON POURS
       ↓
GND PLANE
       ↓
REPOUR ALL
       ↓
PCB HEALTH CHECK
       ↓
BATCH DRC
       ↓
CORREGIR VIOLACIONES
       ↓
PREPARAR SILKSCREEN
       ↓
REVISIÓN 2D
       ↓
REVISIÓN 3D
       ↓
REVISAR AGUJEROS
       ↓
DRC FINAL
       ↓
CREAR OUTJOB
       ↓
GENERAR GERBER / GERBER X2
       ↓
GENERAR NC DRILL
       ↓
VERIFICAR CON CAMTASTIC
       ↓
REVISAR TODAS LAS CAPAS
       ↓
COMPROBAR DRILL
       ↓
CREAR ZIP
       ↓
ENVIAR AL FABRICANTE
```

---

# Conclusión

El diseño de una PCB no consiste únicamente en dibujar un esquemático y posteriormente conectar los pads mediante pistas.

Un flujo correcto de trabajo debe mantener una relación coherente entre:

```text
ESQUEMÁTICO
     ↓
LÓGICA ELÉCTRICA
     ↓
COMPONENTES
     ↓
FOOTPRINTS
     ↓
REGLAS
     ↓
PCB
     ↓
VALIDACIÓN
     ↓
FABRICACIÓN
```

Altium Designer permite administrar todas estas etapas dentro de un mismo entorno, pero esta integración también significa que un error cometido en una etapa temprana puede propagarse hasta fabricación.

Por ejemplo:

```text
Símbolo incorrecto
        ↓
Pinout incorrecto
        ↓
PCB aparentemente válida
        ↓
DRC sin errores
        ↓
PCB fabricada incorrectamente
```

Por esta razón, las herramientas automáticas como:

```text
ERC
DRC
AutoRouter
Silkscreen Preparation
Health Check
```

deben considerarse herramientas de **verificación y asistencia**, no sustitutos de la revisión del diseñador.

El flujo más seguro consiste siempre en:

```text
DISEÑAR
   ↓
COMPROBAR
   ↓
VALIDAR
   ↓
REVISAR VISUALMENTE
   ↓
GENERAR
   ↓
VOLVER A COMPROBAR
```

Especialmente antes de fabricación, debemos recordar una regla fundamental:

> **Los archivos Gerber y NC Drill son la representación que verá el fabricante, no necesariamente lo que nosotros vemos dentro del archivo `.PcbDoc`.**

Por tanto, la última comprobación siempre debe realizarse sobre los **archivos de fabricación generados**, cargándolos nuevamente en un visor CAM y verificando que la información que será enviada a producción corresponda exactamente con la PCB que queremos fabricar.
