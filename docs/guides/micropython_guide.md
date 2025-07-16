# Guía de Instalación del Firmware

Sigue estos tres pasos para preparar tu placa **Raspberry Pi Pico W** para el laboratorio.

!!! note "Requisitos"
    -  Una placa **Raspberry Pi Pico W**.
    -  Un **cable de datos** micro-USB.
    -  El editor **[Thonny IDE](https://thonny.org/)** instalado.

---

### Paso 1: Descargar el Firmware

Primero, obtén el archivo de firmware oficial de MicroPython, descargar la última versión del firmware.

[ **Firmware MicroPython para Pico W (.uf2)**](https://www.micropython.org/download/RPI_PICO_W/)

Guarda este archivo en tu escritorio o en un lugar fácil de encontrar.

---

### Paso 2: Instalar el Firmware en la Placa

Ahora, vamos a "flashear" el firmware en la memoria del Pico.

1.  **Mantén presionado** el botón **`BOOTSEL`** de tu Pico.

![Diagrama del proceso de flasheo](https://projects-static.raspberrypi.org/projects/get-started-pico-w/dd582d22736dc24fce9ad03b5f9f69b64fa6408c/en/images/bootsel.png)
*<p align="center" ><strong>Imagen:</strong> Botón BOOTSEL</p>*

2.  **Sin soltarlo**, conecta el Pico a tu computadora.
3.  Aparecerá una unidad llamada `RPI-RP2`. Ahora **suelta** el botón `BOOTSEL`.
4.  **Arrastra y suelta** el archivo `.uf2` que descargaste sobre esa unidad `RPI-RP2`.

!!! success "¡Firmware Instalado!"
    La placa se reiniciará sola y la unidad desaparecerá. Esto es normal.



---

### Paso 3: Subir los Archivos del Curso

Finalmente, carga el código del laboratorio usando Thonny.

1.  Abre **Thonny** y conecta tu Pico (de forma normal, sin `BOOTSEL`).
2.  Verifica que Thonny detecte el Pico en el menú inferior derecho (`MicroPython (Raspberry Pi Pico)`).

*<figure markdown="span" align="center">
  ![Image title](https://projects-static.raspberrypi.org/projects/get-started-pico-w/dd582d22736dc24fce9ad03b5f9f69b64fa6408c/en/images/thonny-select-interpreter.png)
  <figcaption><strong>Imagen:</strong> Botón BOOTSEL</figcaption>
</figure>*

3.  Ve a `Ver > Archivos` para mostrar el explorador de archivos.
4.  Busca la carpeta `firmware/` de nuestro proyecto a la izquierda, hazle clic derecho y selecciona **`Subir a /`** (`Upload to /`).

!!! danger "Instrucción Crítica"
    Asegúrate de subir la **carpeta `firmware` completa**, no solo los archivos que contiene. La estructura del proyecto es esencial para que funcione.

---

### ¡Listo!

Tu placa está preparada. Ya puedes cargar los ejemplos a la Raspberry Pi Pico W.