
# Clase 13: Super Cleanup

## LEGO® Education SPIKE™ Prime

### Descripción
En esta clase, los estudiantes diseñan y programan una pinza automática que abre y cierra al detectar presión mediante un sensor de fuerza. Esta actividad es ideal para introducir el uso de sensores como controladores de interacción, permitiendo crear mecanismos automatizados para "recoger" objetos.

---

### 📎 Instrucciones de armado y actividad:

- [Ver lección oficial en LEGO Education](https://education.lego.com/es-es/lessons/prime-invention-squad/super-cleanup/)
- [Instrucciones de construcción - Parte 2 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt109d7e1105803297/5ec96f592faa6a256062b52f/supercleaup-bi-pdf-book2of3.pdf?locale=es-es)
- [Instrucciones de construcción - Parte 3 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/bltdb108d96005a741c/5ec96f33e014445192ea99e2/supercleaup-bi-pdf-book3of3.pdf?locale=es-es)

---

### 💻 Código Python

```python
from hub import port
import runloop
import motor
import force_sensor

async def main():
    while True:
        # Espera a que se presione el sensor de fuerza
        await runloop.until(lambda: force_sensor.pressed(port.E))
        motor.run(port.A, -750)

        # Espera a que se suelte el sensor de fuerza
        await runloop.until(lambda: not force_sensor.pressed(port.E))
        motor.run(port.A, 750)

runloop.run(main())
```

---

### 🧠 Objetivos de la clase

- Usar sensores de fuerza como entrada para activar mecanismos.
- Programar ciclos de espera para detectar y reaccionar a eventos físicos.
- Explorar aplicaciones de sistemas automatizados simples.
- Aplicar lógica de repetición (`while True`) con condiciones de entrada y salida.
- Comprender el uso de señales físicas como disparadores de eventos en robótica.
