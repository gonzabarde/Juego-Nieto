# Jenga de Cultura General

Reinvención escolar del clásico Jenga para Argentina: bloques impresos en 3D con colores por materia, cartas de preguntas y un sistema de puntos. De 2 a 4 jugadores.

---

## Cómo se juega

1. Armá la torre con los bloques 3D (como un Jenga común).
2. En tu turno, sacá un bloque e identificá su **materia** (color) y **nivel** (saturación del color).
3. Robá una carta del mazo correspondiente y respondé la pregunta.
4. Si acertás, sumás **1, 2 o 3 puntos** según el nivel. Si fallás, no sumás nada.
5. Colocá el bloque arriba de la torre. Sigue el siguiente jugador.
6. Cuando la torre cae, **termina la partida**. Quien la tiró **pierde todos sus puntos**. Gana quien tenga más puntos.

> Reglas completas en [`Jenga_Cultura_General_Reglas.pdf`](Jenga_Cultura_General_Reglas.pdf)

---

## Materias y colores

| Materia | Color | Nivel 1 | Nivel 2 | Nivel 3 | Bloques |
|---------|-------|---------|---------|---------|---------|
| Historia | Rojo | claro · 1 pt | medio · 2 pts | intenso · 3 pts | 8 |
| Geografía | Verde | claro · 1 pt | medio · 2 pts | intenso · 3 pts | 8 |
| Ciencias Naturales | Azul | claro · 1 pt | medio · 2 pts | intenso · 3 pts | 8 |
| Lengua y Literatura | Violeta | claro · 1 pt | medio · 2 pts | intenso · 3 pts | 8 |
| Educación Cívica | Naranja | claro · 1 pt | medio · 2 pts | intenso · 3 pts | 8 |

**Total:** 40 bloques + 1 base · 60 cartas · 5 materias × 3 niveles de dificultad

Detalle de colores hex y cantidad de bloques: [`datos/Materias_y_Bloques.pdf`](datos/Materias_y_Bloques.pdf)

---

## Archivos del proyecto

| Archivo | Descripción |
|---------|-------------|
| [`Jenga_Cultura_General_Reglas.pdf`](Jenga_Cultura_General_Reglas.pdf) | Reglas del juego |
| [`preguntas/SISTEMA_PUNTOS.pdf`](preguntas/SISTEMA_PUNTOS.pdf) | Explicación del sistema de puntajes |
| [`Hoja_de_Puntaje.pdf`](Hoja_de_Puntaje.pdf) | Planilla para anotar puntos por turno |
| [`preguntas/<materia>/nivel-<1\|2\|3>/cartas.pdf`](preguntas/) | Cartas de preguntas (15 mazos) |
| [`datos/Materias_y_Bloques.pdf`](datos/Materias_y_Bloques.pdf) | Tabla de materias, colores y bloques |
| [`3d/Jenga de Cultura General.stl`](3d/Jenga%20de%20Cultura%20General.stl) | Modelo 3D para imprimir (Fusion 360) |
| [`informe/INFORME.pdf`](informe/INFORME.pdf) | Informe escolar del trabajo |

### Cartas por materia

```
preguntas/
├── historia/   nivel-1 · nivel-2 · nivel-3
├── geografia/  nivel-1 · nivel-2 · nivel-3
├── ciencias/   nivel-1 · nivel-2 · nivel-3
├── lengua/     nivel-1 · nivel-2 · nivel-3
└── civica/     nivel-1 · nivel-2 · nivel-3
```

Cada `cartas.pdf` tiene 2 páginas (frente y dorso) para imprimir a doble cara y recortar.

---

## Para imprimir

- **Bloques 3D:** imprimir el STL en impresora FDM. Dimensiones estándar Jenga: 7,5 × 2,5 × 1,5 cm por bloque.
- **Cartas:** imprimir a doble cara, recortar (~72 × 100 mm).
- **Puntaje:** imprimir `Hoja_de_Puntaje.pdf` y anotar turno a turno.

---

## Informe

El informe del trabajo está en [`informe/INFORME.pdf`](informe/INFORME.pdf). La sección 6 (prueba de juego) se completa después de jugar una partida en clase.
