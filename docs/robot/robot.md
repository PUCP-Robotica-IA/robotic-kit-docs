# Clase `robot`

Antes de iniciar el proyecto, es necesario definir la clase base del robot que se utilizará. Esta clase debe ser capaz de manejar diferentes configuraciones de hardware y proporcionar una interfaz común para interactuar con los motores y sensores.

---

## PASO 1: Definir la clase base del robot

En primer lugar, es necesario importar el método `get_robot` de la librería `robot`. Este método permite obtener una instancia del robot según el tipo de robot y su configuración. Cada configuración depende del tipo de robot, por lo que se sugiere revisar la documentación de [`configure`](../configure/configure.md) para entender las diferentes configuraciones disponibles.

A continuación se muestra un ejemplo de cómo definir la clase base del robot utilizando el método `get_robot` para crear una instancia del robot mecanum:

!!! tip "Ejemplo de inicialización"

    Este bloque de código crea una instancia del robot tipo mecanum usando la configuración definida en `CONFIG`:

    ```python
    from config import CONFIG
    from robot import get_robot

    ROBOT_TYPE = 'mecanum'
    robot = get_robot(ROBOT_TYPE, CONFIG[ROBOT_TYPE])
    ```

---

## PASO 2: Controlar el robot

Luego de llamar a `get_robot`, se puede utilizar la instancia del robot para controlar sus motores y sensores. Por ejemplo:

!!! tip "Ejemplo de uso de metodo `move`"

    ```python
    robot.move(vx=0.5, vy=0.0, omega=0.1)
    ```

---

## Métodos asociados a la clase base del robot

### Funciones relacionadas con el movimiento del robot

#### ROBOT.MOVE
*`robot.move(vx, vy, omega)`*

Calcula y aplica velocidades individuales a las ruedas a partir de velocidades del chasis.

**Parámetros:**

- `vx` (*float*): Velocidad lineal en eje X [m/s]
- `vy` (*float*): Velocidad lineal en eje Y [m/s]
- `omega` (*float*): Velocidad angular del chasis [rad/s]

**Ejemplo:**

!!! tip "Ejemplo de uso de metodo `move`"

    Este comando permite mover el robot con una velocidad lineal de 0.5 m/s en el eje X, sin movimiento en el eje Y, y con una rotación angular de 0.1 rad/s.

    ```python
    robot.move(vx=0.5, vy=0.0, omega=0.1)
    ```


#### ROBOT.STOP
*`robot.stop()`*

Detiene el robot móvil, estableciendo todas las velocidades a cero.

!!! tip "Ejemplo de uso de metodo `stop`"

    Este comando detiene completamente el movimiento del robot.
    ```python
    robot.stop()
    ```

#### ROBOT.SET_CUSTOM_JACOBIAN
*`robot.set_custom_jacobian(func)`*

Define una función externa para calcular el jacobiano personalizado.

**Parámetros:**

- `func` (*callable*): Función que retorna una matriz jacobiana (lista de listas)

!!! tip "Ejemplo de uso de metodo `set_custom_jacobian`"

    Este comando permite definir un jacobiano personalizado para el robot, útil en aplicaciones específicas.

    ```python
    def my_jacobian():
        return [[1, 0, -1], [1, 0, 1], [1, 0, 1], [1, 0, -1]]

    robot.set_custom_jacobian(my_jacobian)
    ```

---

### Funciones relacionadas con el control en lazo cerrado

#### ROBOT.SET_CONTROL_MODE
*`robot.set_control_mode(closed_loop=False)`*

Activa o desactiva el control en lazo cerrado (PID) en todos los motores.

**Parámetros:**

- `closed_loop` (*bool*): `True` para habilitar PID, `False` para desactivar

!!! tip "Ejemplo de uso de metodo `set_control_mode`"

    Este comando activa el control PID en todos los motores del robot.
    ```python
    robot.set_control_mode(closed_loop=True)
    ```

#### ROBOT.SET_PID_CONSTANTS
*`robot.set_pid_constants(motor_index, kp, ki=None, kd=None)`*

Configura los parámetros PID de un motor en específico.

**Parámetros:**

- `motor_index` (*int*): Índice del motor en la lista `robot.motors`
- `kp` (*float*): Constante proporcional
- `ki` (*float*): Constante integral (opcional)
- `kd` (*float*): Constante derivativa (opcional)

!!! tip "Ejemplo de uso de metodo `set_pid_constants`"

    Este comando ajusta los parámetros PID del primer motor del robot.
    ```python
    robot.set_pid_constants(motor_index=0, kp=1.2, ki=0.5, kd=0.05)
    ```

#### ROBOT.ENABLE_AUTO_UPDATE
*`robot.enable_auto_update(interval=10)`*

Habilita la actualización periódica de los motores usando un `Timer`.

**Parámetros:**

- `interval` (*int*): Periodo de actualización en milisegundos (por defecto 10 ms)

!!! tip "Ejemplo de uso de metodo `enable_auto_update`"

    Este comando activa la actualización automática de los motores cada 20 ms.
    ```python
    robot.enable_auto_update(interval=20)
    ```

---

### Funciones relacionadas con los motores individuales

#### ROBOT.MOTORS.ID.SET_SPEED
*`robot.motors[id].set_speed(speed_rps)`*

Establece la velocidad objetivo del motor en revoluciones por segundo (rps).

!!! tip "Ejemplo de uso de metodo `set_speed`"

    Este comando establece la velocidad del primer motor a 10.0 rps.
    ```python
    robot.motors[0].set_speed(10.0)
    ```

#### ROBOT.MOTORS.ID.STOP
*`robot.motors[id].stop()`*

Detiene el motor individual.

!!! tip "Ejemplo de uso de metodo `stop`"

    Este comando detiene el segundo motor del robot.
    ```python
    robot.motors[1].stop()
    ```

#### ROBOT.MOTORS.ID.GET_SPEED
*`robot.motors[id].get_speed()`*

Retorna la velocidad actual del motor.

!!! tip "Ejemplo de uso de metodo `get_speed`"

    Este comando obtiene la velocidad actual del tercer motor.
    ```python
    vel = robot.motors[2].get_speed()
    ```

#### ROBOT.MOTORS.ID.GET_STATE
*`robot.motors[id].get_state()`*

Retorna un diccionario con información del estado del motor (velocidad, posición, PID, etc).

!!! tip "Ejemplo de uso de metodo `get_state`"

    Este comando imprime el estado del cuarto motor, incluyendo velocidad y posición.
    ```python
    print(robot.motors[3].get_state())
    ```

#### ROBOT.MOTORS.ID.ENABLE_CLOSE_LOOP_CONTROL
*`robot.motors[id].enable_close_loop_control(True)`*

Activa el control PID para ese motor.

!!! tip "Ejemplo de uso de metodo `enable_close_loop_control`"

    Este comando activa el control PID en el primer motor del robot.
    ```python
    robot.motors[0].enable_close_loop_control(True)
    ```

#### ROBOT.MOTORS.ID.TUNE_PID
*`robot.motors[id].tune_pid(kp, ki, kd)`*

Ajusta los parámetros PID para un motor específico.

!!! tip "Ejemplo de uso de metodo `tune_pid`"

    Este comando ajusta los parámetros PID del primer motor a kp=1.0, ki=0.1, kd=0.01.
    ```python
    robot.motors[0].tune_pid(kp=1.0, ki=0.1, kd=0.01)
    ```

---

### Funciones relacionadas con la lectura de sensores del robot

#### ROBOT.SENSORS.READ_IMU_THETA
*`robot.sensors.read_imu_theta()`*

Devuelve el ángulo de orientación estimado por el IMU (en radianes).

!!! tip "Ejemplo de uso de metodo `read_imu_theta`"

    Este comando obtiene el ángulo de orientación del robot desde el IMU.
    ```python
    theta = robot.sensors.read_imu_theta()
    ```

#### ROBOT.SENSORS.READ_IMU_VALUES
*`robot.sensors.read_imu_values()`*

Retorna los valores del IMU (acelerómetro y giróscopo).

!!! tip "Ejemplo de uso de metodo `read_imu_values`"

    Este comando obtiene los valores del IMU, incluyendo aceleración y velocidad angular.
    ```python
    imu_data = robot.sensors.read_imu_values()
    ```

#### ROBOT.SENSORS.READ_ULTRASONIC_VALUE
*`robot.sensors.read_ultrasonic_value(sensor_id)`*

Retorna la distancia medida por un sensor ultrasónico específico.

!!! tip "Ejemplo de uso de metodo `read_ultrasonic_value`"

    Este comando obtiene la distancia medida por el primer sensor ultrasónico.
    ```python
    distancia = robot.sensors.read_ultrasonic_value(sensor_id=0)
    ```

#### ROBOT.SENSORS.READ_ULTRASONIC_ALL
*`robot.sensors.read_ultrasonic_all()`*

Retorna una lista con las mediciones de todos los sensores ultrasónicos.

!!! tip "Ejemplo de uso de metodo `read_ultrasonic_all`"

    Este comando obtiene las distancias medidas por todos los sensores ultrasónicos del robot.
    ```python
    distancias = robot.sensors.read_ultrasonic_all()
    ```

---

### ROBOT.UPDATE_ODOMETRY
*`robot.update_odometry()`*

Actualiza la posición estimada del robot. Actualmente no implementado, pero reservado para fusión de datos de encoders e IMU.
!!! tip "Ejemplo de uso de metodo `update_odometry`"

    Este comando actualiza la odometría del robot, aunque actualmente no realiza ninguna acción.
    ```python
    robot.update_odometry()
    ```

---

### ROBOT.MOTORS
*`robot.motors`*

Lista de objetos `MotorWithPID` que representan cada una de las ruedas del robot.

!!! tip "Ejemplo de uso de la lista `robot.motors`"

    Este comando itera sobre cada motor del robot e imprime su estado actual.
    ```python
    for motor in robot.motors:
        print(motor.get_state())
    ```

---
