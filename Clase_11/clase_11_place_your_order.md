
# Clase 10: Place your Order

## LEGO® Education SPIKE™ Prime

### Descripción
En este proyecto, los estudiantes construyen y programan un robot que detecta colores y responde con una secuencia de movimientos de brazo. La actividad simula el funcionamiento de un sistema de pedidos automatizado. Se trabajan sensores de color, matrices de LED, sonidos y secuencias de movimiento con múltiples motores.

---

### 📎 Instrucciones de armado y actividad:

- [Ver lección oficial en LEGO Education](https://education.lego.com/es-es/lessons/prime-kickstart-a-business/place-your-order/)
- [Instrucciones de construcción - Parte 1 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/bltac101443c1c22ca4/5ec924890482bd7de694aea7/place-your-order-bi-pdf-book1of2.pdf?locale=es-es)
- [Instrucciones de construcción - Parte 2 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/bltcd9e881400a8b7ea/5ec924f2857d582712bdde53/place-your-order-bi-pdf-book2of2.pdf?locale=es-es)

---

### 💻 Código Python

```python
from hub import light_matrix, port
from app import sound
import runloop
import motor
import color_sensor
import color
import distance_sensor

async def main():
    # El motor del brazo está en el puerto A
    # El motor de base está en el puerto F
    await motor.run_to_absolute_position(port.A, 350, 500)
    await motor.run_to_absolute_position(port.F, 350, 500)

    sound.play('Connect')
    pixels = [100] * 4
    distance_sensor.show(port.C, pixels)

    for x in range(10):
        light_matrix.show_image(light_matrix.IMAGE_HEART)
        await runloop.sleep_ms(500)
        light_matrix.show_image(light_matrix.IMAGE_HEART_SMALL)
        await runloop.sleep_ms(500)
    light_matrix.show_image(light_matrix.IMAGE_HEART)

    while True:
        # Esperar a que el sensor de color detecte magenta
        await runloop.until(lambda: color_sensor.color(port.D) is color.MAGENTA)
        await motor.run_for_degrees(port.A, 30, 500)
        await motor.run_for_degrees(port.A, -60, 500)
        await motor.run_for_degrees(port.A, 60, 500)
        await motor.run_for_degrees(port.A, -30, 500)
        sound.play('Connect')
        light_matrix.show_image(light_matrix.IMAGE_HEART)

runloop.run(main())
```

---

### 🧠 Objetivos de la clase

- Aplicar sensores de color para activar secuencias automatizadas.
- Usar funciones `await` y `runloop.until()` en ciclos reactivos.
- Controlar movimientos finos y reversibles con motores.
- Utilizar matrices LED y sonidos como retroalimentación interactiva.
- Simular una cadena de pedidos inteligente con entradas visuales.
