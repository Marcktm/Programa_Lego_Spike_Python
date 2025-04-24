
# Clase 16: Help!

## LEGO® Education SPIKE™ Prime

### Descripción
En esta clase, los estudiantes crean una historia interactiva utilizando el sensor de color y sonidos pregrabados. El robot interpreta escenas al pasar sobre superficies de distintos colores, y reproduce efectos de sonido acorde a cada una. Esta actividad fortalece la creatividad narrativa y el uso del entorno LEGO como medio expresivo.

---

### 📎 Instrucciones de armado y actividad:

- [Ver lección oficial en LEGO Education](https://education.lego.com/es-es/lessons/prime-invention-squad/help/)
- [Instrucciones de construcción (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt7c8102105587e585/5ec96d37afa52a7b51941198/help-bi-pdf-book1of1.pdf?locale=es-es)

---

### 💻 Código Python

```python
from hub import port, button
from app import sound
import runloop
import color_sensor
import color

async def main():
    # Historia 1: Kiki va de paseo
    await runloop.until(lambda: button.pressed(button.LEFT))

    await runloop.until(lambda: color_sensor.color(port.B) is color.BLUE)
    await sound.play('Traffic')

    await runloop.until(lambda: color_sensor.color(port.B) is color.YELLOW)
    await sound.play('Ring Tone')

    await runloop.until(lambda: color_sensor.color(port.B) is color.GREEN)
    await sound.play('Dog Bark 1')

    # Historia 2
    await runloop.until(lambda: button.pressed(button.RIGHT))

    await runloop.until(lambda: color_sensor.color(port.B) is color.BLUE)
    await sound.play('Door Knock')

    await runloop.until(lambda: color_sensor.color(port.B) is color.YELLOW)
    await sound.play('Glass Breaking')

    await runloop.until(lambda: color_sensor.color(port.B) is color.GREEN)
    await sound.play('Dog Bark 3')

runloop.run(main())
```

---

### 🧠 Objetivos de la clase

- Crear una narrativa interactiva con sensores y sonidos.
- Utilizar múltiples entradas de color como disparadores de eventos.
- Promover la creatividad y el pensamiento secuencial en programación.
- Explorar estructuras condicionales para representar distintas historias.
- Comprender cómo combinar hardware y software para generar experiencias lúdicas.

