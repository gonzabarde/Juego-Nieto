# Jenga de Cultura General

Reinvención escolar del Jenga para Argentina: bloques impresos en 3D con un color por materia y un nivel de dificultad grabado, cartas de preguntas y un sistema de puntos. De 2 a 4 jugadores, 20 a 30 minutos.

**60 bloques · 20 pisos · 60 cartas · 5 materias × 3 niveles**

---

## Cómo se juega

1. Armá la torre sobre la base: 15 pisos de 3 bloques, cada piso girado 90° respecto del anterior.
2. En tu turno, sacá un bloque con una sola mano.
3. Mirá qué te tocó: la **letra** de la punta dice la materia y el **número romano** de la cara grande dice el nivel. En la torre sólo se ven las puntas, así que elegís la materia y el nivel te toca.
4. El jugador de tu izquierda saca una carta de ese mazo y te lee la pregunta.
5. Respondé antes de apoyar el bloque. Si acertás sumás **1, 2 o 3 puntos** según el nivel; si errás **restás 1** (nunca bajás de cero).
6. Colocá el bloque arriba de todo y pasa el turno.

Cuando la torre se cae, termina la partida. **Quien la tiró pierde todos sus puntos.** Gana el que tenga más.

> Reglas completas, variantes y guía de impresión en **[Jenga_Cultura_General_Reglas.pdf](Jenga_Cultura_General_Reglas.pdf)**

---

## Materias y colores

| Materia | Color | Inicial | Nivel 1 · 1 pt | Nivel 2 · 2 pts | Nivel 3 · 3 pts | Bloques |
|---|---|---|---|---|---|---|
| Historia | Rojo | H | `#FFCCCC` | `#FF5555` | `#AA0000` | 9 |
| Geografía | Verde | G | `#CCFFCC` | `#44BB44` | `#006600` | 9 |
| Ciencias Naturales | Azul | C | `#CCE5FF` | `#4499DD` | `#004488` | 9 |
| Lengua y Literatura | Violeta | L | `#E8CCFF` | `#9955CC` | `#551188` | 9 |
| Educación Cívica | Naranja | E | `#FFE5CC` | `#FF8833` | `#BB4400` | 9 |

Cada materia lleva **4 bloques de cada nivel**. Los bloques se imprimen todos del mismo color: la materia se lee por la inicial grabada en las dos puntas y el nivel por el número romano de la cara grande, que en la torre queda tapado.

---

## Cómo imprimirlo

### Piezas 3D

| Archivo | Qué es | Medidas | Cuántas veces |
|---|---|---|---|
| [`stl/Bandeja de bloques.stl`](stl/) | **30 bloques acomodados** para una cama de 250 × 250 | 219 × 161 × 10,5 mm | **2 veces** → 60 bloques |
| [`stl/materias/*.3mf`](stl/materias/) | Los mismos bloques, separados por materia | 66,5 × 52,5 × 10,5 mm | 4 veces cada uno |
| [`stl/Jenga de Cultura General.stl`](stl/) | Los 15 bloques distintos, juntos (archivo original) | 66 × 298 × 10,5 mm | — (ver nota) |
| [`stl/Base de la torre.stl`](stl/) | Placa que apoya y centra el primer piso | 62,1 × 62,1 × 4,6 mm | 1 vez |
| [`stl/Porta-cartas.stl`](stl/) | Bandeja para los mazos, con muesca para sacarlas | 77 × 105 × 24 mm | 1 vez |
| [`stl/Caja del juego.stl`](stl/) | Caja con dos compartimentos y divisor rebajado | 140,5 × 113 × 108 mm | 1 vez |
| [`stl/Tapa de la caja.stl`](stl/) | Tapa con muescas de agarre | 145,2 × 117,7 × 32 mm | 1 vez |
| [`stl/piezas/*.3mf`](stl/piezas/) | Las mismas piezas en 3MF, en gris grafito | — | — |

Cada bloque mide **52,5 × 17,5 × 10,5 mm**: el 70 % de un Jenga común (75 × 25 × 15), para
gastar menos filamento. Los 60 bloques son **20 pisos**, una torre de 21 cm.

Para imprimir, lo más cómodo es la **bandeja**: trae 30 bloques ya acomodados y entra en una cama de 250 × 250 dejando 10 mm de margen por lado. El `.stl` de los 15 juntos mide 298 mm de largo y queda como archivo original de referencia.

Boquilla 0,4 mm · capa 0,2 mm · relleno 15–20 % · **sin soportes**. Si al armar la torre los pisos quedan desparejos, imprimí los bloques al 99 % de escala.

### Cartas

Cada `cartas.pdf` tiene 2 páginas. Imprimilas **a doble faz, girando por el lado largo**, en papel de 160–200 g. Recortá por las cruces de las esquinas: cada carta queda de **72 × 100 mm**.

---

## Archivos del proyecto

| Archivo | Descripción |
|---|---|
| [`Jenga_Cultura_General_Reglas.pdf`](Jenga_Cultura_General_Reglas.pdf) | Manual de reglas completo (4 páginas) |
| [`Hoja_de_Puntaje.pdf`](Hoja_de_Puntaje.pdf) | Planilla para anotar los puntos turno a turno |
| [`datos/Materias_y_Bloques.pdf`](datos/Materias_y_Bloques.pdf) | Colores hex y cantidades para imprimir |
| [`preguntas/`](preguntas/) | Los 15 mazos de cartas |
| [`stl/`](stl/) | Bloques, base y porta-cartas |
| [`informe/INFORME.pdf`](informe/INFORME.pdf) | Informe escolar del trabajo |
| [`presentacion/Informe_del_juego.pdf`](presentacion/) | Informe completo del proyecto en texto, con la prueba de juego para completar |
| [`presentacion/Informe_del_juego.docx`](presentacion/) | El mismo informe en Word, para editarlo a mano |
| [`packaging/Arte_de_la_caja.pdf`](packaging/) | Arte de la caja: tapa, dorso y laterales, a escala real con sangrado |

### Mazos de cartas

```
preguntas/
├── historia/   nivel-1 · nivel-2 · nivel-3
├── geografia/  nivel-1 · nivel-2 · nivel-3
├── ciencias/   nivel-1 · nivel-2 · nivel-3
├── lengua/     nivel-1 · nivel-2 · nivel-3
└── civica/     nivel-1 · nivel-2 · nivel-3
```

15 mazos × 4 cartas = 60 preguntas.

---

## Créditos

Proyecto escolar de impresión 3D. Las 60 preguntas corresponden a contenidos
de secundaria argentina: Historia, Geografía, Ciencias Naturales, Lengua y
Literatura y Educación Cívica.

Jenga es una marca registrada de Pokonobe Associates. Este es un trabajo
escolar sin fines comerciales.
