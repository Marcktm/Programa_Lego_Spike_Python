
# Clase 7: Keep it Really Safe!

## LEGO® Education SPIKE™ Prime

### Descripción
En esta actividad, los estudiantes deben mejorar una caja fuerte para agregarle una cerradura con dial. El desafío consiste en sincronizar el giro del dial con la presión de un botón en el momento justo, lo que introduce control de tiempo, lectura de posiciones relativas y ejecución de funciones asíncronas. Si el intento falla, el robot emite un sonido de advertencia.

---

### 📎 Instrucciones de armado y actividad:

- [Ver lección oficial en LEGO Education](https://education.lego.com/es-es/lessons/prime-kickstart-a-business/keep-it-really-safe/)
- [Instrucciones de construcción - Parte 1 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt890416052373ee13/5ec9298d2bcd084408606131/keep-it-really-safe-bi-pdf-book1of2.pdf?locale=es-es)
- [Instrucciones de construcción - Parte 2 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/bltbd5a76c6d4aec5e8/5ec929e1cd4cf750c8892dc3/keep-it-really-safe-bi-pdf-book2of2.pdf?locale=es-es)

---

### 💻 Código Python

```python
from hub import port, light_matrix, button, sound
import runloop
import motor
import app
import time

# El motor de la cerradura está en el puerto C.
# El motor del dial está en el puerto B.
# El motor de la tapa del dial está en el puerto E.

# Función que desbloquea la caja fuerte
async def unlock():
    start_time = time.ticks_ms()

    # Mientras no se presione el botón izquierdo o el dial no haya girado 180 grados
    while not button.pressed(button.LEFT) or motor.relative_position(port.B) < 180:
        await sound.beep(262, 200)
        await motor.run_for_degrees(port.E, 15, 500)
        await runloop.sleep_ms(800)

        # Si pasan 5 segundos sin éxito, reproducir sonido de error
        if time.ticks_diff(time.ticks_ms(), start_time) > 5000:
            await app.sound.play('Bonk')
            return

    # Si se cumple la condición correcta, abrir la caja
    light_matrix.show_image(light_matrix.IMAGE_YES)
    await motor.run_to_absolute_position(port.E, 0, 500)
    await motor.run_for_time(port.C, 1000, 500)
    await app.sound.play('Wand')

# Función principal
async def main():
    await sound.beep(262, 200)
    await sound.beep(523, 200)

    # Cierra la caja fuerte
    await motor.run_for_time(port.C, 1000, -500)
    await motor.run_to_absolute_position(port.B, 0, 500, stop=motor.COAST)
    motor.reset_relative_position(port.B, 0)
    await motor.run_to_absolute_position(port.E, 0, 500)
    light_matrix.show_image(light_matrix.IMAGE_NO)

    # Llama a la función para desbloquear
    await unlock()

runloop.run(main())
```

---

### 🧠 Objetivos de la clase

- Mejorar una estructura funcional previa con nuevas condiciones de seguridad.
- Usar funciones asíncronas (`async def`) para separar lógica de control compleja.
- Controlar tiempos y secuencias mediante `time.ticks_ms()` y `runloop.sleep_ms()`.
- Aplicar lógica condicional junto a retroalimentación visual y sonora.
- Reforzar el pensamiento lógico al crear una “cerradura electrónica” sensible a múltiples factores.
