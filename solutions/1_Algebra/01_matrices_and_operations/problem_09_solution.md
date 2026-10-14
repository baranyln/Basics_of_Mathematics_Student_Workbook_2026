# Solution: Exercise 9 — Composing Transformations

## 1. Problem Statement

Let
$$S = \begin{pmatrix} 2 & 0 \\ 0 & 1 \end{pmatrix}, \qquad R = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix}$$
The matrix $S$ describes nonuniform scaling (doubles the $x$-coordinate, leaves $y$ unchanged), while $R$ describes a $90^\circ$ counterclockwise rotation.

For
$$x = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$$
compute $RSx$ and $SRx$. Compare the results and explain geometrically why the order of these transformations matters.

---

## 2. Step-by-Step Mathematical Explanation

### Transformation Interpretation
A matrix-vector product $M x$ transforms vector $x$ under the linear map associated with $M$.
- When composing two transformations $A$ and $B$, the notation $(AB)x = A(Bx)$ means transformation $B$ is applied **first**, followed by transformation $A$.

---

### Step 1: Compute $RSx$ (Scale first, then Rotate)
1. Apply $S$ to $x$:
   $$Sx = \begin{pmatrix} 2 & 0 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \begin{pmatrix} 2(1) + 0(2) \\ 0(1) + 1(2) \end{pmatrix} = \begin{pmatrix} 2 \\ 2 \end{pmatrix}$$
2. Now apply $R$ to $(Sx)$:
   $$RSx = R(Sx) = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix} \begin{pmatrix} 2 \\ 2 \end{pmatrix} = \begin{pmatrix} 0(2) + (-1)(2) \\ 1(2) + 0(2) \end{pmatrix} = \begin{pmatrix} -2 \\ 2 \end{pmatrix}$$

Alternatively, compute the composite matrix $RS$:
$$RS = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix} \begin{pmatrix} 2 & 0 \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} 0 & -1 \\ 2 & 0 \end{pmatrix} \implies RSx = \begin{pmatrix} 0 & -1 \\ 2 & 0 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \begin{pmatrix} -2 \\ 2 \end{pmatrix}$$

---

### Step 2: Compute $SRx$ (Rotate first, then Scale)
1. Apply $R$ to $x$:
   $$Rx = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \begin{pmatrix} 0(1) + (-1)(2) \\ 1(1) + 0(2) \end{pmatrix} = \begin{pmatrix} -2 \\ 1 \end{pmatrix}$$
2. Now apply $S$ to $(Rx)$:
   $$SRx = S(Rx) = \begin{pmatrix} 2 & 0 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} -2 \\ 1 \end{pmatrix} = \begin{pmatrix} 2(-2) + 0(1) \\ 0(-2) + 1(1) \end{pmatrix} = \begin{pmatrix} -4 \\ 1 \end{pmatrix}$$

Alternatively, compute the composite matrix $SR$:
$$SR = \begin{pmatrix} 2 & 0 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix} = \begin{pmatrix} 0 & -2 \\ 1 & 0 \end{pmatrix} \implies SRx = \begin{pmatrix} 0 & -2 \\ 1 & 0 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \begin{pmatrix} -4 \\ 1 \end{pmatrix}$$

---

### Step 3: Comparison and Geometric Explanation

Comparing results:
$$RSx = \begin{pmatrix} -2 \\ 2 \end{pmatrix} \neq \begin{pmatrix} -4 \\ 1 \end{pmatrix} = SRx$$

**Geometric Explanation:**
- **In $RSx$ (Scale $\to$ Rotate):**
  1. The initial point $(1, 2)$ has its horizontal coordinate doubled to $(2, 2)$.
  2. Rotating by $90^\circ$ counterclockwise sends $(x, y) \mapsto (-y, x)$, moving $(2, 2)$ to $(-2, 2)$.
- **In $SRx$ (Rotate $\to$ Scale):**
  1. The initial point $(1, 2)$ is rotated $90^\circ$ first, mapping it to $(-2, 1)$. Here, the original $y$-component ($2$) has become the new $x$-coordinate (with a sign change, $-2$).
  2. The scaling matrix $S$ acts strictly along the coordinate $x$-axis, doubling the current $x$-coordinate: $(-2) \times 2 = -4$. The resulting vector is $(-4, 1)$.

**Conclusion:**
Because nonuniform scaling acts along fixed coordinate axes, rotating a vector prior to scaling completely changes which geometric direction undergoes stretching. Hence, geometric transformations do not commute in general.

---

## 3. Python Implementation

```python
import numpy as np

def solve_exercise_9():
    S = np.array([
        [2, 0],
        [0, 1]
    ], dtype=float)

    R = np.array([
        [0, -1],
        [1,  0]
    ], dtype=float)

    x = np.array([1, 2], dtype=float)

    # Order 1: Scale then Rotate
    RSx = R @ (S @ x)
    RS_matrix = R @ S

    # Order 2: Rotate then Scale
    SRx = S @ (R @ x)
    SR_matrix = S @ R

    print("x =", x)
    print("RSx (Scale then Rotate) =", RSx)
    print("SRx (Rotate then Scale) =", SRx)
    print("\nMatrix RS:\n", RS_matrix)
    print("Matrix SR:\n", SR_matrix)
    print("\nDo the composite matrices commute?", np.allclose(RS_matrix, SR_matrix))

if __name__ == "__main__":
    solve_exercise_9()
```

---

## 4. Key Takeaways
- Matrix multiplication represents composition of functions: $(A \circ B)(x) = A(B(x))$.
- The rightmost matrix acts first on the vector.
- Noncommutativity of matrix multiplication directly mirrors the noncommutativity of spatial transformations in geometry.

