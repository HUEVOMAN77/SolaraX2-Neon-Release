# SolaraX2 Neon Release

**SolaraX2** es un fork comunitario de un emulador de PlayStation 2 para Android basado en el proyecto [izzy2lost/PSX2](https://github.com/izzy2lost/PSX2) y en el núcleo de emulación derivado de [PCSX2](https://github.com/PCSX2/pcsx2). Esta publicación contiene una APK Release compilada desde el fork público [HUEVOMAN77/SolaraX2](https://github.com/HUEVOMAN77/SolaraX2), rama `feature/adaptive-turnip-profiles`, commit `d526d097`.

La versión se enfoca en una experiencia moderna para Android: biblioteca de juegos con carátulas, interfaz en español latino, tema neón con degradados, controles táctiles compactos, perfiles adaptativos de rendimiento, compatibilidad con drivers Turnip en dispositivos Snapdragon compatibles y la función **Solarax SmartScale**.

> **Importante:** SolaraX2 es un emulador. No incluye juegos, BIOS ni ROMs comerciales. El usuario debe utilizar únicamente BIOS, imágenes de juegos y archivos que tenga derecho a usar conforme a la legislación de su país.

## Descarga

| Archivo | Descripción |
| --- | --- |
| [`SolaraX2-neon-release.apk`](./SolaraX2-neon-release.apk) | APK Release para instalar en Android |
| [`SolaraX2-neon-release.apk.sha256`](./SolaraX2-neon-release.apk.sha256) | Hash SHA-256 para verificar la integridad |
| [`LICENSE.md`](./LICENSE.md) | Licencia GPLv3 heredada del proyecto fuente |

**SHA-256 de la APK:**

```text
9719c56e2eea65f9aa3d7636748546a67861347993cea249d81b90f3df20888d
```

## Requisitos y compatibilidad

La APK está orientada a dispositivos Android arm64-v8a modernos. El rendimiento real depende del juego, la temperatura, la velocidad de almacenamiento, la configuración gráfica y la potencia del teléfono. La emulación de PS2 es exigente; por eso ningún perfil puede garantizar que todo el catálogo funcione de 30 a 60 FPS en todos los dispositivos.

| Tipo de dispositivo | Recomendación |
| --- | --- |
| Snapdragon 8 | Vulkan del sistema o Turnip compatible; se puede probar una resolución interna mayor cuando el juego sea estable |
| Snapdragon 7 | Vulkan y perfil adaptativo; SmartScale puede priorizar 40, 50 o 60 FPS según la carga |
| Snapdragon 6 | Priorizar Vulkan estable, SmartScale, perfil de baja memoria y metas de 30 o 40 FPS |
| Android con 4 GB de RAM | Usar resolución interna baja, buffers adaptativos y cerrar aplicaciones en segundo plano |
| MediaTek/Mali, incluido MT6768 | Turnip no aplica porque es un driver específico de Adreno; usar Vulkan del sistema u OpenGL Hardware |
| Dispositivo sin Vulkan funcional | Probar OpenGL Hardware; Software queda como opción de compatibilidad, pero normalmente será más lento |

La aplicación no requiere que el teléfono sea Snapdragon para funcionar. Turnip solamente aparece como una opción útil cuando el hardware utiliza una GPU Adreno compatible con drivers Turnip. En un Xiaomi MediaTek con GPU Mali se debe utilizar Vulkan del sistema u OpenGL.

## Instalación

Descargá `SolaraX2-neon-release.apk` desde este repositorio y abrí el archivo desde el administrador de archivos de Android. Si Android lo solicita, autorizá temporalmente la instalación desde esa fuente. Después de instalar, se recomienda volver a desactivar ese permiso.

Al abrir SolaraX2 por primera vez, configurá la BIOS verificada, agregá una carpeta de juegos y esperá a que termine el escaneo. La aplicación conserva las funciones existentes del emulador, incluyendo BIOS, audio, controles, estados guardados, tarjetas de memoria, RetroAchievements, parches y opciones avanzadas.

## Flujo de uso en el teléfono

### 1. Configurar la BIOS

La BIOS no se distribuye con SolaraX2. Desde el centro de ajustes, importá una BIOS que tengas derecho a utilizar. El verificador de BIOS muestra el estado de las regiones reconocidas y evita presentar una configuración como lista cuando falta un archivo válido.

### 2. Importar o agregar juegos

Desde la biblioteca, elegí **Agregar carpeta** y seleccioná la carpeta donde guardás tus imágenes de juegos. El escaneo admite las extensiones configuradas por el proyecto, como `.iso`, `.bin`, `.img`, `.mdf`, `.nrg`, `.chd`, `.cso`, `.zso`, `.gz` y archivos arcade compatibles.

La biblioteca conserva favoritos y juegos recientes. Los favoritos aparecen primero y los juegos jugados recientemente se ordenan por último uso.

### 3. Carátulas automáticas

Cuando SolaraX2 encuentra un juego sin carátula válida, resuelve su serial mediante el núcleo, el nombre del archivo o la ruta disponible. Después encola una descarga en segundo plano desde la colección pública de carátulas 3D utilizada por el proyecto. La colección documenta rutas basadas en serial, incluyendo el patrón de carátulas 3D `covers/3d/${serial}.png` [1].

El proceso funciona de la siguiente manera:

1. Se escanea la biblioteca y se identifica cada juego.
2. Se consulta primero la caché local y el almacenamiento SAF.
3. Solo los seriales que no tienen una imagen PNG válida se agregan a la descarga.
4. La tarea espera una conexión de red disponible y procesa los juegos en lotes.
5. La imagen se descarga a un archivo temporal, se valida como PNG y recién después se confirma en la caché.
6. Al terminar la tarea, la biblioteca se actualiza automáticamente.

Las carátulas personalizadas no se reemplazan si están marcadas como tales. La descarga automática se puede desactivar desde **Ajustes → Descargar carátulas automáticamente**. Si no hay conexión, el juego sigue funcionando con el estado vacío o con la carátula local disponible.

## Solarax SmartScale

**Solarax SmartScale** adapta la resolución interna durante la ejecución. Puede reducir la escala interna entre aproximadamente **0.5x y 1.0x** para intentar sostener una meta seleccionada de **30, 40, 50 o 60 FPS**. El framebuffer se presenta posteriormente al tamaño de la superficie Android, por lo que la imagen ocupa la pantalla configurada aunque el renderizado interno sea menor.

SmartScale no crea detalle que no exista en el renderizado interno ni transforma mágicamente un juego lento en uno rápido. Su objetivo es intercambiar parte de la nitidez interna por estabilidad de frametime. La recomendación práctica es la siguiente:

| Rendimiento observado | Meta sugerida |
| --- | --- |
| Juego pesado en gama baja | 30 FPS |
| Juego jugable pero irregular | 40 FPS |
| Juego relativamente estable | 50 FPS |
| Juego ligero o dispositivo potente | 60 FPS |

El controlador utiliza muestras reales de FPS y frametime, aplica histéresis para evitar cambios constantes y considera información térmica y de memoria. Si el teléfono se calienta o la frecuencia cae, Thermal Guard puede reducir temporalmente la meta para evitar tirones y sobrecalentamiento.

## Optimización adaptativa

La APK incluye perfiles que intentan seleccionar valores seguros según RAM, CPU, familia Snapdragon/Adreno y presión de memoria. Las funciones principales son:

| Función | Comportamiento |
| --- | --- |
| Perfil adaptativo Snapdragon | Detecta la plataforma y aplica valores conservadores para Snapdragon 6, 7 y 8 |
| Perfil de baja memoria | Reduce buffers de streaming Vulkan en dispositivos cercanos a 4 GB de RAM |
| Adaptive Core Governor | Observa frametime, CPU/EE, VU, GS, GPU y frecuencia disponible para clasificar cuellos de botella |
| Afinidad cooperativa | Puede mover el hilo EE hacia núcleos adecuados cuando se detecta saturación persistente; tiene interruptor independiente |
| Thermal Guard | Baja temporalmente la meta cuando Android reporta calentamiento o pérdida de frecuencia |
| Vulkan Memory Guardian | Consulta presión de memoria y presupuesto VMA cuando el driver lo expone |
| Caché de shaders | Conserva el pipeline cache durante la sesión para reducir recompilaciones repetidas |
| Solarax Guardian | Registra fallos de arranque por juego y activa un perfil de rescate conservador tras fallos repetidos |
| Perfiles por juego | Aprende una meta estable por identidad de juego sin modificar BIOS, controles o audio |

Estas funciones tienen rutas de desactivación y fallback. No se aplican hacks universales destinados a alterar la exactitud global de la emulación. Las funciones experimentales pueden desactivarse desde ajustes avanzados.

## Turnip y Vulkan

Turnip es un driver Vulkan alternativo orientado principalmente a GPUs Adreno. SolaraX2 incluye selección de driver personalizado, validación de símbolos Vulkan y fallback automático al driver del sistema si el driver seleccionado no puede inicializarse.

Para usarlo en un Snapdragon compatible:

1. Abrí **Ajustes → Turnip / Driver GPU personalizado**.
2. Importá o seleccioná el driver compatible con tu dispositivo.
3. Elegí Vulkan como renderizador.
4. Reiniciá el juego y comprobá estabilidad, temperatura y frametime.
5. Si no inicia o aparecen errores gráficos, regresá a **Driver del sistema**.

En dispositivos Mali, como el Xiaomi MediaTek MT6768, Turnip no es aplicable. En esos teléfonos la selección recomendada es **Vulkan del sistema** y, si presenta problemas, **OpenGL Hardware**.

## Tema neón y controles táctiles

La biblioteca utiliza un fondo oscuro con degradados entre negro azulado, violeta y cian. Los controles mantienen una distribución compacta para no cubrir toda la pantalla y usan bordes luminosos con transparencias suaves. Los botones de PlayStation conservan sus símbolos △, ○, × y □, mientras que la cruceta, los gatillos, SELECT/START y los joysticks permanecen separados y legibles.

### Personalizar posiciones

Para mover los controles manualmente:

1. Abrí **Ajustes** desde la biblioteca o desde el menú del juego.
2. Entrá en **Editar controles táctiles**.
3. Presioná **Comenzar edición**.
4. Arrastrá cada botón a la posición que prefieras.
5. Soltá el botón para guardar automáticamente su posición.
6. Para volver a la distribución original, elegí **Restablecer controles**.

El editor cambia la posición visual, no el mapeo interno de las entradas. Por lo tanto, mover un botón no cambia la función que ejecuta: △, ○, ×, □, L1, R1, SELECT, START y los demás controles conservan sus asignaciones.

## Solución de problemas

| Problema | Acción recomendada |
| --- | --- |
| El juego funciona lento | Activá SmartScale, elegí 30 o 40 FPS, usá Vulkan y cerrá aplicaciones en segundo plano |
| El teléfono se calienta | Bajá la meta de FPS, usá resolución interna menor y dejá que Thermal Guard actúe |
| Turnip no aparece o falla | Confirmá que el dispositivo tenga Adreno; en Mali usá Vulkan del sistema u OpenGL |
| La carátula no aparece | Verificá la conexión, el serial del archivo y que la descarga automática esté activa; también podés reintentar desde la gestión de carátulas |
| La biblioteca está vacía | Volvé a agregar la carpeta mediante el selector de almacenamiento y otorgá el permiso persistente |
| Los controles quedaron desordenados | Abrí el editor y seleccioná **Restablecer controles** |
| El juego no arranca | Comprobá la BIOS, probá el renderer del sistema, desactivá funciones experimentales y permití que Solarax Guardian use el perfil de rescate |
| Hay tirones después de cambiar de juego | Reiniciá la ejecución del juego para que el pipeline cache y el perfil por juego se estabilicen |

## Alcance y limitaciones

SolaraX2 mejora la interfaz, la gestión de perfiles, la adaptación de resolución y la experiencia de uso, pero no puede eliminar las limitaciones físicas del teléfono ni garantizar compatibilidad perfecta con cada título. La velocidad puede variar considerablemente entre escenas del mismo juego. Algunos juegos requieren ajustes específicos de renderer, blending, VSync, parches o resolución.

La carátula automática depende de que exista una imagen para el serial correspondiente en la fuente pública. Si un juego no tiene carátula en esa colección, se conserva el estado sin carátula y el emulador sigue permitiendo jugarlo.

## Licencia y código fuente

SolaraX2 se distribuye bajo **GPLv3**. El código fuente y el historial de modificaciones están disponibles en el fork público [HUEVOMAN77/SolaraX2](https://github.com/HUEVOMAN77/SolaraX2). Esta publicación separada sirve como distribución de la APK Release y su documentación.

## Referencias

[1]: https://github.com/xlenore/ps2-covers "xlenore/ps2-covers — colección pública de carátulas PS2"

[2]: https://github.com/izzy2lost/PSX2 "izzy2lost/PSX2 — proyecto Android PS2 utilizado como base del fork"

[3]: https://github.com/PCSX2/pcsx2 "PCSX2 — núcleo y proyecto de emulación de PlayStation 2"

[4]: https://www.gnu.org/licenses/gpl-3.0.html "GNU General Public License, versión 3"
