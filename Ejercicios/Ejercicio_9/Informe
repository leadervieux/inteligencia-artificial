# Inferencia con cláusulas definidas — Caso de la biblioteca

## 1. Introducción y base de conocimientos

Hemos implementado un nuevo archivo de base de conocimientos en formato YAML para modelar las reglas de acceso nocturno a la biblioteca. Las tres consultas principales enviadas a los dos motores de inferencia son:
1. `AccesoNoche(Ana)`
2. `AccesoNoche(Luis)`
3. `AccesoNoche(Marta)`

---

## 2. Resultados globales

Tras la ejecución de los algoritmos sobre la base inicial:
* **Para Ana y Marta:** La consulta está **demostrada** por ambos algoritmos (`FC=YES`, `BC=YES`).
* **Para Luis:** La consulta **no está demostrada** por ninguno de los dos algoritmos (`FC=NO`, `BC=NO`).

---

## 3. Análisis detallado y respuestas a las preguntas

### ¿Por qué aparece `Becario(Ana)` únicamente en el encadenamiento hacia adelante?
`Becario(Ana)` aparece en el encadenamiento hacia adelante (*forward chaining*) porque este algoritmo está **impulsado por los datos** (*data-driven*). Explora y deriva *todas* las consecuencias posibles de la base de conocimientos antes de emitir cualquier prueba, aplicando sistemáticamente todas las reglas válidas. 

En cambio, el encadenamiento hacia atrás (*backward chaining*) está **impulsado por la meta** (*goal-driven*): parte de la consulta y solo retrocede a través de las reglas estrictamente necesarias. Como la regla de la beca (`R_beca`) no es útil para demostrar el acceso nocturno, el encadenamiento hacia atrás la ignora por completo.

### ¿Por qué el encadenamiento hacia atrás prueba `R_miembro_est` para Marta aunque sea profesora?
El encadenamiento hacia atrás prueba las reglas en el orden estricto de la tabla. Para demostrar `AccesoNoche(Marta)`, el sistema intenta primero demostrar que es miembro (`Miembro(Marta)`). 

Para ello, evalúa la primera regla de la tabla que permite deducir un miembro: `R_miembro_est` (que requiere ser estudiante). El algoritmo no "sabe" de antemano que Marta es profesora; por lo tanto, prueba esta primera opción, constata un fallo (`Estudiante(Marta)` es falso) y luego pasa de forma natural a la regla siguiente, `R_miembro_prof`, la cual tiene éxito gracias al hecho `Profesor(Marta)`.

### ¿Qué sucede si se añade el hecho `TieneCredencial(Luis)`?
Si se añade el hecho `TieneCredencial(Luis)` a la base y se vuelve a lanzar la consulta `AccesoNoche(Luis)`, **la consulta queda demostrada por ambos algoritmos**. 

En efecto, Luis ya era un estudiante (`Estudiante(Luis)`). Al añadirle una credencial, se satisfacen todas las premisas de la regla `R_miembro_est`, lo que lo califica como `Miembro(Luis)`. Combinado con el horario nocturno (`HorarioNocturno(Hoy)`), la regla `R_acceso` se dispara y valida el acceso nocturno.

---

## 4. Conclusión: Comparación de enfoques

Este ejercicio ilustra perfectamente los compromisos entre las dos estrategias de inferencia:
* **El encadenamiento hacia adelante** es ideal cuando se desea deducir un máximo de información global a partir de un conjunto de hechos, pero puede resultar ineficiente si genera muchos hechos inútiles (como el estatus de becario en nuestro caso).
* **El encadenamiento hacia atrás** es mucho más eficiente cuando se busca validar una hipótesis precisa o responder a una consulta específica, ya que evita calcular ramas enteras de la base de conocimientos que no sirven para el objetivo buscado.
