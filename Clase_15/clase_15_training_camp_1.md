
# Clase 14: Training Camp 1 - Driving Around

## LEGO® Education SPIKE™ Prime

### Descripción
En esta clase, los estudiantes programan un robot móvil para que recorra un cuadrado perfecto. Utilizan cálculos matemáticos para convertir distancia a grados de rotación, además de coordinar movimientos de avance y giro recto usando pares de motores. Esta actividad es excelente para reforzar lógica de programación, geometría y control de trayectoria.

---

### 📎 Instrucciones de armado y actividad:

- [Ver lección oficial en LEGO Education](https://education.lego.com/es-es/lessons/prime-competition-ready/training-camp-1-driving-around/)
- [Instrucciones de construcción (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt06873e1b438a0d7e/5ec8e66f033ad5045f4c79a6/driving-base-bi-pdf-book1of1.pdf?locale=es-es)

---

### 💻 Código Python

```python
from hub import port
import runloop
import motor_pair

# El motor izquierdo está en el puerto C
# El motor derecho está en el puerto D
motor_pair.pair(motor_pair.PAIR_1, port.C, port.D)

async def main():
    # Recorre un cuadrado con cuatro lados
    for x in range(4):
        # Para recorrer 10 cm, calculamos (10 / 17.5) * 360 ≈ 206 grados
        await motor_pair.move_for_degrees(motor_pair.PAIR_1, 206, 0, velocity=300)
        await runloop.sleep_ms(500)
        # Girar a la derecha
        await motor_pair.move_for_degrees(motor_pair.PAIR_1, 182, 100, velocity=300)

runloop.run(main())
```

---

### 🧠 Objetivos de la clase

- Aprender a convertir distancias lineales a rotaciones de motor.
- Aplicar bucles `for` para repetición estructurada.
- Controlar trayectorias mediante movimiento combinado de motores.
- Reforzar conceptos de geometría y orientación en programación.
- Ajustar parámetros como grados y velocidad para obtener trayectorias precisas.
