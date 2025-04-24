
# Clase 9: Design for Someone

## LEGO® Education SPIKE™ Prime

### Descripción
En este proyecto, los estudiantes diseñan una prótesis que se adapta al brazo de una persona. El brazo robótico puede cerrarse sobre el brazo y soltarse presionando un botón. También detecta la fuerza aplicada y da retroalimentación visual si esta supera cierto umbral.  
Una excelente introducción a la ingeniería biomédica y al diseño inclusivo con tecnología.

---

### 📎 Instrucciones de armado y actividad:

- [Ver lección oficial en LEGO Education](https://education.lego.com/es-es/lessons/prime-invention-squad/design-for-someone/)
- [Instrucciones de construcción - Parte 1 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt2e399cf8d3b5ae05/5ec9720da8bb8c02ad27b20f/design-for-someone-bi-pdf-book1of2.pdf?locale=es-es)
- [Instrucciones de construcción - Parte 2 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/bltfa53bbbf3c618f5a/5ec97160f8b8c35280dc0696/design-for-someone-bi-pdf-book2of2.pdf?locale=es-es)

---

### 💻 Código Python

```python
from hub import light_matrix, port, sound, button
import runloop
import motor
import force_sensor

async def main():
    await motor.run_to_absolute_position(port.A, 0, 750)
    await motor.run_to_absolute_position(port.E, 0, 750)
    await sound.beep(262, 500)
    await sound.beep(523, 500)

    # Hacer que la prótesis se cierre sobre el brazo
    await motor.run_for_time(port.A, 1000, 750, stop=motor.HOLD)
    await motor.run_for_time(port.E, 1000, -750, stop=motor.HOLD)

    while True:
        if button.pressed(button.RIGHT):
            # Soltar la prótesis
            await motor.run_to_absolute_position(port.A, 0, 750)
            await motor.run_to_absolute_position(port.E, 0, 750)

        if force_sensor.force(port.B) > 50:
            light_matrix.show_image(light_matrix.IMAGE_SQUARE)
            # Aquí se puede agregar más código para abrir/cerrar pinza
        else:
            light_matrix.clear()
            await runloop.sleep_ms(10)

runloop.run(main())
```

---

### 🧠 Objetivos de la clase

- Simular un dispositivo biomecánico de ayuda utilizando motores y sensores.
- Controlar acciones con botones físicos y condiciones de fuerza.
- Aplicar retroalimentación visual mediante la matriz LED.
- Fomentar la empatía y el diseño centrado en el usuario.
- Desarrollar lógica de programación con estructuras `while` y `if`.
