# Spinning Pyramid
This code will render a spinning pyramid using ASCII character hash (#). This use basic linear algebra and trigonometry. This is one of the hardest shapes that I did.

## Pyramid
A square-based pyramid consists of:

- **4 base vertices** forming a square
- **1 apex** above (or below) the center of the base
- **4 triangular faces** connecting the apex to each side of the base

I use Cartesian coordinates for 5 key points of the pyramid:

```js
[
  [1, 1, -1],   // base front-right
  [-1, 1, -1],  // base front-left
  [-1, 1, 1],   // base back-left
  [1, 1, 1],    // base back-right
  [0, -1, 0]    // apex
]
```
This will create a pyramid pointing upward.

## 3D Spinning
I rotate the pyramid around the Y-axis using the Y-axis rotation matrix:
$\begin{pmatrix} \cos(\theta) & 0 & \sin(\theta) \\ 0 & 1 & 0 \\ -\sin(\theta) & 0 & \cos(\theta) \end{pmatrix}$

Applied to each vertex (x, y, z), it produces the rotated point:

```js
const xRot = x * cos - z * sin;
const zRot = x * sin + z * cos;
```
This gives a realistic horizontal rotation.

## Perspective Projection

To show depth and 3D perspective on 2D canvas, we use this simple projection:

$$ x' = \frac{x}{z+d}, \quad y' = \frac{y}{z+d} $$

Where <kbd>d</kbd> is camera's depth factor. We use:

```js
const perspective = 5;
const xProj = xRot / (zRot + perspective);
const yProj = y / (zRot + perspective);
```

This ensures points farther away appear smaller (perspective effect).

## Screen Mapping
The 2D projected coordinates are mapped to the ASCII canvas:

```js
const screenX = Math.round((xProj + 1) * canvasSize / 2);
const screenY = Math.round((yProj + 1) * canvasSize / 2);
```
This centers the projection and fits it to the grid size.
