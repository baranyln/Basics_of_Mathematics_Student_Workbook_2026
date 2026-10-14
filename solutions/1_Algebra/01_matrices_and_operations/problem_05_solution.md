# Solution: Exercise 5 — Matrix Times Vector

## 1. Problem Statement

Let
$$A = \begin{pmatrix} 2 & -1 \\ 1 & 3 \end{pmatrix}, \qquad x = \begin{pmatrix} 4 \\ 2 \end{pmatrix}$$
Compute $Ax$. Then express $Ax$ as a linear combination of the columns of $A$, with coefficients coming from the vector $x$.

---

## 2. Step-by-Step Mathematical Explanation

### Method 1: Row-by-Column (Inner Product) View
Multiplying the rows of $A$ by vector $x$:
$$Ax = \begin{pmatrix} 2 & -1 \\ 1 & 3 \end{pmatrix} \begin{pmatrix} 4 \\ 2 \end{pmatrix} = \begin{pmatrix} (2)(4) + (-1)(2) \\ (1)(4) + (3)(2) \end{pmatrix} = \begin{pmatrix} 8 - 2 \\ 4 + 6 \end{pmatrix} = \begin{pmatrix} 6 \\ 10 \end{pmatrix}$$

---

### Method 2: Column View (Linear Combination of Columns)
Let the columns of matrix $A$ be denoted by $a_1$ and $a_2$:
$$a_1 = \begin{pmatrix} 2 \\ 1 \end{pmatrix}, \qquad a_2 = \begin{pmatrix} -1 \\ 3 \end{pmatrix}$$

The vector $x$ has components $x_1 = 4$ and $x_2 = 2$.
By the column definition of matrix-vector multiplication:
$$Ax = x_1 a_1 + x_2 a_2$$

Substituting the values:
$$Ax = 4 \begin{pmatrix} 2 \\ 1 \end{pmatrix} + 2 \begin{pmatrix} -1 \\ 3 \end{pmatrix} = \begin{pmatrix} 4 \cdot 2 \\ 4 \cdot 1 \end{pmatrix} + \begin{pmatrix} 2 \cdot (-1) \\ 2 \cdot 3 \end{pmatrix} = \begin{pmatrix} 8 \\ 4 \end{pmatrix} + \begin{pmatrix} -2 \\ 6 \end{pmatrix} = \begin{pmatrix} 8 + (-2) \\ 4 + 6 \end{pmatrix} = \begin{pmatrix} 6 \\ 10 \end{pmatrix}$$

---

### Significance
Both viewpoints yield the identical result $\begin{pmatrix} 6 \\ 10 \end{pmatrix}$.
- **Row view:** Each element of the output vector is a scalar projection (dot product) of a row onto the input vector.
- **Column view:** The output vector lies in the **column space** $\text{Col}(A)$; it is a weighted combination of the basis directions spanned by the columns of $A$, weighted by the coordinates of $x$.

---

## 3. Python Implementation

```python
import numpy as np

def solve_exercise_5():
    A = np.array([
        [2, -1],
        [1,  3]
    ], dtype=float)

    x = np.array([4, 2], dtype=float)

    # 1. Standard matrix-vector multiplication
    Ax = A @ x

    # 2. Linear combination of columns
    col1 = A[:, 0]
    col2 = A[:, 1]
    Ax_linear_comb = x[0] * col1 + x[1] * col2

    print("Matrix A:\n", A)
    print("Vector x:", x)
    print("\nAx (Matrix multiplication):\n", Ax)
    print("Ax (Linear combination of columns):\n", Ax_linear_comb)

    # Mathematical verification
    assert np.allclose(Ax, Ax_linear_comb), "Both methods must yield identical results!"
    print("\nVerification successful: Ax equals 4*col1 + 2*col2.")

if __name__ == "__main__":
    solve_exercise_5()
```

---

## 4. Key Takeaways
- The column perspective $Ax = \sum x_j a_j$ is fundamental to understanding systems of linear equations: solving $Ax = b$ means finding the weights $x$ needed to express $b$ as a linear combination of the columns of $A$.

