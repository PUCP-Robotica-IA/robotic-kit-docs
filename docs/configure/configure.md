# CONFIGURACIONES INICIALES

## config.py

📦 **CONFIG:** Diccionario de configuración de hardware

Este bloque de código es un diccionario en Python que contiene la configuración de hardware para distintos tipos de robots o dispositivos. Cada clave representa una configuración específica que puede activarse según el tipo de robot que se esté utilizando.

*   `CONFIG ["test"]` : Configura al robot omnidireccional en modo prueba para usar dos de sus ruedas mediante mediante señales PWM, encoders(a,b) y dirección.
  * PWM, dirección y encoders.
*   `CONFIG ["mecanum"]` : Configura al robot omnidireccional para usar sus cuatro ruedas y sensores asociador.
  * PWM, dirección y encoders.
  * Sensores ultrasónicos (3) conectados a pines analógicos (ADC).
  * Sensor IMU conectado por I2C.
*   `CONFIG ["arm"]` : Configura al brazo robotico de cuatro grados de libertad.    
  * 4 servomotores.
  * Salida para efector final.
  * Sensor ultrasonido.
*   `CONFIG ["sensors"]` : Configura al brazo robotico de cuatro grados de libertad.    
  * Sensores ultrasónicos (3) conectados a pines analógicos (ADC).
  * Sensor IMU conectado por I2C.


`merge_motor_directions(config)`

Esta función toma un subdiccionario del diccionario CONFIG que contiene una lista de parámetros de configuración para motores bajo la clave "motors", y fusiona cada uno de ellos con posibles valores adicionales definidos externamente (por ejemplo, direcciones personalizadas).
    
Parámetros:

*   `config: 'dict'`
  
  Diccionario de configuración de hardware correspondiente al robot omnidireccional.