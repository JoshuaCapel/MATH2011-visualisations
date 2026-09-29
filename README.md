# Vector Field Line Integral App

This is a standalone HTML/JavaScript visualisation of a vector field and a cubic Bézier curve. The curve has four draggable control points, and the app displays the integrand

\[
\mathbf F(\mathbf r(t))\cdot\mathbf r'(t)
\]

as a graph against the Bézier parameter \(t\).

## Running the app

Open `vector-field-line-integrand.html` in a web browser. The app loads D3.js from jsDelivr, so an internet connection is required unless D3 is downloaded locally.

## Features

- Interactive SVG vector-field diagram.
- Cubic Bézier curve with four draggable control points.
- D3.js drag behaviour for mouse and touch interaction.
- Selectable vector fields:
  - \(\mathbf F=(-y,x)\)
  - \(\mathbf F=(1,0.5)\)
  - \(\mathbf F=(x,y)\)
  - \(\mathbf F=(y,x)\)
- Graph of \(\mathbf F(\mathbf r(t))\cdot\mathbf r'(t)\).
- Exact final line integral calculated from polynomial formulas.
- Reset button for restoring the initial Bézier curve.

## Mathematical setup

The curve is a cubic Bézier curve with control points \(p_0,p_1,p_2,p_3\):

\[
\mathbf r(t)=(1-t)^3p_0+3(1-t)^2tp_1+3(1-t)t^2p_2+t^3p_3,
\qquad 0\leq t\leq1.
\]

The screen-to-mathematical-coordinate conversion is:

```js
function screenToField(p) {
  return [(p.x - W / 2) / 55, (H / 2 - p.y) / 55];
}
```

Thus the mathematical positive \(y\)-direction points upwards, even though SVG screen coordinates increase downwards.

## Important functions

`F(x, y)` selects the current vector field.

`bez(t)` evaluates the Bézier curve.

`bezDeriv(t)` evaluates its derivative.

`compute()` samples the integrand for plotting:

```js
F(r(t)) · r'(t)
```

`exactIntegral()` calculates the final line integral using the supplied closed-form polynomial expressions in the four control points.

`drawCurve()` redraws the curve and attaches D3 drag behaviour to the control points.

`drawPlot()` redraws the integrand graph.

`update()` redraws the visualisation and updates the displayed exact integral.

## Possible future improvements

- Display the exact formula for the currently selected field.
- Add editable vector-field parameters.
- Show the point \(\mathbf r(t)\) and tangent vector as \(t\) changes.
- Add animation along the curve.
- Display both the integrand and cumulative integral.
- Bundle D3 locally so the app works offline.
