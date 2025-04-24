
# Clase 3: Rain or Shine?

## LEGO® Education SPIKE™ Prime

### Descripción
Este proyecto utiliza dos motores para simular la reacción de un presentador del clima ante condiciones meteorológicas. Se emplean estructuras condicionales en Python, junto con la matriz LED y sonidos, para representar si el día está soleado, lluvioso o indefinido.

---

### 📎 Instrucciones de armado y actividad:

- [Ver actividad en el sitio oficial de LEGO Education](https://education.lego.com/es-es/lessons/prime-life-hacks/rain-or-shine/)
- [Instrucciones de construcción (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt465aba8e468f37ff/5ec908ed59651863385585ba/rain-of-shine-bi-pdf-book1of1.pdf?locale=es-es)

---

### 💻 Código Python

```python
from hub import light_matrix, port, sound
import app
import runloop
import motor

# El motor del paraguas está en el puerto B.
# El motor de las gafas de sol está en el puerto F.

async def main():
    YOUR_LOCAL_FORECAST = 'sunny'

    # Esto coloca al robot en la posición inicial correcta.
    await motor.run_to_absolute_position(port.B, 45, 750)
    await motor.run_to_absolute_position(port.F, 300, 750)

    await sound.beep(262, 200)
    await sound.beep(523, 200)

    # Si hace sol, ponte gafas de sol.
    if YOUR_LOCAL_FORECAST == 'sunny':
        await motor.run_to_absolute_position(port.F, 0, 750)
        light_matrix.show_image(light_matrix.IMAGE_SQUARE)
        await runloop.sleep_ms(200)
        await motor.run_to_absolute_position(port.F, 300, 750)
    elif YOUR_LOCAL_FORECAST == 'rainy':
        # O si llueve, levante el paraguas.
        await motor.run_to_absolute_position(port.B, 340, 750)
        await app.sound_play('Rain')
        await motor.run_to_absolute_position(port.B, 45, 750)
    else:
        # De lo contrario mostrar X.
        light_matrix.show_image(light_matrix.IMAGE_NO)

runloop.run(main())
```

---

### 🧠 Objetivo de la clase

- Usar condiciones (`if`, `elif`, `else`) para controlar el flujo del programa.
- Programar secuencias con reacciones específicas ante diferentes valores de una variable.
- Integrar sonidos, imágenes y movimiento con motores para lograr interacciones completas.
- Comprender cómo simular decisiones basadas en entradas predefinidas o contextuales.

