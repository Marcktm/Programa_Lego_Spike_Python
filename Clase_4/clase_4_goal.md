
# Clase 4: ¡Gol! (LEGO SPIKE Prime)  

## Colaborar para crear un divertido juego de mesa y marcar todos los goles posibles

En este proyecto, los estudiantes van a **construir y programar un juego de mesa de fútbol**. Montarán una portería y un lanzador robótico con el Hub SPIKE Prime, junto con un jugador manual y un disco que servirá de pelota.  
El robot se programa para **disparar el disco** al presionar un botón, intentando marcar gol en la portería.

El objetivo es **colaborar en equipo** para anotar tantos goles como sea posible en un minuto. Esta actividad fomenta la cooperación entre los alumnos, la experimentación con los parámetros del programa para mejorar la puntería, ¡y la diversión durante el proceso!

---

## 📎 Recursos

- [Ver lección oficial en LEGO Education](https://education.lego.com/es-es/lessons/prime-extra-resources/goal/)
- [Instrucciones de construcción - Parte 1 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blt25ccf29333726892/5ec82ab3e806087c31d74bf8/goal-bi-pdf-book1of2.pdf?locale=es-es)
- [Instrucciones de construcción - Parte 2 (PDF)](https://assets.education.lego.com/v3/assets/blt293eea581807678a/blteb6456e334796987/5ec82aad857d582712bdbec1/goal-bi-pdf-book2of2.pdf?locale=es-es)

---

## 💻 Código Python

```python
from hub import port, button
import runloop
import motor

async def main():
    while True:
        # Colocar el motor en la posición de 0 grados
        motor.run_to_absolute_position(port.A, 0, 1000)

        # Esperar a que se presione el botón izquierdo para mover el motor 360 grados
        await runloop.until(lambda: button.pressed(button.LEFT))
        await motor.run_for_degrees(port.A, 360, 1000)

        # Esperar un segundo antes de poder volver a presionar el botón
        await runloop.sleep_ms(1000)

runloop.run(main())
```

---

## 🧠 Objetivos de la clase

- Controlar el posicionamiento absoluto de motores.
- Usar `runloop.until()` para esperar eventos de botones.
- Implementar un ciclo continuo que permita repetir la acción de disparo.
- Fomentar la creatividad y el trabajo en equipo mediante un juego físico y programado.
