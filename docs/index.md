# Firmware educativo para Kits Robóticos – PUCP

![MicroPython](https://img.shields.io/badge/MicroPython-1.20-blue.svg)
![Raspberry Pi Pico W](https://img.shields.io/badge/Raspberry%20Pi-Pico%20W-cc0000.svg)
![Licencia Académica PUCP](https://img.shields.io/badge/Licencia-PUCP--Académica-lightgrey.svg)

Este repositorio contiene el **firmware base desarrollado en MicroPython** para kits robóticos educativos utilizados en la carrera de Ingeniería Mecatrónica en la **Pontificia Universidad católica del Perú**. El proyecto está diseñado para facilitar el aprendizaje práctico de temas fundamentales en robótica móvil y robótica de manipuladores.

---

## Objetivos del proyecto
Desarrollar una plataforma de firmware modular y educativa que permita a los estudiantes:
!!! note annotate "Objetivos"
    - Comprender y experimentar con cinemática de robots móviles (diferencial, ackermann, mecanum).
    - Programar y controlar brazos robóticos.
    - Implementar algoritmos como "Go to Goal", planificación de trayectorias y filtros de Kalman.
    - Utilizar sensores reales (IMU, encoders, sensores ultrasónicos).
    - Familiarizarse con conceptos de navegación, control y percepción.

---

## Plataformas soportadas

- Robot con ruedas mecanum
- Brazos robóticos
- (Futuro) Vehiculo diferencial, ackerman, Robots con patas, LIDAR, otros sensores

---

## Estructura del repositorio

```
Software_Pico/
│
├── firmware/              ← Código fuente principal del firmware
│   ├── config/            ← Archivos de configuración (hardware, estudiantes)
│   ├── robot/             ← Implementaciones de los distintos robots
│   ├── sensors/           ← Interfaces para sensores (IMU, encoder, ultrasónicos)
│   ├── utils/             ← Utilidades compartidas (PID, secuencias, jacobianos)
│   └── libraries/         ← Librerías externas o wrappers (MQTT, IMU)
│
├── student_examples/      ← Ejemplos de código para uso en laboratorios
├── labs/                  ← Prácticas guiadas por tema o curso
├── tests/                 ← Scripts internos para pruebas de hardware/software
│   └── helpers/           ← Utilidades para pruebas
├── docs/                  ← Documentación técnica y guías de uso
│   └── hardware           ← Diagramas de conexiones y specificaciones
│   └── modules            ← Documentacion de modulos para uso de estudiantes
└── dev_tools/             ← Scripts para compilación, flasheo, etc.
```

---

## Guía de Inicio para Estudiantes

Sigue estos pasos en orden para configurar tu robot desde cero y dejarlo listo para los laboratorios.

### Parte 1: Preparación del Entorno

En esta parte, instalarás todo el software necesario en tu computadora y en la placa Pico W.

*   **Paso 1: Instalar el Firmware en la Pico W**
    *   Sigue las instrucciones de la **[Guía 1: Instalación del Firmware](guides/micropython_guide.md)** para preparar tu placa.

*   **Paso 2: Ejecutar tu Primer Programa**
    *   Aprende a usar Thonny con la **[Guía 2: Tu primer programa con Thonny](guides/thony_guide.md)**.

*   **Paso 3: Cargar los Archivos del Robot**
    *   Transfiere las librerías a tu placa siguiendo la **[Guía 3: Carga de archivos base](guides/base_guide.md)**.

---
### Parte 2: Configuración y Verificación del Robot

Una vez finalizada la configuración del entorno, el siguiente paso es la calibración de los motores para asegurar su correcto funcionamiento.

*   **Paso 4: Verificación y Ajuste de la Dirección de los Motores**

    Se debe seguir un proceso iterativo de prueba y ajuste para cada motor del robot.

    1.  **Abrir el script de diagnóstico:** Mediante Thonny, abra el archivo `1_test_wheel_direction.py`, ubicado en el directorio `student_examples/` de su proyecto local.

    2.  **Seleccionar el motor a probar:** En el código fuente del script, modifique el valor del parámetro `motor_id` en la llamada a la función `test_wheel_direction()`. Asigne el índice del motor que desea verificar (p. ej., `motor_id=0` para el primer motor).

    ```py
        # En el archivo 1_test_wheel_direction.py
        ROBOT_TYPE = 'test'
        # Inicializa la instancia del robot con los parámetros correspondientes
        robot = get_robot(ROBOT_TYPE, CONFIG[ROBOT_TYPE])

        # Ejecuta la prueba en el motor con índice 1
        # Realizar la prueba con cada motor y modificar la configuración
        # en config.py según corresponda
        test_wheel_direction(robot, motor_id=1)
    ```

    3.  **Ejecutar la prueba:** Ejecute el script en Thonny (▶). Observe el comportamiento físico de la rueda seleccionada y la información de diagnóstico que se imprime en la consola.

    4.  **Aplicar correcciones (si es necesario):** Si el comportamiento observado no es el esperado, abra el archivo de configuración `/config/student_config.py` ubicado en la memoria de la Raspberry Pi Pico.

        !!! danger "Advertencia Importante"
            **No modifiques `config.mpy`** — este archivo está protegido y contiene la configuración base. Modifica únicamente `student_config.py`.

        Aplique los siguientes ajustes según el caso:
        *   **Rotación del motor invertida:** Si el motor gira en la dirección opuesta a la esperada, añada el parámetro `"inverted": True` al diccionario del motor correspondiente.
        *   **Lectura del encoder invertida:** Si la consola indica que la lectura del encoder es incorrecta, añada el parámetro `"encoder_inverted": True`.
        *   **Operación correcta:** Si el motor funciona correctamente, el diccionario correspondiente debe permanecer vacío (`{}`).

        ```python
        # Ejemplo de aplicación de correcciones en /config/student_config.py
        MOTOR_DIRECTION = [
            {"inverted": True},          # Motor 0: requería inversión de giro.
            {},                          # Motor 1: operaba correctamente.
            {"encoder_inverted": True},  # Motor 2: requería inversión de la lectura del encoder.
            # ... y así sucesivamente.
        ]
        ```

    5.  **Guardar y repetir el proceso:** Guarde los cambios en el archivo `student_config.py` y repita los pasos 2 a 4 para cada uno de los motores del robot.

!!! note "Documentación Detallada"
    Para una explicación exhaustiva de los parámetros de configuración, incluyendo diagramas y ejemplos visuales de cada caso de prueba, consulte la siguiente guía:
    ➡️ **[Guía de Configuración y Calibración de Motores](configure/motor_config_guide.md)**

---

## Laboratorios incluidos

| Carpeta                   | Tema                       |
| ------------------------- | -------------------------- |
| `labs/pid_speed`          | Control PID de velocidad   |
| `labs/go_to_goal`         | Movimiento hacia un objetivo (Go-to-Goal)      |
| `labs/trajectory`         | Planificación de trayectorias |
| `labs/kalman`             | Estimación de estado con Filtro de Kalman           |
| `labs/manipulators`       | Cinemática de manipuladores |

---

## Versionado

Cada semestre académico se etiqueta una versión estable del repositorio.

!!! info "Ejemplos de etiquetas (`tags`)"

    Las versiones estables siguen el formato `v<año>-<semestre>-labkit`.

    *   `v2025-1-labkit` → Semestre **2025-1**
    *   `v2024-2-labkit` → Semestre **2024-2**

Para ver y utilizar una versión anterior, puedes usar los siguientes comandos:
```bash
git tag                
git checkout v2024-2-labkit
```

1.  **Listar versiones:** El comando `git tag` te mostrará todas las etiquetas disponibles en el historial del proyecto.
2.  **Cambiar de versión:** Una vez que identifiques la etiqueta que necesitas, `git checkout` te permite "viajar en el tiempo" a ese punto exacto del código.

---

## Organización del Desarrollo

Las contribuciones del equipo se organizan a través de las siguientes ramas principales:

!!! tip "Flujo de Ramas en Git"

    *   `main` — Versión estable.

    *   `dev` — Desarrollo activo.  

    *   `feature/<nombre>` — Funcionalidades nuevas en desarrollo.

    *   `course/<curso>` — Adaptaciones específicas para cursos o prácticas  

---

## Licencia

Este proyecto es de uso académico exclusivo para cursos dictados en la PUCP.  
Para solicitudes de uso externo, contactar con el equipo docente o coordinador del proyecto.

---

## Contacto

Para dudas, soporte o sugerencias:

- **Coordinador técnico:** [dequiroz@pucp.edu.pe] 
- **Repositorio oficial:** <https://github.com/PUCP-Robotica-IA/Software_Pico>

