
# Clase 12: Out of Order

## LEGO® Education SPIKE™ Prime

### Descripción
En este proyecto, los estudiantes construirán un robot que simula estar fuera de servicio, pero que puede volver a funcionar siguiendo una secuencia programada. Se combinan sensores de distancia, botones y emparejamiento de motores para simular movimiento y control del entorno.

---

### 📎 Instrucciones de armado y actividad:

- [Ver lección oficial en LEGO Education](https://education.lego.com/es-es/lessons/prime-kickstart-a-business/out-of-order/)
- [Instrucciones de construcción (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt49da50c2bc43ea63/5ec9262c7976043edd42fb9f/out-of-order-bi-pdf-book1of1.pdf?locale=es-es)

---

### 💻 Código Python

```python
from hub import port, button
import runloop
import motor
import motor_pair
import distance_sensor

# El motor trasero está en el puerto C
# Emparejar motores con el izquierdo en A y el derecho en E
motor_pair.pair(motor_pair.PAIR_1, port.A, port.E)

async def main():
    # Espera hasta que se presione el botón izquierdo
    await runloop.until(lambda: button.pressed(button.LEFT))
    await motor.run_to_absolute_position(port.C, 0, 1000)
    motor_pair.move(motor_pair.PAIR_1, 0, velocity=500)

    # Ajustar la distancia (robot avanza hasta que esté a menos de 150 mm del obstáculo)
    await runloop.until(lambda: distance_sensor.distance(port.B) < 150)
    motor_pair.stop(motor_pair.PAIR_1)

    # Espera hasta que se presione el botón derecho
    await runloop.until(lambda: button.pressed(button.RIGHT))
    await motor.run_to_absolute_position(port.C, 0, 1000)
    motor_pair.move(motor_pair.PAIR_1, 0, velocity=500)

    # Avanza hasta estar a menos de 150 mm
    await runloop.until(lambda: distance_sensor.distance(port.B) < 150)
    motor_pair.stop(motor_pair.PAIR_1)

    # Gira el robot
    await motor.run_to_absolute_position(port.C, 20, 1000)
    await runloop.sleep_ms(1000)
    await motor_pair.move_for_degrees(motor_pair.PAIR_1, -1028, 0, velocity=500)
    await motor.run_to_absolute_position(port.C, 0, 1000)

    # Ajustar la distancia final
    await motor_pair.move_for_degrees(motor_pair.PAIR_1, 1028, 0, velocity=500)

runloop.run(main())
```

---

### 🧠 Objetivos de la clase

- Emparejar motores para movimiento coordinado.
- Controlar el flujo del programa mediante botones físicos.
- Utilizar sensores de distancia para crear condiciones de detención automatizada.
- Simular el funcionamiento de un sistema con fallas temporales o eventos interrumpidos.
- Aplicar lógica de espera y condiciones usando `runloop.until()` para programación reactiva.
