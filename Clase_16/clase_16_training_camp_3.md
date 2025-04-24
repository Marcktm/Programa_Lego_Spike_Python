
# Clase 15: Training Camp 3 - React to Lines

## LEGO® Education SPIKE™ Prime

### Descripción
En esta clase, los estudiantes usarán el sensor de color para detectar líneas negras sobre una superficie blanca. Se exploran dos comportamientos: detenerse al detectar negro, o seguir una línea negra sobre fondo blanco. Los alumnos programarán reacciones autónomas mediante estructuras condicionales y repetitivas.

---

### 📎 Instrucciones de armado y actividad:

- [Ver lección oficial en LEGO Education](https://education.lego.com/es-es/lessons/prime-competition-ready/training-camp-3-react-to-lines/)
- [Instrucciones de construcción - Base del vehículo (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt06873e1b438a0d7e/5ec8e66f033ad5045f4c79a6/driving-base-bi-pdf-book1of1.pdf?locale=es-es)
- [Instrucciones - Sensor de color (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt1e6ac4849c880a3d/5ec8e74f56542b5199dc012f/driving-base-with-color-sensor-bi-pdf-book1of1.pdf?locale=es-es)

---

### 💻 Código Python

```python
from hub import port, button
import runloop
import motor_pair
import color_sensor
import color

# El motor izquierdo está en el puerto C
# El motor derecho está en el puerto D
# El sensor de color está en el puerto B
motor_pair.pair(motor_pair.PAIR_1, port.C, port.D)

async def main():
    # Establece la velocidad base
    velocity_value = 400

    while True:
        # Si se presiona el botón izquierdo, el robot se detiene sobre una línea negra
        if button.pressed(button.LEFT):
            motor_pair.move(motor_pair.PAIR_1, 0, velocity=velocity_value)
            await runloop.until(lambda: color_sensor.color(port.B) is color.BLACK)
            motor_pair.stop(motor_pair.PAIR_1)

        # Si se presiona el botón derecho, el robot sigue la línea negra
        if button.pressed(button.RIGHT):
            while True:
                motor_pair.move_tank(motor_pair.PAIR_1, 1.0, 0, velocity=velocity_value)
                await runloop.until(lambda: color_sensor.color(port.B) is color.BLACK)
                motor_pair.move_tank(motor_pair.PAIR_1, velocity_value, 0)
                await runloop.until(lambda: color_sensor.color(port.B) is color.WHITE)
```

---

### 🧠 Objetivos de la clase

- Usar sensores de color para detectar cambios de superficie.
- Implementar reacciones distintas según la entrada del usuario (botones).
- Aplicar estructuras condicionales (`if`) y repetitivas (`while`) en un entorno real.
- Comprender cómo se utiliza la lógica binaria para tareas de seguimiento de línea.
- Desarrollar programación autónoma basada en sensores.

