# Solution: Exercise 2 — Addition and Scalar Multiplication

## 1. Problem Statement

For
$$A = \begin{pmatrix} 1 & 2 \\ -1 & 3 \end{pmatrix}, \qquad B = \begin{pmatrix} 4 & -2 \\ 0 & 5 \end{pmatrix}$$
compute:
$$A+B, \qquad A-B, \qquad 3A-2B.$$
Explain why matrix addition is possible only for matrices of the same size.

---

## 2. Step-by-Step Mathematical Explanation

### Definition of Matrix Addition and Scalar Multiplication
Let $A = (a_{ij})$ and $B = (b_{ij})$ be matrices of the same size $m \times n$, and let $c \in \mathbb{R}$ be a scalar.
- **Addition:** $(A + B)_{ij} = a_{ij} + b_{ij}$
- **Subtraction:** $(A - B)_{ij} = a_{ij} - b_{ij}$
- **Scalar Multiplication:** $(c A)_{ij} = c \cdot a_{ij}$

Both $A$ and $B$ are $2 \times 2$ matrices, so all linear combinations are well-defined.

---

### Step 1: Compute $A + B$
$$A + B = \begin{pmatrix} 1 & 2 \\ -1 & 3 \end{pmatrix} + \begin{pmatrix} 4 & -2 \\ 0 & 5 \end{pmatrix} = \begin{pmatrix} 1 + 4 & 2 + (-2) \\ -1 + 0 & 3 + 5 \end{pmatrix} = \begin{pmatrix} 5 & 0 \\ -1 & 8 \end{pmatrix}$$

---

### Step 2: Compute $A - B$
$$A - B = \begin{pmatrix} 1 & 2 \\ -1 & 3 \end{pmatrix} - \begin{pmatrix} 4 & -2 \\ 0 & 5 \end{pmatrix} = \begin{pmatrix} 1 - 4 & 2 - (-2) \\ -1 - 0 & 3 - 5 \end{pmatrix} = \begin{pmatrix} -3 & 4 \\ -1 & -2 \end{pmatrix}$$

---

### Step 3: Compute $3A - 2B$
First, perform scalar multiplication:
$$3A = 3 \begin{pmatrix} 1 & 2 \\ -1 & 3 \end{pmatrix} = \begin{pmatrix} 3 \cdot 1 & 3 \cdot 2 \\ 3 \cdot (-1) & 3 \cdot 3 \end{pmatrix} = \begin{pmatrix} 3 & 6 \\ -3 & 9 \end{pmatrix}$$

$$2B = 2 \begin{pmatrix} 4 & -2 \\ 0 & 5 \end{pmatrix} = \begin{pmatrix} 2 \cdot 4 & 2 \cdot (-2) \\ 2 \cdot 0 & 2 \cdot 5 \end{pmatrix} = \begin{pmatrix} 8 & -4 \\ 0 & 10 \end{pmatrix}$$

Now subtract $2B$ from $3A$:
$$3A - 2B = \begin{pmatrix} 3 & 6 \\ -3 & 9 \end{pmatrix} - \begin{pmatrix} 8 & -4 \\ 0 & 10 \end{pmatrix} = \begin{pmatrix} 3 - 8 & 6 - (-4) \\ -3 - 0 & 9 - 10 \end{pmatrix} = \begin{pmatrix} -5 & 10 \\ -3 & -1 \end{pmatrix}$$

---

### Explanation: Why Addition Requires Identical Dimensions
Matrix addition is defined **entry-by-entry** (component-wise):
$$(A + B)_{ij} = a_{ij} + b_{ij}$$
For this operation to produce a valid matrix:
1. Every entry $a_{ij}$ of $A$ must correspond to a unique entry $b_{ij}$ of $B$.
2. If matrix $A$ has dimensions $m_1 \times n_1$ and matrix $B$ has dimensions $m_2 \times n_2$ with $m_1 \neq m_2$ or $n_1 \neq n_2$, there exist indices $(i, j)$ that exist in one matrix but not in the other.
3. Therefore, no binary addition operation between their entries can be completed, making addition undefined.

---

## 3. Python Implementation

```python
import numpy as np

def solve_exercise_2():
    A = np.array([
        [ 1,  2],
        [-1,  3]
    ], dtype=int)

    B = np.array([
        [ 4, -2],
        [ 0,  5]
    ], dtype=int)

    # Computations
    A_plus_B = A + B
    A_minus_B = A - B
    threeA_minus_twoB = 3 * A - 2 * B

    print("A + B =\n", A_plus_B)
    print("\nA - B =\n", A_minus_B)
    print("\n3A - 2B =\n", threeA_minus_twoB)

    # Verification of shapes
    assert A.shape == B.shape, "Matrices must have identical shapes for addition."

if __name__ == "__main__":
    solve_exercise_2()
```

---

## 4. Key Takeaways
- Matrix addition and scalar multiplication inherit the algebraic properties of the underlying real numbers: commutativity ($A+B = B+A$), associativity ($(A+B)+C = A+(B+C)$), and distributivity ($c(A+B) = cA + cB$).

