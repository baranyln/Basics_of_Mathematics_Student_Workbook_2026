# Solution: Exercise 8 — Row Operations and Their Reversibility

## 1. Problem Statement

For
$$A = \begin{pmatrix} 1 & 2 & -1 \\ 2 & 4 & 1 \\ -1 & 1 & 3 \end{pmatrix}$$
perform, in order:
1. $R_2 \leftarrow R_2 - 2R_1$,
2. $R_3 \leftarrow R_3 + R_1$,
3. interchange $R_2$ and $R_3$ ($R_2 \leftrightarrow R_3$).

Write the matrix after each step. Then, for each of the three operations, state an operation that reverses it.

---

## 2. Step-by-Step Mathematical Explanation

### Initial Matrix
$$A^{(0)} = \begin{pmatrix} 1 & 2 & -1 \\ 2 & 4 & 1 \\ -1 & 1 & 3 \end{pmatrix}$$

---

### Step 1: Row Operation $R_2 \leftarrow R_2 - 2R_1$
We subtract $2$ times row 1 from row 2:
$$R_2 = (2, 4, 1) - 2(1, 2, -1) = (2 - 2, 4 - 4, 1 - (-2)) = (0, 0, 3)$$

The updated matrix is:
$$A^{(1)} = \begin{pmatrix} 1 & 2 & -1 \\ 0 & 0 & 3 \\ -1 & 1 & 3 \end{pmatrix}$$

**Inverse Operation:**
To reverse subtracting $2R_1$ from $R_2$, we add $2R_1$ back to $R_2$:
$$R_2 \leftarrow R_2 + 2R_1$$

---

### Step 2: Row Operation $R_3 \leftarrow R_3 + R_1$
We add row 1 to row 3:
$$R_3 = (-1, 1, 3) + (1, 2, -1) = (-1 + 1, 1 + 2, 3 + (-1)) = (0, 3, 2)$$

The updated matrix is:
$$A^{(2)} = \begin{pmatrix} 1 & 2 & -1 \\ 0 & 0 & 3 \\ 0 & 3 & 2 \end{pmatrix}$$

**Inverse Operation:**
To reverse adding $R_1$ to $R_3$, we subtract $R_1$ from $R_3$:
$$R_3 \leftarrow R_3 - R_1$$

---

### Step 3: Row Operation $R_2 \leftrightarrow R_3$ (Row Swap)
We interchange row 2 and row 3:
- New Row 2: $(0, 3, 2)$
- New Row 3: $(0, 0, 3)$

The updated matrix is:
$$A^{(3)} = \begin{pmatrix} 1 & 2 & -1 \\ 0 & 3 & 2 \\ 0 & 0 & 3 \end{pmatrix}$$

**Inverse Operation:**
Interchanging the rows again restores the previous configuration (the swap operation is its own inverse):
$$R_2 \leftrightarrow R_3$$

---

### Summary of Elementary Operations and Inverses

| Step | Operation Applied | Resulting Matrix | Inverse Operation |
| :---: | :---: | :---: | :---: |
| **0** | *Initial* | $\begin{pmatrix} 1 & 2 & -1 \\ 2 & 4 & 1 \\ -1 & 1 & 3 \end{pmatrix}$ | — |
| **1** | $R_2 \leftarrow R_2 - 2R_1$ | $\begin{pmatrix} 1 & 2 & -1 \\ 0 & 0 & 3 \\ -1 & 1 & 3 \end{pmatrix}$ | $R_2 \leftarrow R_2 + 2R_1$ |
| **2** | $R_3 \leftarrow R_3 + R_1$ | $\begin{pmatrix} 1 & 2 & -1 \\ 0 & 0 & 3 \\ 0 & 3 & 2 \end{pmatrix}$ | $R_3 \leftarrow R_3 - R_1$ |
| **3** | $R_2 \leftrightarrow R_3$ | $\begin{pmatrix} 1 & 2 & -1 \\ 0 & 3 & 2 \\ 0 & 0 & 3 \end{pmatrix}$ | $R_2 \leftrightarrow R_3$ |

*Note: The resulting matrix $A^{(3)}$ is in upper triangular (row echelon) form.*

---

## 3. Python Implementation

```python
import numpy as np

def solve_exercise_8():
    # Initial matrix
    A0 = np.array([
        [ 1,  2, -1],
        [ 2,  4,  1],
        [-1,  1,  3]
    ], dtype=float)

    print("Initial Matrix A:\n", A0)

    # Step 1: R2 <- R2 - 2*R1
    A1 = A0.copy()
    A1[1] = A1[1] - 2 * A1[0]
    print("\nAfter Step 1 (R2 <- R2 - 2*R1):\n", A1)

    # Step 2: R3 <- R3 + R1
    A2 = A1.copy()
    A2[2] = A2[2] + A2[0]
    print("\nAfter Step 2 (R3 <- R3 + R1):\n", A2)

    # Step 3: Swap R2 and R3
    A3 = A2.copy()
    A3[[1, 2]] = A3[[2, 1]]
    print("\nAfter Step 3 (R2 <-> R3) [Row Echelon Form]:\n", A3)

    # Reversal Verification: apply inverse operations in reverse order
    A_rev = A3.copy()
    # Undo Step 3
    A_rev[[1, 2]] = A_rev[[2, 1]]
    # Undo Step 2
    A_rev[2] = A_rev[2] - A_rev[0]
    # Undo Step 1
    A_rev[1] = A_rev[1] + 2 * A_rev[0]

    print("\nMatrix after reversing all operations:\n", A_rev)
    assert np.allclose(A0, A_rev), "Inverse operations did not restore original matrix!"
    print("\nVerification successful: Original matrix fully restored.")

if __name__ == "__main__":
    solve_exercise_8()
```

---

## 4. Key Takeaways
- Elementary row operations preserve the solution set of linear systems.
- Every elementary row operation is reversible and corresponds to pre-multiplication by an invertible elementary matrix $E$.

