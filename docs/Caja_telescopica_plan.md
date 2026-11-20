# Plan: la caja telescópica

> **Para quien lo ejecute:** los pasos van con casilla (`- [ ]`) para ir
> tachándolos. Cada tarea termina en algo verificable por sí solo.

**Objetivo:** que la tapa cubra el 76 % de la caja en vez del 24 %, y que
el arte se parta en seis hojas para poder pegarlo sin sellar la caja.

**Cómo:** la base no se toca. La tapa sube de 32 a 95 mm, calculada desde
una constante `BANDA` en vez de escrita. El arte pasa de cuatro caras a
seis, todas derivadas de `medidas()`, y las dos laterales de la tapa
llevan recortada la muesca de agarre.

**Herramientas:** Python, reportlab para los PDF, trimesh para medir las
mallas, pymupdf para el mockup.

**Diseño:** [docs/Caja_telescopica.md](Caja_telescopica.md)

## Restricciones generales

- Cama de 250 × 250 mm con 10 mm de margen: nada puede pasar de 230.
- Altura de la caja cerrada: **125 mm**, igual que hoy.
- Banda de base a la vista: **30 mm**.
- Holgura tapa/base: **0,5 mm por lado** (era 0,35).
- Ninguna medida del arte se escribe a mano: todas salen de
  `make_caja.medidas()`.
- Este proyecto no tiene tests unitarios. Lo que hace de test es correr
  el generador y medir lo que sale: mallas con `trimesh`, PDF con
  `pdftotext` y el tamaño de página con `pymupdf`.

## A qué prestarle atención

Cinco formas de que esto pase todas las verificaciones y aun así falle
en la mano. Cada una tiene su chequeo en la tarea que la provoca:

1. **La tapa agarra y no sale.** 93 mm de recorrido entre dos paredes
   impresas. El interior de la tapa tiene que ser el exterior de la base
   más 2 × 0,5 mm. → Tarea 1.
2. **Una hoja de arte cruza la junta.** Si alguna página que no sea la
   tapa de arriba o el fondo mide más de 95 mm de alto, al pegarla sellás
   la caja. → Tarea 2.
3. **La banda y la tapa no cierran la cuenta.** 93 (lo que cubre la tapa)
   + 30 (la banda) tiene que dar 123, el alto de la base. Si no, queda
   una franja de plástico desnudo o papel sobrante. → Tarea 2.
4. **El papel tapa el agarre.** La muesca de 60 × 11 mm va en los lados
   cortos de la tapa, que miden 131 mm de ancho. El recorte del papel
   tiene que caer en el mismo lugar, y la única forma de garantizarlo es
   que las dos salgan del mismo número: hoy `ANCHO_MUESCA` y
   `FONDO_MUESCA` viven adentro de `tapa()` en `make_caja.py` y el arte
   no los ve. → Tarea 2.
5. **Al cambiar la escala del bloque el arte queda viejo.** Ya pasó dos
   veces en este proyecto. Las seis caras tienen que seguir a la caja
   sin tocar nada. → Tarea 2.

---

### Tarea 1: La tapa sube a 95 mm

**Archivos:**
- Modificar: `jenga-fuentes/make_caja.py`

**Interfaces:**
- Produce: `BANDA = 30.0` y `JUEGO_TAPA = 0.5` a nivel de módulo;
  `medidas()["tapa"]` pasa a devolver `(153.0, 131.0, 95.0)`.
- Consume: nada nuevo.

- [ ] **Paso 1: escribir la verificación, que todavía falla**

En `C:\Users\joaqu\jenga-fuentes\verificar_caja.py`:

```python
import make_caja
m = make_caja.medidas()
tw, tl, th = m["tapa"]
assert th == 95.0, th
assert m["H"] + make_caja.PISO == 125.0            # cerrada
assert m["H"] - (th - make_caja.PISO) == 30.0      # banda a la vista
assert tw - m["W"] == 2 * (make_caja.JUEGO_TAPA + make_caja.PARED)
assert make_caja.JUEGO_TAPA == 0.5
assert (make_caja.ANCHO_MUESCA, make_caja.FONDO_MUESCA) == (60.0, 11.0)
```

Ojo con el ancho: al subir la holgura de 0,35 a 0,5 la tapa pasa de
152,7 × 130,7 a **153,0 × 131,0**. El diseño decía 152,7 porque se
escribió antes de decidir la holgura; el arte lo sigue solo porque sale
de `medidas()`.

- [ ] **Paso 2: correrla y ver que falla**

`python verificar_caja.py` → `AssertionError: 32.0`

- [ ] **Paso 3: implementar**

En `make_caja.py`: agregar `BANDA = 30.0` junto a las otras constantes,
con un comentario de por qué 30 y no 12. Cambiar `JUEGO_TAPA` de `0.35`
a `0.5`. En `medidas()`, el tercer valor de `tapa` pasa de `32.0` a
`H_ext + PISO - BANDA`. Subir `ANCHO_MUESCA = 60.0` y
`FONDO_MUESCA = 11.0` de adentro de `tapa()` a nivel de módulo, para que
el arte pueda importarlos (riesgo 4).

- [ ] **Paso 4: correrla y ver que pasa**

`python verificar_caja.py` → sin salida.

- [ ] **Paso 5: regenerar y medir la malla**

`python make_caja.py C:/Users/joaqu/Juego-Nietardo`
Esperado: `Tapa ... 153.0 x 131.0 x 95.0 mm ... CERRADA`, y la caja sin
cambios en `148.0 x 126.0 x 123.0`.

- [ ] **Paso 6: confirmar que entra en la cama**

El lado mayor de la tapa es 153 mm, contra 230 útiles.

- [ ] **Paso 7: commit**

```bash
git add stl/ docs/
git commit -m "La tapa cubre 93 mm en vez de 30"
```

---

### Tarea 2: El arte pasa a seis caras

**Archivos:**
- Modificar: `jenga-fuentes/make_packaging.py`

**Interfaces:**
- Consume: `make_caja.medidas()` de la tarea 1.
- Produce: `CARAS` con seis claves — `tapa`, `frente`, `lateral`,
  `banda_frente`, `banda_lateral`, `fondo`. El PDF sale con seis
  páginas, en ese orden.
- También de la tarea 1: `make_caja.ANCHO_MUESCA = 60.0` y
  `FONDO_MUESCA = 11.0` suben a nivel de módulo, para que el arte use
  los mismos números que la pieza en vez de repetirlos.

- [ ] **Paso 1: escribir la verificación, que todavía falla**

En `C:\Users\joaqu\jenga-fuentes\verificar_arte.py`:

```python
import pymupdf, make_caja, make_packaging as mp
m = make_caja.medidas()
BANDA, PISO = 30.0, make_caja.PISO
tw, tl, th = m["tapa"]

assert set(mp.CARAS) == {"tapa", "frente", "lateral",
                         "banda_frente", "banda_lateral", "fondo"}
assert mp.CARAS["frente"] == (tw, th)              # la cara de la tapa
assert mp.CARAS["lateral"] == (tl, th)
assert mp.CARAS["banda_frente"] == (m["W"], BANDA)
assert mp.CARAS["banda_lateral"] == (m["L"], BANDA)
# riesgo 3: la cuenta cierra
assert (th - PISO) + BANDA == m["H"]
# riesgo 2: ninguna hoja cruza la junta
for clave, (_, alto) in mp.CARAS.items():
    if clave not in ("tapa", "fondo"):
        assert alto <= th, (clave, alto)

d = pymupdf.open(r"C:\Users\joaqu\Juego-Nietardo\packaging\Arte_de_la_caja.pdf")
assert d.page_count == 6, d.page_count
MM = 72 / 25.4
borde = 2 * (mp.SANGRADO + mp.MARCA)
for pag, clave in enumerate(["tapa", "fondo", "frente", "lateral",
                             "banda_frente", "banda_lateral"]):
    a, b = mp.CARAS[clave]
    r = d[pag].rect
    assert abs(r.width - (a * MM + borde)) < 0.5, (clave, r.width)
    assert abs(r.height - (b * MM + borde)) < 0.5, (clave, r.height)
```

- [ ] **Paso 2: correrla y ver que falla**

`python verificar_arte.py` → falla en el `set(mp.CARAS)`.

- [ ] **Paso 3: ampliar `_caras()` a seis**

Las cuatro nuevas medidas salen de `m` y de `BANDA`, importada de
`make_caja`. `frente` y `lateral` pasan a usar el ancho de la **tapa**
(`tw`, `tl`), no el de la base: la tapa es la que se ve.

- [ ] **Paso 4: partir `cara_lateral` en dos funciones**

`cara_lateral(c, clave, titulo)` queda para las caras altas de la tapa y
**pierde la banda oscura de 12 mm**, que ahora es la base de verdad.
Nueva `cara_banda(c, clave, titulo)`: fondo `FONDO`, el título en
`GRIS_MEDIO` centrado, sin logo — es una tira de 30 mm.

- [ ] **Paso 5: recortar la muesca en las dos caras laterales**

`MUESCA = (60.0, 11.0)` a nivel de módulo. En `cara_lateral`, cuando la
clave es `lateral`, dibujar el recorte centrado en el borde de abajo:
rectángulo en blanco sobre el arte más una línea punteada de corte,
igual que las marcas de las esquinas.

- [ ] **Paso 6: emitir las seis páginas en `__main__`**

Orden: `tapa`, `fondo`, `frente`, `lateral`, `banda_frente`,
`banda_lateral`. El `print` final lista las seis con su medida.

- [ ] **Paso 7: regenerar y correr la verificación**

```bash
python make_packaging.py C:/Users/joaqu/Juego-Nietardo
python verificar_arte.py
```
Esperado: seis páginas, sin salida de la verificación.

- [ ] **Paso 8: riesgo 5 — que el arte siga a la caja**

Correr la verificación con el bloque a otra escala y ver que sigue
pasando:

```bash
python -c "import contenido; contenido.BLOQUE=(75.,25.,15.)" && python verificar_arte.py
```
Si alguna medida estuviera escrita a mano, acá revienta.

- [ ] **Paso 9: commit**

```bash
git add packaging/ docs/
git commit -m "El arte se parte en seis caras, una por pieza"
```

---

### Tarea 3: El mockup muestra las dos piezas

**Archivos:**
- Modificar: `jenga-fuentes/make_mockup.py`

**Interfaces:**
- Consume: el PDF de seis páginas de la tarea 2.

- [ ] **Paso 1: corregir los índices de página**

`cara_del_pdf(pdf, 2)` y `(pdf, 3)` siguen siendo frente y lateral, pero
ahora son las caras **de la tapa**, de 95 mm. Agregar las páginas 4 y 5,
las bandas.

- [ ] **Paso 2: pegar cada cara en su franja de altura**

Las caras de la tapa van de 30 a 125 mm; las bandas, de 0 a 30.
`pegar_cara` ya recibe las cuatro esquinas en mm, así que es cuestión de
pasarle las de cada franja.

- [ ] **Paso 3: regenerar y mirarlo**

`python make_mockup.py C:/Users/joaqu/Juego-Nietardo` y abrir
`packaging/Mockup_de_la_caja.png`. Tiene que verse el cuerpo ambarillo
con la banda oscura abajo, sin corte visible entre las dos.

- [ ] **Paso 4: commit**

---

### Tarea 4: Los documentos

**Archivos:**
- Modificar: `jenga-fuentes/make_memoria.py`, `make_readme.py`

- [ ] **Paso 1: la memoria**

El párrafo de la caja tiene que decir que son dos piezas y cuánto cubre
la tapa. La tabla de filamento ya sale de `filamento.py`, así que los
gramos se actualizan solos.

- [ ] **Paso 2: regenerar todo**

```bash
for s in make_memoria make_readme; do python $s.py C:/Users/joaqu/Juego-Nietardo; done
```

- [ ] **Paso 3: que no quede ninguna medida vieja**

Correr el barrido de medidas sobre los 25 documentos buscando `32 mm`,
`152,7`, `130,7` y `12 mm` de banda. Esperado: ninguno.

- [ ] **Paso 4: verificar las 16 piezas 3D de punta a punta**

Cerradas, orientadas y dentro de la cama.

- [ ] **Paso 5: commit y push**
