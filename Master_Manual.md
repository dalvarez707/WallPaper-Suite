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

### 4.3 Selectores de Estado Avanzados (Filtros de Proceso)

Para un control quirúrgico de tu colección, la **Zona Superior** incluye cuatro listas desplegables (*selectores*). Estos selectores te permiten filtrar las imágenes basándose en las acciones o decisiones de curado que hayas tomado sobre ellas.

<div align="center">
  <img width="657" height="47" alt="image" src="https://github.com/user-attachments/assets/4c252f2c-0b8b-4857-9c09-2384bf78d420" />
</div>

Los cuatro estados que puedes rastrear son:

*   **Pendiente:** Aplica específicamente a las imágenes clasificadas como **CROP**. Filtra aquellas que aún no han recibido su reencuadre manual. *(Nota: Las imágenes APTAS nunca aparecerán aquí, ya que no requieren recorte).*
*   **Flip:** Filtra las imágenes a las que se les ha aplicado un reflejo o espejo horizontal para mejorar la composición visual del fondo.
*   **Ignorada:** Filtra las imágenes marcadas para que la aplicación secundaria (*Companion*) las pase por alto al rotar los wallpapers, sin importar si cumplen con los tags o la calidad.
*   **Eliminar:** Filtra las imágenes que has marcado con bandera roja, pendientes de ser borradas definitivamente del disco duro.

#### Modos de Operación de los Selectores (Las 3 Opciones):
Cada una de las cuatro listas desplegables cuenta con tres modos idénticos que dictan cómo interactúan con tu catálogo:

1.  **Inactivo:** El filtro no se aplica. El sistema muestra todas las imágenes sin importar si cumplen o no con ese estado específico.
2.  **Mostrar:** Filtro restrictivo positivo. El sistema **solo mostrará** las imágenes que tengan activo ese estado (por ejemplo, si pones *Pendiente* en "Mostrar", solo verás las imágenes Crop a las que les falta su recorte).
3.  **Ocultar:** Filtro restrictivo negativo. El sistema **esconderá por completo** las imágenes que tengan ese estado (por ejemplo, si pones *Eliminar* en "Ocultar", limpiarás tu vista de trabajo de cualquier imagen que ya hayas decidido borrar).

> 🔄 **Recalculación Instantánea:**
> El motor del Master es dinámico. En el milisegundo en que cambies el valor de cualquiera de estas listas, la tira de miniaturas (*thumbs*) de la izquierda se actualizará inmediatamente, y los números entre paréntesis de los **Switches de Calidad** se recalcularán para decirte con precisión cuántas imágenes de cada categoría sobrevivieron a tus filtros avanzados.

### 4.4 Lanzamiento del motor secundario (Botón 'Companion')

El último elemento de control ubicado en la **Zona Superior** es el botón **'Companion'**. Este control actúa como el puente de activación hacia el software secundario encargado de gestionar y rotar los fondos de pantalla en tu sistema.

<div align="center">
  <img width="95" height="42" alt="image" src="https://github.com/user-attachments/assets/bd48c2cc-7564-4c65-b268-5d2b865c1f19" />
</div>

Su funcionamiento y lógica de seguridad operan de la siguiente manera:

*   **Lanzamiento:** Si el Companion se encuentra cerrado, al presionar este botón el Master lo ejecutará e iniciará de forma automática en segundo plano.
*   **Alerta de Ejecución:** Si el Companion ya se está ejecutando en el sistema, el Master detectará el proceso activo y desplegará una ventana de alerta informándote que la aplicación ya está operando, evitando aperturas duplicadas innecesarias.

> 💡 **Nota de usabilidad (Bandeja del Sistema):**
> Si presionas el botón y el Master te muestra la alerta de que ya está activo, pero no ves ninguna ventana flotante, recuerda que **el Companion está diseñado para trabajar de forma discreta y puede encontrarse minimizado en la bandeja del sistema (system tray)**, junto al reloj de Windows. Puedes interactuar con él directamente desde su icono en esa barra.

### 4.5 Motor de Búsqueda Avanzado y Filtro de Etiquetas (Tags)

Al inicio de la **Columna Izquierda** se ubica el cuadro de edición de búsqueda. Este componente es uno de los módulos más potentes del Master: no se limita a buscar palabras simples, sino que procesa operadores lógicos y comandos virtuales en tiempo real para segmentar tu catálogo de forma quirúrgica.
<div align="center">
<img width="339" height="52" alt="image" src="https://github.com/user-attachments/assets/9036caac-aa63-472c-b352-7a5267739301" />
</div>

> 💡 **Ayuda en Interfaz:** Si dejas el cursor del ratón (*hover*) posicionado sobre este cuadro de texto, el sistema desplegará un mensaje emergente (*tooltip*) con un resumen rápido de los comandos admitidos.

---

#### A) Operadores Lógicos de Sintaxis

Puedes combinar palabras clave (que buscan coincidencia tanto en las etiquetas asignadas como en el nombre del propio archivo) utilizando los siguientes operadores de filtrado:

| Operador | Tipo de Lógica | Función | Ejemplo Práctico |
| :---: | :---: | --- | --- |
| **` ` (Espacio)** | **Término Básico** | Separa condiciones obligatorias consecutivas de forma general. | `paisaje montaña` |
| **`+`** | **Y (AND)** | **Condición Estricta.** La imagen debe contener obligatoriamente todos los términos unidos por el más. | `dress+high_heels` |
| **`,`** | **O (OR)** | **Grupos Independientes.** Separa bloques de búsqueda. El sistema mostrará la imagen si cumple con al menos uno de los bloques aislados por la coma. | `cat, dog` |
| **`-`** | **NO (NOT)** | **Exclusión.** Descarta y oculta cualquier imagen que contenga la palabra que sigue al signo de resta. | `-beach -short` |

---

#### B) Comandos Virtuales de Estado

Adicionalmente al texto de las etiquetas, puedes escribir palabras clave precedidas de dos puntos (`:`) para interrogar directamente los metadatos o el estado interno de conservación de cada wallpaper:

* **`:favorita` o `:favoritas`**: Muestra exclusivamente las imágenes que has marcado con la estrella de selección especial.
* **`:nofavorita` o `:nofavoritas`**: Muestra las imágenes comunes que no forman parte de tus destacadas.
* **`:tag`**: Filtra y expone únicamente las imágenes que ya tienen asignada al menos una etiqueta. Ideal para revisar lo que ya has trabajado.
* **`:notag`**: Muestra todas las imágenes que se encuentran completamente limpias y sin etiquetas. Ideal para identificar el trabajo que tienes pendiente por clasificar.

---

#### C) Caso de Éxito: Ejemplo Combinado Complejo

La verdadera potencia del motor radica en que puedes mezclar todo lo anterior en una sola línea de búsqueda. Observa cómo el sistema interpreta la siguiente instrucción:

`:favorita dress+high heels, blonde+high heels -beach`

El algoritmo del Master analiza la sintaxis y divide el catálogo ejecutando la siguiente lógica en orden:

1. **Filtro Base Inicial:** Solo tomará en cuenta imágenes que sean `:favorita`.
2. **Evaluación de Bloques (Separados por la coma `,`):**
   * **Bloque 1:** Mostrará la imagen si tiene la etiqueta exacta `dress` **Y** la etiqueta compuesta exacta `high heels` (identificada perfectamente gracias al operador `+`).
   * **Bloque 2:** Si la imagen no cumple con el Bloque 1, el sistema le dará una segunda oportunidad si contiene la etiqueta `blonde` **Y** la etiqueta compuesta `high heels`.
3. **Filtro de Exclusión Global:** De todos los resultados que hayan sobrevivido a los pasos anteriores, **eliminará de la vista** cualquier imagen que contenga la palabra o etiqueta `beach`.
---
> ⌨️ **Activación del Filtro (Gatillo por Teclado):**
> Para evitar caídas de rendimiento mientras escribes comandos complejos, el motor de búsqueda no se aplica letra por letra. El filtrado se ejecutará únicamente cuando presiones la tecla **`Enter`** dentro del cuadro de edición o cuando uses la tecla **`Tab`** (o hagas clic fuera) para salir del cuadro.
---
#### D) Limpieza Rápida del Buscador

Para agilizar el flujo de trabajo, el cuadro de edición cuenta con un mecanismo de reinicio inmediato:

* **Botón de Borrado (`X`):** En el momento en que escribas cualquier caracter o tengas un filtro de búsqueda activo, aparecerá automáticamente un icono de una **`X`** en el extremo derecho del cuadro de texto. 
* Al hacer clic sobre esta **`X`**, el motor limpiará por completo la línea de comandos de un solo paso, restableciendo de inmediato la tira de miniaturas para mostrar todo el catálogo original (según los filtros de los switches superiores).
### 4.6 Ordenamiento del Catálogo (Ascendente / Descendente)

Ubicado inmediatamente debajo del motor de búsqueda avanzada, se encuentra el selector de ordenamiento. Este control te permite definir la dirección en la que se organizará la secuencia de archivos en tu tira de exploración.

<div align="center">
  <img width="200" height="28" alt="image" src="https://github.com/user-attachments/assets/381f931d-12fd-4a9b-92cc-f6bf0d635780" />
</div>

Su funcionamiento es directo y automático:

* **Orden Ascendente (Por defecto):** Organiza el catálogo de forma alfabética estándar de la **A a la Z** (o numéricamente de menor a mayor basado en el nombre del archivo de imagen).
* **Orden Descendente:** Invierte por completo el catálogo, organizándolo de la **Z a la A**.

> 🔄 **Aplicación Inmediata:**
> Al igual que el resto de los controles del Master, no necesitas confirmar la acción. Al cambiar la selección en esta lista desplegable, el orden de la tira de miniaturas (*thumbs*) se reestructurará en tiempo real en la pantalla.

### 4.7 Catálogo Gráfico y Estado de Miniaturas (Tira de Thumbs)

Ubicada en la **Columna Izquierda**, justo debajo de las herramientas de ordenamiento, se encuentra la **Tira de Miniaturas (Thumbs)**. Este componente actúa como el catálogo visual interactivo de la carpeta y sirve como un tablero de control rápido, ya que cada miniatura refleja fielmente los procesos, etiquetas y estados aplicados a la imagen.

<div align="center">
  <img width="322" height="472" alt="image" src="https://github.com/user-attachments/assets/e6b40389-15f7-46d2-83c7-9b86c44821b3" />
</div>

#### Características del Renderizado Visual:
* **Dimensión Óptima:** Las imágenes se despliegan con una altura máxima fija de **120px**, pero **mantienen estrictamente su relación de aspecto original** en su contenedor para evitar distorsiones visuales.
* **Preservación Original:** La miniatura en la tira **siempre mostrará la imagen en su estado físico original** (por ejemplo, si aplicas un *Flip Horizontal*, este se reflejará en el Canvas de trabajo derecho, pero el *thumb* conservará su orientación base).

---

#### 🎨 Capas de Información y Código de Indicadores:

Cada miniatura puede acumular uno o varios de los siguientes indicadores visuales de forma simultánea según su estado actual en el archivo `datos_carpeta.json`:

1. **Bordes por Categoría de Calidad:**
   * **🟢 Borde Verde:** Imagen **APTA** (óptima para la pantalla).
   * **🔵 Borde Azul:** Imagen marcada para **CROP** (requiere reencuadre).
   * **🔴 Borde Rojo:** Imagen identificada como **LowRes** (baja resolución).

2. **Indicador de Selección Activa (Flecha Negra):**
   * Una pequeña **flecha negra** se posicionará sobre el extremo izquierdo de la miniatura que esté seleccionada actualmente. La imagen que posea esta flecha se cargará de inmediato en el Canvas de trabajo del panel derecho.

3. **Etiquetas de Proceso (Borde Derecho):**
   * **⭐ +Fav:** Se muestra si la imagen ha sido marcada en tu lista de favoritas.
   * **✂️ +Crop:** Se añade si la imagen ya cuenta con coordenadas de recorte válidas y personalizadas.
   * **↔️ +Flip:** Indica que la imagen tiene activo el reflejo horizontal para mejorar su composición.
   * **🏷️ +Tag:** Aparece si la imagen ya tiene una o más palabras clave (etiquetas) asignadas.

4. **Estado de Exclusión (Ignorar):**
   * **⚠️ +Ignorar:** Si marcas una imagen para ser omitida por el rotador, aparecerá esta etiqueta en el borde derecho, **todo el marco de la miniatura se tornará gris y la imagen se desaturará (blanco y negro)** para denotar su inactividad.

5. **Bandera de Destrucción (Eliminar):**
   * **❌ MARCADA PARA ELIMINAR:** Si etiquetas una imagen para ser borrada, se le aplicará un **bloqueo visual completo con un overlay translúcido de color ROJO** y un texto superpuesto con la advertencia, destacándola inmediatamente del resto.

---

#### ⌨️ Navegación y Control por Teclado

Para mantener ese flujo de trabajo en "piloto automático" y no depender exclusivamente del ratón, el Master cuenta con un sistema de navegación dual:

* **Navegación por Ratón:** Haz un clic izquierdo directo sobre cualquier miniatura de la tira para activarla.
* **Navegación por Teclado:** Puedes explorar el catálogo de forma fluida utilizando las teclas:
  * ⬆️ **`RePág` (Page Up):** Salta inmediatamente a la imagen **anterior** de la lista.
  * ⬇️ **`AvPág` (Page Down):** Salta inmediatamente a la imagen **siguiente** de la lista.

Al usar cualquiera de los dos métodos, la imagen se seleccionará, la flecha negra se moverá a su costado y el Canvas derecho se actualizará al instante con el archivo seleccionado.

### 4.8.1 El Canvas de Previsualización Dinámica y Herramienta de Recorte (*Crop*)

El Canvas es el lienzo interactivo principal donde se proyecta la imagen seleccionada en la tira de miniaturas. Además de servir como monitor a gran escala, es el entorno donde se calcula y ejecuta el reencuadre de los fondos de pantalla.

<div align="center">
  <img width="1562" height="818" alt="image" src="https://github.com/user-attachments/assets/ae706cad-eb9b-41ca-af96-eba672f8e130" />
</div>

#### 📐 El Marco Matemático de Reencuadre (Aspect Ratio Mask)
Cuando la imagen activa tiene un diagnóstico de calidad **CROP** o **LowRes**, el Canvas proyecta automáticamente una máscara de recorte en forma de recuadro. 

*   **Composición del Marco:** Consiste únicamente en un **borde perimetral delgado**, manteniendo el interior completamente transparente para no obstruir la visibilidad del wallpaper.
*   **Proporción Inteligente:** Las dimensiones de este marco se calculan matemáticamente en tiempo real de forma proporcional a la relación de aspecto del monitor (en este manual, $16:9$).
*   **Código de Color de Estado:**
    *   **🟡 Borde Amarillo:** Indica que el reencuadre está **Pendiente**. Es el estado inicial de una imagen *Crop* que aún no ha sido guardada.
    *   **🟢 Borde Verde:** Indica que el reencuadre ha sido **Establecido y Guardado** con éxito en el archivo JSON.

> ⚠️ **Aclaración sobre el Curado LowRes:**
> El sistema permite aplicar de forma libre el marco de recorte sobre imágenes catalogadas como **LowRes**. Sin embargo, debes tener en cuenta que, al forzar su uso como wallpaper, la imagen podría lucir pixelada en tu monitor debido a su falta de resolución nativa.

---

#### 🎮 Restricción de Ejes y Métodos de Ajuste

El marco inteligente detecta la orientación excedente del wallpaper y **bloquea automáticamente los ejes** que no necesitas, permitiéndote deslizar el encuadre únicamente hacia donde hay píxeles disponibles:
*   Si la imagen es **más alta** que la proporción del monitor, el marco se deslizará estrictamente en el **eje vertical** (Arriba / Abajo).
*   Si la imagen es **más larga**, el marco se deslizará estrictamente en el **eje horizontal** (Izquierda / Derecha).

Para ajustar la composición perfecta, puedes utilizar dos métodos indistintos:

1.  **Control con Ratón (Arrastrar y Soltar):** Haz clic izquierdo sostenido dentro del recuadro, arrástralo hasta la posición deseada y suelta el botón. El sistema capturará las coordenadas exactas y guardará el cambio de manera automática (el borde cambiará a verde).
2.  **Control Fino con Teclado (Flechas de Dirección):** Puedes usar las flechas del teclado (`↑` `↓` `←` `→`) para desplazar el marco píxel por píxel. Las flechas activas corresponderán únicamente al eje excedente de la imagen.

---

#### ⌨️ Gestión de Foco e Interrupción del Teclado

> ⚠️ **NOTA DE USABILIDAD (Conflicto de Teclas):**
> Las flechas de dirección del teclado **no moverán el marco de recorte si el cursor está parpadeando dentro de un cuadro de texto** (como el filtro de búsqueda o el editor de etiquetas), ya que en ese momento el sistema prioriza la escritura.
> 
> *   **Solución Rápida:** Presiona la tecla **`Tab`** para alternar el foco de la interfaz. Al pulsarla, saltarás instantáneamente del área de edición de texto de vuelta al área de trabajo del Canvas, reactivando las flechas para el control del *Crop*.

### 4.8.2 Editor de Etiquetas Personalizadas (Tags)

Ubicado inmediatamente debajo del Canvas de previsualización, se encuentra el campo de edición de etiquetas. Este cuadro de texto te permite indexar palabras clave directamente en los metadatos de la imagen activa dentro del archivo `datos_carpeta.json`.

<div align="center">
  <img width="415" height="72" alt="image" src="https://github.com/user-attachments/assets/bd226856-212d-46c0-8890-df101cefcae3" />
</div>

#### 🏷️ Reglas de Sintaxis y Comportamiento del Editor
El sistema está diseñado para ser un lienzo limpio y directo, admitiendo dos estructuras principales separadas estrictamente por **comas (`,`)**:

* **Tags Simples:** Palabras clave de un solo término. *Ejemplo: `ciudad, paisaje, bosque`.*
* **Tags Compuestos:** Frases o conceptos de múltiples palabras con espacios intermedios. *Ejemplo: `ciudad de mexico, bosque de chapultepec`.*

> ⚠️ **Comportamiento Literal del Campo (Sin Asistencias):**
> Es muy importante tener en cuenta que el editor **no cuenta con autollenado o texto predictivo, ni incluye corrector ortográfico**. El Master guardará de forma exacta y literal lo que escribas; si introduces un tag con una falta de ortografía o un dedazo, así se almacenará en los metadatos de la imagen y afectará a tus futuras búsquedas. ¡Revisa bien antes de confirmar!

> 💡 **Consejo de Indexación:**
> El motor del Master es capaz de interpretar de forma independiente los tags simples de los compuestos. Para una base de datos más robusta, se recomienda "anidar" conceptos de lo general a lo particular en la misma imagen. Por ejemplo, puedes escribir: `ciudad, ciudad de mexico` o `bosque, bosque de chapultepec`. Esto te permitirá encontrar la imagen más adelante tanto si buscas el término genérico como la ubicación exacta.

> 🚫 **Restricción de Caracteres:**
> Aunque el campo técnicamente acepta caracteres especiales, acentos o diéresis (`´`, `¨`, etc.), **se desaconseja por completo su uso** para garantizar la máxima compatibilidad, consistencia y velocidad al momento de ejecutar tus búsquedas avanzadas.

---

#### 💾 Guardado Automático y Gestión del Foco

El flujo de captura está optimizado para que no tengas que soltar el teclado en ningún momento:

* **Persistencia:** Las etiquetas se guardarán de forma automática en el JSON en el instante en que presiones la tecla **`Enter`** o cuando salgas del cuadro de texto presionando la tecla **`Tab`**.
* **Comportamiento de las Flechas:** Mientras el cursor esté parpadeando dentro de este campo, las flechas de dirección (`←` `→`) servirán exclusivamente para navegar entre las letras del texto que estás escribiendo. 

> ⌨️ **Recordatorio de Navegación:**
> Recuerda que mientras estés editando tags, el control del *Crop* en el Canvas superior quedará temporalmente suspendido. Para volver a mover el marco de recorte con las flechas, simplemente presiona **`Tab`** para trasladar el foco de la interfaz de vuelta al área de trabajo.

### 4.8.3 Barra de Información Dinámica del Archivo

Ubicada justo debajo del editor de etiquetas, se encuentra una línea de metadatos dividida estratégicamente en **tres columnas independientes**. Este bloque proporciona un desglose informativo completo del archivo activo y un acceso directo al sistema de archivos de Windows.

<div align="center">
  <img width="1483" height="45" alt="image" src="https://github.com/user-attachments/assets/ad1b860d-16c0-4921-8a4d-15fc8fd6c413" />
</div>

#### 🏛️ Estructura de las Tres Columnas:

* **Columna 1: Acceso Directo al Archivo (`Archivo: [Nombre]`)**
    * Muestra la etiqueta `Archivo:` seguida del nombre completo de la imagen actual resaltado en **color azul**.
    * 🖱️ **Acción Especial (Doble Clic):** Si haces doble clic izquierdo sobre el nombre en azul, el Master ejecutará un comando del sistema que **abrirá instantáneamente la carpeta contenedora en el Explorador de Windows, dejando el archivo de la imagen actual seleccionado mecánicamente**. Es ideal para copiar, mover o respaldar el archivo físico sin buscarlo manualmente.

* **Columna 2: Cintillo de Estados en Tiempo Real**
    * Este bloque funciona como un espejo informativo de control. Despliega en grande el diagnóstico técnico de calidad (**🟢 Apta / 🔵 Crop / 🔴 LowRes**) y los 5 indicadores de proceso que tenga activos la imagen en ese microsegundo (**⭐ Fav**, **✂️ Crop**, **↔️ Flip**, **⚠️ Ignorar**, **❌ Eliminar**).
    * Su paleta de colores, iconos y nomenclaturas coinciden exactamente con los de la tira de *thumbs* izquierda, permitiendo una confirmación visual rápida mientras trabajas en el Canvas.

* **Columna 3: Dimensiones Físicas (`Tamaño (px): Ancho x Alto`)**
    * Muestra de forma estrictamente informativa la resolución nativa real del archivo de imagen en píxeles (por ejemplo: `3840 x 2160`). Te sirve como métrica de referencia para entender por qué el software le asignó su categoría de calidad actual.

### 4.8.4 Panel de Acciones y Botonera Operativa

Ubicada en la parte inferior del Área de Trabajo, se encuentra la barra de herramientas principal. Está distribuida de forma uniforme y agrupa todos los controles de edición de estado, navegación acelerada y el módulo destructor de archivos.

<div align="center">
  <img width="1555" height="41" alt="image" src="https://github.com/user-attachments/assets/66f86a11-cc0d-40f3-a4fb-ccc2ec8b94f9" />
</div>

#### 🎮 Comportamiento de Conmutación (*Toggle*)
La mayoría de los botones operan bajo una lógica de conmutación de estados (*toggle*). Al presionarlos (o usar su atajo de teclado), la imagen alternará instantáneamente entre tener el estado activo o inactivo en la base de datos JSON.

---

#### 🛠️ Desglose de Controles y Atajos de Teclado:

| Botón | Atajo de Teclado | Tipo de Acción | Comportamiento y Efecto Visual |
| :--- | :---: | :---: | :--- |
| **`< Previa`** | **`RePág`** | Navegación | Retrocede de forma secuencial a la imagen anterior del catálogo filtrado. |
| **`Confirmar`** | **`Enter`** | Validación Acelerada | Consolida y guarda la posición actual del marco de recorte en el JSON. **Función clave para el "piloto automático":** si el *Crop* centrado que el sistema calcula por defecto te parece correcto, basta con presionar `Enter` para asegurar la posición de inmediato sin necesidad de interactuar con el mouse o reajustar con las flechas. *(Fondo Verde).* |
| **`Flip`** | **`Ctrl + H`** | Estado Visual | Invierte horizontalmente el wallpaper **exclusivamente dentro del Canvas grande como simulación de composición**. No altera el archivo físico ni modifica la vista de la miniatura izquierda. |
| **`Favorita`** | **`Ctrl + F`** | Estado / Tag | Añade o remueve la estrella distintiva de selección especial. *(Fondo Amarillo).* |
| **`Ignorar`** | **`Esc`** | Estado / Filtro | Marca la imagen para ser omitida por el rotador secundario (*Companion*). Desatura el *thumb* a blanco y negro. |
| **`Eliminar`** | **`Supr`** *(Delete)* | Pre-Borrado | Aplica una bandera roja de destrucción y superpone el overlay de advertencia sobre la miniatura, dejándola en lista de espera. *(Fondo Rojo).* |
| **`Siguiente >`** | **`AvPág`** | Navegación | Avanza de forma secuencial a la siguiente imagen del catálogo filtrado. |

> ⚠️ **NOTA DE SEGURIDAD DE FOCO (Conflicto con la tecla Enter):**
> Al igual que sucede con las flechas de dirección, la tecla **`Enter` NO funcionará para confirmar o establecer el Crop si el cursor se encuentra parpadeando dentro de algún área de edición de texto** (ya sea en el filtro de tags superior o en el editor de tags de la imagen). En esos casos, `Enter` se reservará exclusivamente para procesar el texto escrito. Recuerda presionar **`Tab`** para salir del cuadro de texto, recuperar el foco en el Canvas y reactivar el guardado rápido del recorte.

---

#### 🗑️ El Botón Rojo de Destrucción (Vaciar Papelera Global)

El último botón de la cuadrícula (identificado con el icono **🗑️** y un color rojo intenso) es **el único componente que realiza una acción destructiva directa sobre tus archivos físicos**. <img width="192" height="32" alt="image" src="https://github.com/user-attachments/assets/2466e6e2-91fe-4f4d-9303-012f5a7774e1" />


Las imágenes marcadas con la bandera de "Eliminar" (con el botón o la tecla `Supr`) no se borran del disco duro de inmediato; permanecen en un estado de retención seguro dentro de la aplicación. Para consolidar el borrado, debes ejecutar este módulo:

1.  **Activación:** Haz clic en el botón **🗑️**.
2.  **Cuadro de Confirmación de Seguridad:** El Master interrumpirá la pantalla mostrando una ventana de alerta del sistema que te informará explícitamente:
    * La cantidad exacta de imágenes que están a punto de ser procesadas.
    * La advertencia de que los archivos serán removidos de su directorio actual y transferidos directamente a la **Papelera de Reciclaje de Windows**.
3.  **Ejecución:** Los archivos físicos no serán alterados a menos que confirmes la acción en dicha ventana emergente, dándote una red de seguridad infalible contra borrados accidentales.
