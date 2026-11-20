# La caja telescópica

Diseño acordado el 20/11/2026. Escrito antes de tocar código.

## Qué y por qué

La caja del juego pasa a ser una **caja telescópica de dos piezas**: una
tapa que baja sobre la base y la cubre casi entera, como las cajas
rígidas de celular. Hoy la tapa es un sombrerito de 32 mm que apenas
asoma arriba.

Es un pedido de la materia: hay que entregar el modelado de la caja. El
uso real es imprimirla en 3D, imprimir el PDF del arte en papel y
pegarlo encima.

## Objetivos

- Que la caja cerrada se vea como el mockup: cuerpo ambarillo y una
  banda oscura abajo.
- Que la base siga guardando el juego completo, con sus dos
  compartimentos y el divisor.
- Que el arte se pueda pegar **sin sellar la caja**: cada hoja va
  entera sobre una sola pieza.

## No objetivos

- Cambiar el contenido ni cómo se acomodan los 60 bloques.
- Cambiar la altura de la caja cerrada. Sigue en 125 mm.
- Rehacer la identidad visual. El arte se recorta, no se rediseña.

## Anti-objetivos

Dos formas de que esto salga mal aunque técnicamente funcione:

- **Que una hoja de papel cruce la junta.** Pegás la caja y queda
  cerrada para siempre. Es el riesgo principal.
- **Que la tapa agarre.** Son 93 mm de recorrido entre dos paredes
  impresas. Con poca holgura entra una vez y no sale más.

## Restricciones

- Cama de impresión de 250 × 250 mm, con 10 mm de margen por lado.
- El arte se imprime en hojas planas y se pega: cada cara visible tiene
  que ser un rectángulo plano, de una sola pieza.
- La pila de bloques mide 120 mm y el interior de la base, 121. No hay
  margen para bajar la caja.

## Enfoques

Se evaluaron dos, iguales en forma y distintos en cuánto asoma la base:

**1 · Fiel al mockup, banda de 12 mm.** Es lo que dibuja el arte hoy
(el comentario en el generador dice *"banda oscura abajo, como la
tapa"*). La tapa queda de 113 mm y pesa unos 190 g. Se descartó por el
pegado: una tira de papel de 12 mm alrededor de una caja, a mano, sale
torcida, y se nota justo en el borde de abajo.

**2 · Banda de 30 mm. ELEGIDA.** La tapa cubre el 76 % y sigue leyéndose
como la caja del video. La tira de la base pasa a 30 mm, que se pega
cómoda. Ahorra 24 g contra la opción 1.

Se descartó antes de llegar a la mesa una tercera: que la tapa baje
hasta la mesa y tape la base por completo. No hay que recortar el arte,
pero se pierde la banda del mockup y el borde de la tapa raspa.

## Lo decidido

**La base no cambia.** 148 × 126 × 123 mm, con los dos compartimentos y
el divisor rebajado, tal cual está. Esto salió al revisar la geometría:
la tapa de hoy ya se encastra hacia abajo, sólo que es corta.

**La tapa pasa de 32 a 95 mm de alto.** Su cavidad es la altura menos
los 2 mm de pared, o sea 93 mm, y eso es lo que baja sobre la base:

```
   altura de la tapa   95 mm
   menos la pared       2 mm
   = cubre             93 mm
   la base mide       123 mm
   = banda a la vista  30 mm
   cerrada: 123 + 2 =  125 mm   (igual que hoy)
```

El número que se escribe es la banda, 30 mm; la altura de la tapa sale
de ahí, para que mover la banda no obligue a recalcular nada.

**Holgura entre tapa y base: de 0,35 a 0,5 mm por lado.** Mi decisión,
por el anti-objetivo de arriba: 0,35 alcanza para 30 mm de recorrido,
no para 93.

**El arte pasa de 4 caras a 6:**

| cara | medida | pieza |
|---|---|---|
| tapa (arriba) | 153,0 × 131,0 | tapa · sin cambios |
| frente | 153,0 × 95 | tapa |
| lateral | 131,0 × 95 | tapa · con muesca |
| frente de la base | 148 × 30 | base |
| lateral de la base | 126 × 30 | base |
| fondo | 148 × 126 | base · sin cambios |

La banda oscura de 12 mm que hoy llevan los costados **se borra del
arte**: a partir de ahora la banda es la base de verdad, impresa en
gris oscuro.

**Las dos caras laterales llevan una muesca.** La tapa tiene un rebaje
de 60 × 11 mm en el borde de abajo de cada lado corto, para poder
agarrarla. El papel de esas dos caras tiene que venir recortado con esa
muesca, o tapa el agarre.

**Costo:** la tapa pasa de 85 a 166 g, unas 7 horas más de impresora.
El juego completo, de 734 a 815 g.

## Lo que queda a criterio de quien lo construya

- Cómo se recorta el arte: lo natural es que las seis caras salgan del
  mismo generador que hoy hace cuatro, con las medidas calculadas desde
  la caja y no escritas a mano.
- Si la muesca del papel se dibuja como recorte real o como marca de
  corte punteada.
- El orden de las páginas del PDF.

## Qué se toca

- `make_caja.py` — la altura de la tapa y la holgura.
- `make_packaging.py` — las seis caras y la banda que se borra.
- `make_mockup.py` — el mockup tiene que mostrar las dos piezas.
- Los documentos que citan las medidas: README, memoria, informe.
