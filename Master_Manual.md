# Administrador de Wallpapers - Guía de Uso del Master

Bienvenido al manual de usuario del Master de Wallpapers. Este software fue diseñado con un enfoque práctico y óptimo para automatizar, clasificar y curar colecciones de imágenes, transformándolas en fondos de pantalla perfectos para tu resolución nativa actual, sin alterar jamás tus archivos originales.

---

## 1. Arquitectura de la Interfaz (Zonas de Trabajo)

Para ofrecer un flujo de trabajo fluido y visual, la pantalla principal del Master se divide estratégicamente en tres zonas operativas:

* **Zona Superior (Control y Estado):** Es el panel de mando. Aquí se despliega la información técnica de la pantalla activa del sistema, se selecciona la ruta de la carpeta de trabajo y se gestionan los filtros globales para segmentar las imágenes según su estado de curado.
<div align="center">
  <img width="1908" height="42" alt="image" src="https://github.com/user-attachments/assets/fe3d79e5-0155-44aa-948e-f532bd6317a0" />
</div>

* **Columna Izquierda (Navegación y Catálogo):** Diseñada para la búsqueda y selección rápida. Incluye herramientas de filtrado por etiquetas (tags), ordenamiento alfabético (ascendente/descendente) y una lista vertical con desplazamiento fluido (*scroll*) que muestra las miniaturas (*thumbs*) de todas las imágenes disponibles.
<div align="center">
<img width="354" height="968" alt="image" src="https://github.com/user-attachments/assets/4de98401-c8af-4c0b-b558-e8771909e9dd" />
</div>

* **Panel Derecho (Detalle, Previsualización y Acción):** El área de trabajo principal. Muestra una vista previa ampliada de la imagen seleccionada junto con su herramienta de encuadre (*crop*). Adicionalmente, presenta un resumen con los metadatos de la imagen y la botonera de funciones para asignar estados o etiquetas en tiempo real.
<div align="center">
<img width="1559" height="969" alt="image" src="https://github.com/user-attachments/assets/0bd23f78-55b7-4825-874b-b98800a217a9" />
</div>
---
## 2. Diagnóstico Automático y Clasificación de Imágenes

En el momento exacto en que seleccionas y abres una carpeta de trabajo, el Master ejecuta un proceso en segundo plano que analiza cada archivo de imagen. El sistema extrae la resolución en píxeles ($ancho \times alto$) y calcula de forma matemática la relación de aspecto, comparándola inmediatamente con tu pantalla actual.

A partir de este análisis, el programa clasifica automáticamente las imágenes en tres estados base:

* **APTAS:** Imágenes que cuentan con la resolución y la relación de aspecto idóneas para usarse inmediatamente como fondo de pantalla sin modificaciones.
* **CROP:** Imágenes que poseen una resolución alta y óptima, pero cuya relación de aspecto difiere de la pantalla actual, por lo que requieren un reencuadre o recorte manual para lucir perfectas.
* **LowRes:** Imágenes cuyo ancho, alto o ambos ejes son menores a la resolución nativa de tu pantalla actual, quedando marcadas para identificarse rápidamente como archivos de baja resolución.

---

## 3. Persistencia de Datos Segura (`datos_carpeta.json`)

Toda la magia del curado se realiza de manera **no destructiva**. El Master jamás modificará, recortará ni alterará tus archivos de imagen originales durante el proceso.

Para lograr esto, al abrir la carpeta origen se genera automáticamente un archivo centralizado llamado `datos_carpeta.json`.

> ⚠️ **NOTA CRÍTICA DE SEGURIDAD:** > El archivo `datos_carpeta.json` almacena de forma virtual todo el progreso de tu trabajo (etiquetas asignadas, estados modificados y coordenadas de recorte). **Bajo ninguna circunstancia debes borrar este archivo ni editar su contenido de manera manual**, a menos que cuentes con conocimientos profundos en la sintaxis y estructura de archivos JSON. Si el archivo se corrompe o se elimina, perderás todo el historial de curado de esa carpeta específica.

## 4. Flujo de Trabajo (¿Cómo usar el Master?)

En esta sección se detalla el proceso paso a paso para operar el sistema. Para efectos prácticos de este manual, **todos los ejemplos e imágenes ilustrativas se basan en una pantalla con resolución nativa de 1920x1080 (Relación de aspecto 16:9)**. Los valores numéricos que veas en tu interfaz cambiarán automáticamente para adaptarse a los componentes de tu propio hardware.

> ℹ️ **NOTA TÉCNICA IMPORTANTE (Validez del Curado):**
> En la esquina superior izquierda de la **Zona Superior**, el Master detecta y despliega inmediatamente la resolución actual y la relación de aspecto de tu monitor. 
> 
> Es crucial entender que **el diagnóstico de calidad (APTAS / CROP / LowRes) y las coordenadas de los recortes generados están íntimamente ligados a la pantalla donde se realiza el proceso**. Por lo tanto, el archivo de curado resultante solo tendrá validez estricta en la computadora de trabajo original o en equipos que cuenten con un monitor de idénticas características de resolución y aspecto. Si trasladas la carpeta a una PC con una pantalla diferente, las clasificaciones y encuadres podrían no ser exactos.

---

### 4.1 Selección de Ruta y Carga Inicial de Archivos

El flujo de trabajo comienza en la **Zona Superior** de la interfaz, utilizando los controles de dirección de carpetas.

<div align="center">
  <img width="482" height="39" alt="image" src="https://github.com/user-attachments/assets/5c4e92bf-4e79-4b36-a37d-e5d0ddfccf13" />
</div>

El proceso de carga se gestiona a través de los siguientes componentes:

1. **Botón 'Origen':** Al hacer clic, se desplegará una ventana del explorador de archivos del sistema que te permitirá seleccionar una **Carpeta** de trabajo completa. El Master está optimizado exclusivamente para el procesamiento por lotes, por lo que **no trabaja con archivos individuales**.
2. **Cuadro de Texto (Ruta Actual e Historial):** Ubicado inmediatamente después del botón, este cuadro muestra la ruta absoluta de la carpeta en la que estás trabajando. 

> 💡 **Acceso Rápido al Historial:**
> El Master conserva un registro inteligente de las rutas que has procesado previamente. Si haces clic directamente sobre el cuadro de texto de la ruta, se desplegará un menú dinámico que te permitirá seleccionar y saltar rápidamente a cualquier carpeta de tu historial, ahorrándote la navegación manual en el explorador.

> ℹ️ **Recordatorio de Persistencia:**
> Recuerda que el proceso es totalmente independiente: cada carpeta que decidas abrir mediante este método generará de forma automática y aislada su propio archivo `datos_carpeta.json` en su raíz.

### 4.2 Control de Filtros Globales y Estadísticas de Calidad

Inmediatamente después del cuadro de ruta, en la **Zona Superior**, se ubica el panel de control de estados. Este bloque está compuesto por tres interruptores (*switches*) diferenciados por colores, los cuales actúan como el primer gran filtro del catálogo.

<div align="center">
  <img width="468" height="38" alt="image" src="https://github.com/user-attachments/assets/e569bf0a-64a0-40a0-9ef5-5dfb868e04b7" />
</div>

Cada interruptor representa una de las clasificaciones automáticas de calidad y cuenta con un sistema de doble indicador numérico:

*   **🟢 Apta (Verde):** Filtra las imágenes que encajan perfectamente con la pantalla actual.
*   **🔵 Crop (Azul):** Filtra las imágenes de alta resolución que requieren un reencuadre.
*   **🔴 LowRes (Rojo):** Filtra las imágenes que no alcanzan la resolución mínima nativa.

#### ¿Cómo leer los indicadores numéricos?
Junto al título de cada clasificación verás dos números que se actualizan en tiempo real:
1.  **Primer número (Total de Categoría):** Te indica la cantidad absoluta de imágenes dentro de la carpeta que pertenecen a esa clasificación de calidad específica.
2.  **Segundo número (Entre paréntesis):** Es un contador dinámico. Te muestra cuántas de esas imágenes están siendo desplegadas actualmente en la tira de miniaturas (*thumbs*) de la izquierda debido a que cumplen con el resto de los filtros activos (como las etiquetas o el buscador).

#### Comportamiento de los Switches y Código de Color Visual:
*   **Activo (ON):** El sistema incluye las imágenes de esta categoría en la lista de exploración.
*   **Inactivo (OFF):** Oculta por completo la categoría de la tira de miniaturas, permitiéndote limpiar la vista de trabajo para enfocarte únicamente en el grupo de imágenes que deseas curar.

> 🎨 **Sincronización Visual Dinámica:**
> El color asignado a cada interruptor (**Verde, Azul y Rojo**) no es casualidad. Existe una correspondencia directa con la **Columna Izquierda**: cada miniatura (*thumb*) en la tira de navegación se renderiza con un borde del color que coincide con su diagnóstico actual. 
> * Si ves una miniatura con **borde verde**, sabrás al instante que es **APTA**.
> * Si el **borde es azul**, la imagen está marcada para **CROP**.
> * Si el **borde es rojo**, sabrás de inmediato que es una imagen **LowRes**.
> <div align="center"><img width="319" height="454" alt="image" src="https://github.com/user-attachments/assets/778c46cf-f149-49f8-b3a5-d2b0ca50c3dc" /></div>
> Esto te permite escanear visualmente todo tu catálogo con un solo vistazo antes de interactuar con él.
