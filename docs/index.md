# Firmware Educativo para Kits Robóticos – PUCP

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

## Plataformas Soportadas

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

## Inicio rápido: Cómo Usar el Firmware

### 1. Flashear el Raspberry Pi Pico W

Sigue las instrucciones del archivo `docs/guia_instalacion.md` para instalar MicroPython y cargar los archivos necesarios.

### 2. Configurar tu robot

Modifica únicamente el archivo **`firmware/config/student_config.py`** para definir parámetros ajustables por el usuario.

```python
MOTOR_DIRECTION = [
    {"encoder_inverted": True},                   # Motor 0
    {"inverted": True},                           # Motor 1
]
```

!!! danger "Advertencia Importante"
    **No modifiques `config.mpy`** — este archivos está protegido para evitar daños al hardware.

### 3. Ejecutar un script de ejemplo

Desde Thonny, puedes ejecutar, por ejemplo:

```python

# Función de diagnóstico para verificar sentido de giro y lectura del encoder
from tests.helpers.motor import test_wheel_direction
# Diccionario de configuración que contiene parámetros del robot
from config import CONFIG
# Función que retorna una instancia del robot basado en el tipo
from robot import get_robot

#=========================================================
# Selección del tipo de robot a utilizar en el test.
# Debe de estar definido el config.py
#=========================================================
ROBOT_TYPE = 'test'
# Inicializa la instancia del robot con los parámetros correspondientes
robot = get_robot(ROBOT_TYPE, CONFIG[ROBOT_TYPE])

# Ejecuta la prueba en el motor con índice 1
# Realizar la prueba con cada motor y modificar la configuración
# en config.py según corresponda
test_wheel_direction(robot, motor_id=1)

```

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

