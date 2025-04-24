
# Clase 6: Keep it Safe

## LEGO® Education SPIKE™ Prime

### Descripción
En este proyecto, los estudiantes programarán una caja fuerte que se bloquea y desbloquea con acciones específicas. Utiliza control de motores, posiciones relativas, sensores de botón y retroalimentación visual (matriz LED) y sonora (beeps).  
Es ideal para trabajar lógica condicional, manipulación de motores y ciclos de espera activa.

---

### 📎 Instrucciones de armado y actividad:

- [Ver lección oficial en LEGO Education](https://education.lego.com/es-es/lessons/prime-kickstart-a-business/keep-it-safe/)
- [Instrucciones de construcción - Parte 1 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt4e040ae676c39c82/5ec927f3e806087c31d76d95/keep-ti-safe-bi-pdf-book1of2.pdf?locale=es-es)
- [Instrucciones de construcción - Parte 2 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt6f9f8a049e59705a/5ec92895f32b1a633f905bf9/keep-ti-safe-bi-pdf-book2of2.pdf?locale=es-es)

---

### 💻 Código Python

```python
from hub import port, sound, light_matrix, button
import motor, runloop

async def main():
    await sound.beep(262, 500)
    await sound.beep(523, 500)

    # Cierra la caja fuerte
    await motor.run_to_absolute_position(port.C, 270, 500)
    await motor.run_to_absolute_position(port.B, 0, 750, stop=motor.COAST)
    motor.reset_relative_position(port.B, 0)
    light_matrix.show_image(light_matrix.IMAGE_NO)

    # Abre la caja fuerte
    await runloop.until(lambda: button.pressed(button.LEFT))
    await sound.beep(523, 500)
    await runloop.until(lambda: motor.relative_position(port.B) > 180)
    await sound.beep(262, 500)
    await motor.run_for_time(port.C, 1000, 500)
    light_matrix.show_image(light_matrix.IMAGE_NO)
    await runloop.sleep_ms(2000)
    light_matrix.show_image(light_matrix.IMAGE_YES)
    await runloop.sleep_ms(5000)

runloop.run(main())
```

---

### 🧠 Objetivos de la clase

- Aplicar control de motores en posiciones absolutas y relativas.
- Programar ciclos de espera activa con `runloop.until()`.
- Utilizar entradas de botones para desbloquear funciones específicas.
- Representar visualmente estados del sistema con la matriz LED.
- Comprender el flujo de eventos en un sistema de seguridad automatizado.
