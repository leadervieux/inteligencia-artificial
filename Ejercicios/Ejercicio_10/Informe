# Ejercicio 1: cambiar la imagen de predicción en YOLO

## 1. Método

Primero se ejecutó el notebook sin modificarlo sobre `zidane.jpg` y `bus.jpg`. El único cambio de código es después la fuente de la imagen, tanto en la celda CLI (`source=...`) como en la celda Python (`model('...', save=True)`). No se modificaron el modelo, el número de épocas ni el dataset.

## 2. Resultados

| Imagen | Celda | Detecciones | Cajas |
|---|---|---|---|
| `zidane.jpg` | CLI | 2 `person`, 1 `tie` | 3 |
| `zidane.jpg` | Python | 2 `person`, 1 `tie` | 3 |
| `bus.jpg` | CLI | 4 `person`, 1 `bus`, 1 `stop sign` | 6 |
| `bus.jpg` | Python | 4 `person`, 1 `bus` | 5 |
| Mi foto (`DSCN2657.jpeg`) | CLI (conf = 0,25) | 3 `person`, 1 `bicycle` | 4 |
| Mi foto (`DSCN2657.jpeg`) | Python | 3 `person`, 1 `bicycle`, 1 `handbag` | 5 |
| Mi foto (`DSCN2657.jpeg`) | CLI (conf = 0,7) | 3 `person` | 3 |

Imágenes de salida:
Hay un archivo por imagen en la misma carpeta que este informe.

## 3. Análisis

### Clases detectadas

En las fotos de ejemplo de Ultralytics, YOLO detecta personas, una corbata (Zidane), un autobús y, según la celda, una señal de alto (autobús). En mi foto detecta tres personas, una bicicleta y un bolso.

### Objetos no detectados

El **collar** que lleva una de las personas no fue detectado.  Es lo esperable: la clase «collar» no existe entre las 80 clases de COCO, y YOLO no puede nombrar lo que no ha aprendido.
También hay un reloj y dos teléfonos que no han sido detectados, pero son pequeños y están un poco escondidos.

El resto de los objetos evidentes de la foto sí fueron etiquetados.

### CLI y `model(...)`: ¿coinciden?

No del todo. En mi foto, la celda CLI no detecta el bolso, mientras que `model()` sí lo detecta. En el autobús ocurre al revés: el CLI añade una señal de alto que `model()` no conserva.
Sus confianzas difieren ligeramente, y algunas detecciones cercanas al umbral de 0,25 pasan en uno y no en el otro.

### Efecto del umbral de confianza (reto opcional)

Con `conf=0.7` en lugar de 0,25, el CLI conserva solo las **tres personas**. Por tanto, la bicicleta tiene una confianza entre 0,25 y 0,7. Un umbral más estricto elimina las detecciones inciertas, a costa de más omisiones.
