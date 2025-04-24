
# Clase 2: The Coach

## LEGO® Education SPIKE™ Prime

### Descripción
Este proyecto consiste en programar un entrenador que realiza movimientos rítmicos con las piernas, simulando una rutina de ejercicios. Se trabaja el control de posición y el uso de ciclos temporizados en Python.

---

### 📎 Instrucciones de armado y actividad:

- [Ver actividad en el sitio oficial de LEGO Education](https://education.lego.com/es-es/lessons/prime-life-hacks/the-coach/)
- [Instrucciones de construcción (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt74278122137e7ed4/5ec90b212bcd084408605ce2/coach-bi-pdf-book1of1.pdf?locale=es-es)

---

### 💻 Código Python

```python
from hub import port
import runloop
import motor
import time

# El motor de la pata izquierda está en el puerto F.
# El motor de la pata derecha está en el puerto B.

async def main():
    
    # Coloque el entrenador de pie derecho.
    motor.run_to_absolute_position(port.F, 0, 800)
    motor.run_to_absolute_position(port.B, 0, 800)

    start_time = time.ticks_ms()

    
    #El entrenador bailará durante cinco segundos.
    while time.ticks_diff(time.ticks_ms(), start_time) < 5000:
        motor.set_duty_cycle(port.B, -7000)
        motor.set_duty_cycle(port.F, 7000)

        await runloop.sleep_ms(200)

        motor.set_duty_cycle(port.B, 7000)
        motor.set_duty_cycle(port.F, -7000)

        await runloop.sleep_ms(200)

    motor.stop(port.B)
    motor.stop(port.F)

runloop.run(main())
```

---

### 🧠 Objetivo de la clase

- Comprender y aplicar el uso de `duty_cycle` para controlar velocidad en motores.
- Utilizar estructuras de repetición con control de tiempo (`while`, `ticks_ms`, `ticks_diff`).
- Sincronizar movimientos opuestos en motores para generar acciones coordinadas.
- Consolidar el uso de funciones asincrónicas en Python para Spike Prime.

