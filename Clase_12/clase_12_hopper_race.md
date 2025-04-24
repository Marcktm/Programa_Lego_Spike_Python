
# Clase 11: Hopper Race

## LEGO® Education SPIKE™ Prime

### Descripción
En este proyecto, los estudiantes construirán un robot saltarín (Hopper) y lo programarán para participar en una carrera. Utilizarán una cuenta regresiva visual con la matriz LED, emparejarán motores y controlarán el movimiento durante un tiempo determinado. La distancia que recorre se puede ajustar fácilmente modificando el tiempo de ejecución.

---

### 📎 Instrucciones de armado y actividad:

- [Ver lección oficial en LEGO Education](https://education.lego.com/es-es/lessons/prime-invention-squad/hopper-race/)
- [Instrucciones de construcción (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt28e61b3ed1dbebda/5ec96eab694dd13eb3ffbf78/hopper-teacher-solution-bi-pdf-book1of1.pdf?locale=es-es)

---

### 💻 Código Python

```python
from hub import light_matrix, port
import runloop
import motor_pair

async def main():
    # Emparejar los motores en los puertos E y F
    motor_pair.pair(motor_pair.PAIR_1, port.E, port.F)

    # Cuenta regresiva visual desde 3
    await light_matrix.write('3')
    await runloop.sleep_ms(1000)

    await light_matrix.write('2')
    await runloop.sleep_ms(1000)

    await light_matrix.write('1')
    await runloop.sleep_ms(1000)
    light_matrix.clear()

    # Ajusta este valor para modificar la distancia que recorre el robot
    motor_pair.move_for_time(motor_pair.PAIR_1, 10000, 0, velocity=500)

runloop.run(main())
```

---

### 🧠 Objetivos de la clase

- Emparejar motores para coordinar el movimiento de un robot.
- Controlar el tiempo de ejecución para definir la distancia recorrida.
- Implementar una cuenta regresiva visual con `light_matrix`.
- Experimentar con variaciones de velocidad y duración para observar su efecto.
- Fomentar la competencia amistosa con una carrera de robots.
