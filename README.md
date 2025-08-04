# Spinning Pyramid
This code will render a spinning pyramid using ASCII character hash (#). This use basic linear algebra and trigonometry. This is one of the hardest shapes that i did.

## Pyramid
A square-based pyramid consists of:

- **4 base vertices** forming a square
- **1 apex** above (or below) the center of the base
- **4 triangular faces** connecting the apex to each side of the base

I use Cartesian coordinates for 5 key points of the pyramid

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
