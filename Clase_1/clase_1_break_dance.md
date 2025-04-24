
# Clase 1: Break Dance

## LEGO® Education SPIKE™ Prime

### Descripción
Este proyecto se basa en el modelo "Break Dance", que permite explorar el control de motores, sincronización de movimientos y uso básico de la matriz LED. Está pensado para introducir la programación en Python con LEGO Spike Prime.

---

### 📎 Instrucciones de armado oficiales:

- [Instrucciones Parte 1 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt1b1cabca80846180/5ec9079400455b25665b177d/break-dance-bi-pdf-book1of2.pdf?locale=es-es)
- [Instrucciones Parte 2 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blta15ecafc09d28bab/5ec90760f8b8c35280dbf68c/break-dance-bi-pdf-book2of2.pdf?locale=es-es)

---

### 💻 Código Python

```python
from hub import light_matrix, port
import runloop
import motor

# The arm motor is in port B.
# The leg motor is in port F.

async def main():
    # Move arms and legs to 0 position.
    motor.run_to_absolute_position(port.B, 0, -800)
    await motor.run_to_absolute_position(port.F, 0, -800)
    await runloop.sleep_ms(1000)

    for x in range(10):
        await light_matrix.write('1')
        # Move arms and legs at the same time.
        motor.run_for_degrees(port.F, 360, -800)
        await motor.run_for_degrees(port.B, 360, -800)
        await runloop.sleep_ms(450)

        await light_matrix.write('2')
        motor.run_for_degrees(port.F, 360, -800)
        await motor.run_for_degrees(port.B, 360, -800)
        await runloop.sleep_ms(450)

        await light_matrix.write('3')
        motor.run_for_degrees(port.F, 360, -800)
        await motor.run_for_degrees(port.B, 360, -800)
        await runloop.sleep_ms(450)

runloop.run(main())
```

---

### 🧠 Objetivo de la clase

- Aprender a inicializar motores y establecer posiciones absolutas.
- Controlar movimientos sincronizados en bucle.
- Mostrar números o símbolos en la matriz LED.
- Comprender la estructura básica de un programa asincrónico en Python.

