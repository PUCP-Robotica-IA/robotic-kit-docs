# Clase robot

`class MobileRobot(motor_config)`

Clase base para un robot móvil con múltiples motores controlados por PID. Representa una plataforma genérica de robot móvil que permite el control de múltiples motores, integración de modelos cinemáticos personalizados (jacobianos), actualización periódica mediante temporizador y ajuste de controladores PID por motor.

Nota: Admite robots de tipo diferencial y mecanum u otras arquitecturas que
compartan el mismo esquema de control individual por rueda.

Parametros:

* `motor_configs : dict`

  Lista de diccionarios con los parámetros de configuración de cada motor.
  Cada diccionario debe incluir al menos:
  
Metodos:

* `move(self, vx, vy, omega)`
* `stop()`
* `enable_auto_update(self, interval=10)`
* `_update_motors()`
* `set_custom_jacobian(func)`
* `_jacobian()`
* `default_jacobian()`
* `_compute_wheel_speeds(vx, vy, omega)`
* `update_odometry()`
* `set_control_mode()`
* `set_pid_constants(motor_index, kp)`

Ejemplos:

    from config import CONFIG
    from robot.base import MobileRobot

    robot = MobileRobot(config)
    robot.move(vx=0.2, vy=0.0, omega=0.1)

