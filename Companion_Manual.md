# Manual de Usuario: El Companion
## Sistema de Despliegue y Automatización de Wallpapers
<div align="center">
<img width="786" height="543" alt="image" src="https://github.com/user-attachments/assets/1fdadba9-4ab0-48c7-b7ab-034457011544" />
</div>
---

# 1. Introducción y Filosofía del Sistema

El **Companion** es un servicio de software ligero y discreto diseñado para residir en la memoria de tu sistema (ejecutándose desde el *System Tray* o bandeja de tareas). Su único objetivo es tomar el catálogo de imágenes previamente estructurado, curado y etiquetado en el software *Master*, y lucirlo de forma automatizada directamente en tu escritorio.

### 1.1 Operación Cero Destructiva y Renderizado Dinámico

A diferencia de los rotadores de fondos de pantalla convencionales, el Companion destaca por su enfoque arquitectónico de clonación al vuelo:

* **Clonación en Caché:** El software **nunca altera tus archivos originales** en el disco duro. Cuando se cumple el intervalo de tiempo para cambiar el fondo de pantalla, el motor toma el archivo original de tu colección, genera una copia temporal en memoria/caché, le aplica las transformaciones geométricas heredadas del Master (*Crop* y *Flip*) junto con los efectos visuales activos, y le notifica a Windows que consuma ese clon procesado.
* **Aclaración Estética sobre los Filtros:** Los efectos de color (como Sepia, Blanco y Negro, etc.) se aplican mediante algoritmos matemáticos estándar. Debido a esto, el resultado visual dependerá enteramente de la iluminación, exposición y contraste del archivo original; **no todos los efectos lucirán bien en todas las imágenes**, quedando a discreción del usuario combinarlos de forma óptima.
* **Mapeo Automatizado de Contingencia:** Si el Companion apunta a una carpeta cuyo archivo `datos_carpeta.json` está recién creado (vacío, sin etiquetas ni ediciones de encuadre previas), o si el usuario simplemente decide no aplicar ningún filtro en la interfaz, el sistema activa una red de seguridad: importará **todas las imágenes del directorio** y les aplicará un *Crop* centrado automático por defecto para asegurar que el escritorio siempre se mantenga vestido.
---
# 2. Anatomía de la Interfaz y Módulos de Control

La interfaz del Companion está diseñada para ser compacta, funcional y altamente parametrizable. A diferencia del Master, aquí el foco no está en la edición individual, sino en la segmentación masiva del catálogo.
---
### 2.1 Las 5 Secciones de Parametrización

#### 1. Carpetas de Origen (Mega-Pool de Selección)
<div align="center">
<img width="756" height="79" alt="image" src="https://github.com/user-attachments/assets/aa1df105-0b83-4558-8270-a74f15fc1cd2" />
</div>
Este módulo te permite vincular una o varias rutas de forma simultánea, combinando catálogos para crear una gran lista de reproducción de wallpapers.
* **Carga desde el Historial:** Las carpetas se eligen directamente a partir del historial universal que ha registrado el Master.
* **Visualización Dinámica:** Las rutas activas se cargan visualmente en la interfaz como etiquetas (*labels*). Cada una cuenta con un pequeño icono de eliminación (**`X`**); al hacer clic en él, la carpeta se remueve de la rotación actual de manera instantánea.

#### 2. Switches de Calidad y Estado
<div align="center">
<img width="753" height="63" alt="image" src="https://github.com/user-attachments/assets/d9b444eb-3415-4cdd-90a4-57364f38c757" />
</div>
Selectores binarios (encendido/apagado) que dictan qué imágenes del archivo `datos_carpeta.json` tienen derecho a subir al escritorio. Para garantizar un flujo limpio por defecto, las opciones restrictivas o de descarte vienen desactivadas de fábrica:
* **Filtros de Calidad:** Aptas, Con Crop, LowRes *(Desactivado por defecto)*.
* **Filtros de Estado:** Favoritas *(Desactivado por defecto)*, Ignoradas *(Desactivado por defecto)*, Eliminar *(Desactivado por defecto)*.

#### 3. Filtros de Etiquetas (Inclusión / Exclusión)
<div align="center">
<img width="757" height="118" alt="image" src="https://github.com/user-attachments/assets/c78cd21e-b5c8-43f9-ba10-6053e9e09ff8" />
</div>
Diseñado para la segmentación temática mediante campos de texto libre (en esta sección no se cuenta con llenado predictivo):
* **Campo de Inclusión:** Escribe los tags de las imágenes que deseas ver en pantalla.
* **Campo de Exclusión:** Escribe los tags de los conceptos que quieres vetar por completo de tu escritorio.
* **Sintaxis Lógica:** Ambos campos heredan el motor lógico del Master. Utiliza el operador **`+`** para condiciones estrictas (Y) y la coma (**`,`**) para condiciones alternativas (O).

#### 4. Programación y Comportamiento del Sistema
<div align="center">
<img width="754" height="58" alt="image" src="https://github.com/user-attachments/assets/746d5819-ec8e-45df-bc7e-ae5c4aa51bcc" />
</div>
* **Intervalo de Tiempo:** Un cuadro numérico libre acompañado de un selector de unidades (**Minutos / Horas / Días**). Su diseño flexible te permite configurar desde cambios frenéticos cada pocos minutos hasta transiciones extremas (por ejemplo, cambiar el fondo cada 1000 días).
* **Modo Aleatorio:** Rompe el orden secuencial de los archivos y elige al azar la siguiente imagen que cumpla con los filtros establecidos.
* **Iniciar con Windows:** Al activar este switch, el Companion escribe automáticamente una clave en el Registro de Windows (`Run`) para asegurar su auto-arranque en segundo plano cada vez que enciendas la computadora, de forma transparente y sin requerir interacción.

#### 5. Filtros Matemáticos de Color (Efectos de Capa)
<div align="center">
<img width="748" height="71" alt="image" src="https://github.com/user-attachments/assets/38ab1330-5497-4a46-8f27-e95da70bbc59" />
</div>
Permite alterar artísticamente el clon temporal de la imagen antes de inyectarlo al sistema:
* **Monocromáticos:** Blanco y Negro (B&W) y Sepia.
* **Artísticos:** Efecto Lomo y Tonos Pastel.
* **Modo Aleatorio de Color:** Aplica un filtro diferente al azar en cada cambio de wallpaper (incluyendo la posibilidad de que la imagen se muestre limpia y sin filtros), logrando que tu biblioteca visual se sienta siempre fresca y variada.
> ⚠️ **Nota Importante sobre los Filtros de Color:**
> Los filtros artísticos se calculan de manera destructiva sobre el clon temporal de la imagen, por lo que **no pueden acumularse**. Cada efecto se aplica de forma estrictamente individual (por ejemplo, no es posible combinar *Sepia* con *Efecto Lomo* al mismo tiempo). Al seleccionar un filtro nuevo, este sustituirá por completo al anterior.
---

### 2.2 Controles de Operación y Monitoreo Inferior

* **6. Botón de Control de Servicio:** Un interruptor maestro rotulado como **Iniciar** o **Detener**. Permite congelar el temporizador del Companion o arrancar el ciclo de rotación con un solo clic.
* **7. Barra de Estado:** Ubicada en la base de la ventana, te muestra una miniatura en tiempo real del wallpaper que viste tu escritorio en ese instante y un contador digital que te indica exactamente **cuántas imágenes de las carpetas seleccionadas cumplen con los filtros actuales**. Si el contador marca cero, el servicio te lo advertirá visualmente.
<div align="center">
<img width="757" height="86" alt="image" src="https://github.com/user-attachments/assets/dd162f5c-c750-4ba1-a331-b120a532d155" />
</div>
