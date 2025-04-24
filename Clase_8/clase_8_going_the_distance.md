
# Clase 8: Going the Distance

## LEGO® Education SPIKE™ Prime

### Descripción
En este proyecto, los estudiantes crearán un robot "rinoceronte" que se detiene cuando detecta un obstáculo usando el sensor de fuerza. Aprenderán a emparejar motores para moverse en línea recta, controlar la velocidad y utilizar sensores para detener el robot automáticamente.

---

### 📎 Instrucciones de armado y actividad:

- [Ver lección oficial en LEGO Education](https://education.lego.com/es-es/lessons/prime-extra-resources/going-the-distance/)
- [Instrucciones de construcción - Parte 1 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt5daa010e44db3cb8/5ec82a257976043edd42dcc7/going-the-distance-bi-pdf-book1of2.pdf?locale=es-es)
- [Instrucciones de construcción - Parte 2 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt1a06a16daa5c9787/5ec82a12fe6e990f9ab3b83a/going-the-distance-bi-pdf-book2of2.pdf?locale=es-es)

---

### 💻 Código Python

```python
from hub import port
import runloop
import motor_pair
import force_sensor

async def main():
    # Empareja los motores (izquierdo en puerto B, derecho en puerto A)
    motor_pair.pair(motor_pair.PAIR_1, port.B, port.A)

    # Mueve el robot hacia adelante a 500 grados por segundo
    motor_pair.move(motor_pair.PAIR_1, 0, velocity=500)

    # Espera hasta que se presione el sensor de fuerza
    await runloop.until(lambda: force_sensor.pressed(port.C))

    # Detiene el robot al presionar el sensor
    motor_pair.stop(motor_pair.PAIR_1)

runloop.run(main())
```

---

### 🧠 Objetivos de la clase

- Controlar el movimiento en línea recta mediante emparejamiento de motores.
- Regular la velocidad de avance de forma precisa.
- Usar sensores para implementar lógica de parada automática.
- Aplicar `runloop.until()` para crear robots que reaccionen ante estímulos físicos.
- Explorar la relación entre fuerza física y respuesta robótica.
