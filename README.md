# SolaraX2 — Versión 0.1

## Primera fase del proyecto

**SolaraX2 0.1** es la primera fase pública de este fork comunitario de un emulador de PlayStation 2 para Android. El proyecto se está retomando y reorganizando progresivamente sobre la base del código abierto de [izzy2lost/PSX2](https://github.com/izzy2lost/PSX2), con el núcleo de emulación derivado de [PCSX2](https://github.com/PCSX2/pcsx2).

Esta versión no representa el estado final del emulador. Es una base inicial funcional sobre la que se irán incorporando más mejoras, optimizaciones, compatibilidad, ajustes específicos por juego y refinamientos de la interfaz. El objetivo es avanzar por etapas, probar cada cambio en Android y mantener una ruta segura de fallback para no perder las funciones existentes.

> **Estado actual:** primera fase de desarrollo — versión `0.1`.

La APK no incluye juegos ni BIOS. El usuario debe utilizar únicamente archivos que tenga derecho a usar. SolaraX2 conserva el funcionamiento del emulador y añade una capa de interfaz, configuración y optimización orientada a Android.

## Descarga de esta versión

| Archivo | Descripción |
| --- | --- |
| [`SolaraX2-v0.1.apk`](./SolaraX2-v0.1.apk) | APK de la primera fase pública |
| [`SolaraX2-v0.1.apk.sha256`](./SolaraX2-v0.1.apk.sha256) | Hash SHA-256 de la APK |
| [`LICENSE.md`](./LICENSE.md) | Licencia GPLv3 |

### Descarga directa

[**Descargar SolaraX2 v0.1 directamente desde GitHub**](https://github.com/HUEVOMAN77/SolaraX2-Neon-Release/raw/refs/heads/main/SolaraX2-v0.1.apk)

**SHA-256:**

```text
cc67cd18f7fc5b8b5bf32d80da977d57b9d712b3b90f7be5583c7db001b6a114
```

## Cómo funcionará SolaraX2 en el teléfono

El funcionamiento general será el de un emulador tradicional de PS2, pero con una interfaz más organizada y herramientas adaptativas para Android. Después de instalar la APK, el usuario configurará una BIOS válida, seleccionará una carpeta de juegos y podrá importar sus imágenes de juego a la biblioteca.

La biblioteca mostrará los juegos detectados, permitirá buscarlos, ordenarlos mediante favoritos y reconocer los títulos jugados recientemente. Al seleccionar un juego se abrirá su pantalla de detalles y desde allí se podrá iniciar la emulación o volver a configurar sus opciones.

Durante la ejecución, los controles táctiles compactos aparecerán sobre el juego sin cubrir toda la pantalla. La distribución conserva la cruceta, el joystick analógico, los botones △ ○ × □, L1/L2, R1/R2, L3/R3, SELECT y START. También se mantienen las entradas de controles físicos cuando el teléfono reconoce un mando externo.

## Mejoras incluidas en la versión 0.1

### Interfaz inicial en español latino

La interfaz principal fue reorganizada como una biblioteca de juegos. La pantalla de inicio deja de depender de una tabla técnica como elemento principal y presenta carátulas, nombres, estados, búsqueda y acciones de biblioteca.

Se añadieron textos principales en español latino para que el usuario pueda localizar la BIOS, los juegos, las opciones gráficas, los controles, el sistema y las funciones avanzadas sin depender de una interfaz en inglés.

### Identidad visual SolaraX2

La aplicación utiliza el nombre exacto **SolaraX2** y una identidad visual propia. El icono conserva un diseño sencillo compuesto por un sol dorado y una X coral sobre un fondo azul oscuro, evitando una apariencia futurista excesiva.

### Tema neón para la biblioteca

La interfaz de la biblioteca incorpora un estilo oscuro con degradados de negro azulado, violeta y cian. Los elementos principales utilizan superficies profundas y acentos luminosos para diferenciar la biblioteca, las tarjetas de juegos, los botones de acción y los estados de selección.

El estilo busca que la aplicación se vea moderna sin sacrificar legibilidad. Los degradados se aplican como recursos nativos de Android, por lo que no dependen de una imagen externa ni añaden una carga gráfica innecesaria al juego.

### Controles táctiles compactos con estilo neón

Los controles táctiles fueron diseñados para conservar una distribución compacta, semejante a las interfaces prácticas de otros emuladores Android, sin convertirse en una marca de agua grande sobre la imagen.

Los botones tienen fondos translúcidos, bordes cian, magenta o violeta y un estado pulsado más luminoso. Los símbolos de PlayStation se mantienen separados, y el joystick muestra un anillo cian, detalles violetas y una perilla con acento magenta.

La apariencia visual no cambia el mapeo interno. Cada botón sigue enviando la misma entrada que antes, y todas las funciones originales del emulador permanecen disponibles.

### Personalización manual de controles

La primera fase incluye la base del editor manual de controles. Desde los ajustes se puede abrir **Editar controles táctiles**, activar el modo de edición y arrastrar los botones individualmente a una ubicación preferida.

Al soltar un botón, SolaraX2 guarda su posición en las preferencias de la aplicación. La personalización se aplica nuevamente al iniciar el juego y se puede borrar mediante **Restablecer controles**. Esta función cambia la posición visual, no la función del botón: mover △ no lo convierte en ○ ni modifica el mapeo del núcleo.

El editor seguirá ampliándose en fases posteriores para añadir más opciones de escala, organización por grupos, perfiles por orientación y controles de edición más detallados.

### Biblioteca con favoritos y recientes

Cada juego puede marcarse como favorito. Los favoritos se ordenan primero y los juegos jugados recientemente conservan su fecha de uso para facilitar el acceso al catálogo habitual.

La pantalla de detalles muestra el nombre del juego, su estado de disponibilidad, la condición de favorito y el botón para iniciar la emulación.

### Descarga automática de carátulas

Cuando se importa o escanea un juego, SolaraX2 intenta obtener su serial utilizando la información disponible del núcleo, el nombre del archivo o la ruta. Si el juego no tiene una carátula válida en la caché, se programa una descarga automática desde una colección pública organizada por serial.

El funcionamiento previsto en esta primera fase es el siguiente:

1. SolaraX2 detecta los juegos de la carpeta seleccionada.
2. Busca una carátula existente en la caché local y en el almacenamiento SAF.
3. Separa los juegos que todavía no tienen una carátula válida.
4. Programa la descarga en segundo plano únicamente cuando hay conexión disponible.
5. Valida la imagen descargada antes de guardarla definitivamente.
6. Actualiza la biblioteca cuando termina la descarga.

La opción **Descargar carátulas automáticamente** queda activada por defecto y puede desactivarse desde Ajustes. Las carátulas personalizadas se conservan y no deben reemplazarse automáticamente.

La colección pública de carátulas documenta rutas por serial para carátulas estándar y 3D, incluida la ruta `covers/3d/${serial}.png` [1]. Si un juego todavía no tiene imagen disponible, seguirá apareciendo en la biblioteca y se podrá jugar normalmente.

### Solarax SmartScale

**Solarax SmartScale** es la función adaptativa principal de esta línea de desarrollo. Su propósito es reducir temporalmente la resolución interna cuando el teléfono no puede sostener la meta de rendimiento elegida.

La escala interna puede moverse aproximadamente entre `0.5x` y `1.0x`, mientras la imagen se presenta al tamaño de la superficie Android. El usuario puede elegir metas de 30, 40, 50 o 60 FPS. La intención es priorizar estabilidad de frametime sobre nitidez interna cuando el hardware está limitado.

| Situación | Meta recomendada |
| --- | --- |
| Juego muy pesado o teléfono de gama baja | 30 FPS |
| Juego jugable pero irregular | 40 FPS |
| Juego relativamente estable | 50 FPS |
| Juego ligero o teléfono potente | 60 FPS |

SmartScale no garantiza una meta concreta para todos los juegos. La PS2 tiene títulos con cargas muy diferentes y algunos pueden necesitar ajustes propios. Esta función se seguirá calibrando en futuras versiones.

### Perfiles adaptativos para Android

SolaraX2 incluye perfiles que observan características generales del teléfono, como memoria disponible, CPU y familia Snapdragon/Adreno, para elegir valores iniciales más seguros.

En dispositivos cercanos a 4 GB de RAM se reducen de forma conservadora ciertos buffers de streaming Vulkan. El objetivo es disminuir la presión de memoria y evitar cierres por falta de recursos, aunque el resultado puede variar según la versión de Android y el driver del fabricante.

### Adaptive Core Governor

El gobernador adaptativo observa muestras reales de FPS, frametime, carga de CPU/EE, VU, GS, GPU y frecuencia de CPU cuando Android la expone. Con esos datos intenta clasificar si el cuello de botella principal está en el procesador, el renderizado o la memoria.

Las acciones experimentales tienen interruptores independientes y rutas de desactivación. No se pretende aplicar un hack universal que cambie la exactitud de la emulación. Si una función experimental provoca inestabilidad, el sistema de rescate puede desactivarla y volver a un perfil conservador.

### Thermal Guard y memoria Vulkan

Thermal Guard reduce temporalmente la meta de FPS cuando el teléfono informa calentamiento o una caída sostenida de frecuencia. Vulkan Memory Guardian observa la presión de memoria del sistema y el presupuesto de memoria Vulkan cuando el driver ofrece esa información.

Estas funciones buscan evitar que el teléfono llegue rápidamente a un estado de throttling térmico. No sustituyen una buena ventilación ni pueden eliminar las limitaciones físicas del dispositivo.

### Compatibilidad con Turnip

Turnip es relevante principalmente para teléfonos Snapdragon con GPU Adreno compatible. SolaraX2 incluye selección de driver Vulkan personalizado, validación básica de símbolos y fallback al driver Vulkan del sistema si Turnip no logra iniciar correctamente.

En teléfonos con MediaTek y GPU Mali, Turnip no corresponde. En esos equipos se recomienda utilizar Vulkan del sistema y, si fuera necesario, OpenGL Hardware. La aplicación no necesita ser Snapdragon para funcionar.

## Qué se conservará del emulador original

El objetivo de SolaraX2 no es eliminar funciones existentes, sino reorganizarlas y mejorarlas progresivamente. La base mantiene el núcleo de emulación y las opciones relacionadas con:

| Área | Estado en la versión 0.1 |
| --- | --- |
| BIOS | Se conserva la importación y verificación existente |
| Audio | Se conserva la ruta de configuración original |
| Controles | Se conserva el mapeo táctil y el soporte de controles externos |
| Estados guardados | Se conserva la gestión existente del emulador |
| Tarjetas de memoria | Se conserva el administrador del proyecto base |
| RetroAchievements | Se conserva la integración existente |
| Parches y opciones por juego | Se conservan para continuar reorganizándolos en próximas fases |
| Renderizadores | Se conservan Vulkan, OpenGL y Software cuando el dispositivo los expone |

## Primera fase y desarrollo futuro

La versión 0.1 debe entenderse como el inicio formal de SolaraX2, no como una edición terminada ni como una promesa de rendimiento perfecto. Primero se está tomando el proyecto, ordenando la interfaz, estabilizando la integración Android y construyendo una base de optimización que pueda medirse y revertirse.

El desarrollo continuará poco a poco. Las próximas fases podrán incluir un editor de controles más completo, perfiles visuales configurables, más fuentes de carátulas, mejor detección de seriales, ajustes específicos por juego, calibración de SmartScale, optimizaciones de memoria y pruebas ampliadas en Snapdragon 6, 7, 8 y dispositivos MediaTek/Mali.

Cada mejora deberá compilarse, validarse y conservar un fallback seguro antes de incorporarse a una Release. La prioridad será aumentar la estabilidad y la compatibilidad sin eliminar funciones del emulador ni alterar de forma irresponsable la exactitud del núcleo.

## Instalación básica

1. Descargá [`SolaraX2-v0.1.apk`](./SolaraX2-v0.1.apk) desde este repositorio.
2. Instalá la APK en un dispositivo Android compatible.
3. Configurá una BIOS válida desde los ajustes.
4. Agregá la carpeta donde tengas tus juegos.
5. Esperá el escaneo de la biblioteca.
6. Revisá SmartScale y el renderer recomendado para tu teléfono.
7. Si usás un Snapdragon compatible, probá Turnip únicamente después de confirmar que el driver corresponde a tu GPU Adreno.
8. Si usás MediaTek/Mali, comenzá con Vulkan del sistema u OpenGL Hardware.

## Verificación del archivo

En Linux, macOS o Termux se puede comprobar la APK con:

```bash
sha256sum -c SolaraX2-v0.1.apk.sha256
```

El resultado esperado es:

```text
SolaraX2-v0.1.apk: OK
```

## Licencia y código fuente

SolaraX2 se distribuye bajo la licencia **GPLv3**. El código fuente del fork se encuentra en [HUEVOMAN77/SolaraX2](https://github.com/HUEVOMAN77/SolaraX2). Este repositorio contiene la APK de la versión 0.1 y su documentación de distribución.

## Referencias

[1]: https://github.com/xlenore/ps2-covers "Colección pública de carátulas PS2 por serial"

[2]: https://github.com/izzy2lost/PSX2 "Proyecto Android PS2 utilizado como base del fork"

[3]: https://github.com/PCSX2/pcsx2 "Proyecto PCSX2 y núcleo de emulación de PlayStation 2"

[4]: https://www.gnu.org/licenses/gpl-3.0.html "Texto oficial de la GNU General Public License v3"
