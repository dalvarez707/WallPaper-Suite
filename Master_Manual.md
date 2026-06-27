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
