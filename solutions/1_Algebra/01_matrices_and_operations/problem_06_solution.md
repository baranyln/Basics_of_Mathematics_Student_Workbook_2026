# Solution: Exercise 6 — Transpose

## 1. Problem Statement

For
$$A = \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{pmatrix}, \qquad B = \begin{pmatrix} 1 & 0 \\ 2 & 1 \\ -1 & 3 \end{pmatrix}$$
compute $A^T$, $B^T$, and $AB$. Then verify in this example that
$$(AB)^T = B^T A^T.$$

---

## 2. Step-by-Step Mathematical Explanation

### Definition of Transpose
The transpose of an $m \times n$ matrix $M$, denoted $M^T$, is the $n \times m$ matrix obtained by interchanging its rows and columns:
$$(M^T)_{ij} = M_{ji}$$

---

### Step 1: Compute Transposes $A^T$ and $B^T$
- Matrix $A$ has size $2 \times 3$, so $A^T$ has size $3 \times 2$:
  $$A^T = \begin{pmatrix} 1 & 4 \\ 2 & 5 \\ 3 & 6 \end{pmatrix}$$

- Matrix $B$ has size $3 \times 2$, so $B^T$ has size $2 \times 3$:
  $$B^T = \begin{pmatrix} 1 & 2 & -1 \\ 0 & 1 & 3 \end{pmatrix}$$

---

### Step 2: Compute Product $AB$
$A$ is $2 \times 3$ and $B$ is $3 \times 2$, so $AB$ is $2 \times 2$:
$$AB = \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 2 & 1 \\ -1 & 3 \end{pmatrix}$$

Computing each entry:
- $(AB)_{11} = 1(1) + 2(2) + 3(-1) = 1 + 4 - 3 = 2$
- $(AB)_{12} = 1(0) + 2(1) + 3(3) = 0 + 2 + 9 = 11$
- $(AB)_{21} = 4(1) + 5(2) + 6(-1) = 4 + 10 - 6 = 8$
- $(AB)_{22} = 4(0) + 5(1) + 6(3) = 0 + 5 + 18 = 23$

$$AB = \begin{pmatrix} 2 & 11 \\ 8 & 23 \end{pmatrix}$$

---

### Step 3: Compute $(AB)^T$
Transposing $AB$:
$$(AB)^T = \begin{pmatrix} 2 & 8 \\ 11 & 23 \end{pmatrix}$$

---

### Step 4: Compute $B^T A^T$
$B^T$ is $2 \times 3$ and $A^T$ is $3 \times 2$, so the product $B^T A^T$ is $2 \times 2$:
$$B^T A^T = \begin{pmatrix} 1 & 2 & -1 \\ 0 & 1 & 3 \end{pmatrix} \begin{pmatrix} 1 & 4 \\ 2 & 5 \\ 3 & 6 \end{pmatrix}$$

Computing each entry:
- $(B^T A^T)_{11} = 1(1) + 2(2) + (-1)(3) = 1 + 4 - 3 = 2$
- $(B^T A^T)_{12} = 1(4) + 2(5) + (-1)(6) = 4 + 10 - 6 = 8$
- $(B^T A^T)_{21} = 0(1) + 1(2) + 3(3) = 0 + 2 + 9 = 11$
- $(B^T A^T)_{22} = 0(4) + 1(5) + 3(6) = 0 + 5 + 18 = 23$

$$B^T A^T = \begin{pmatrix} 2 & 8 \\ 11 & 23 \end{pmatrix}$$

---

### Verification and General Property
We observe that:
$$(AB)^T = \begin{pmatrix} 2 & 8 \\ 11 & 23 \end{pmatrix} = B^T A^T$$

**General proof why order reverses:**
$$((AB)^T)_{ij} = (AB)_{ji} = \sum_{k} a_{jk} b_{ki} = \sum_k (A^T)_{kj} (B^T)_{ik} = \sum_k (B^T)_{ik} (A^T)_{kj} = (B^T A^T)_{ij}$$
The row index of $AB$ comes from rows of $A$ and column index from columns of $B$. Transposing swaps the roles of rows and columns, reversing the product order.

---

## 3. Python Implementation

```python
import numpy as np

def solve_exercise_6():
    A = np.array([
        [1, 2, 3],
        [4, 5, 6]
    ], dtype=int)

    B = np.array([
        [ 1, 0],
        [ 2, 1],
        [-1, 3]
    ], dtype=int)

    # Transposition
    A_T = A.T
    B_T = B.T

    # Matrix multiplication
    AB = A @ B
    AB_T = AB.T
    BT_AT = B_T @ A_T

    print("A^T =\n", A_T)
    print("\nB^T =\n", B_T)
    print("\nAB =\n", AB)
    print("\n(AB)^T =\n", AB_T)
    print("\nB^T * A^T =\n", BT_AT)

    # Mathematical verification
    assert np.array_equal(AB_T, BT_AT), "Transpose product rule failed!"
    print("\nIdentity (AB)^T == B^T A^T holds true.")

if __name__ == "__main__":
    solve_exercise_6()
```

---

## 4. Key Takeaways
- Transposition reverses the order of factors: $(AB)^T = B^T A^T$.
- By extension to $k$ matrices: $(A_1 A_2 \cdots A_k)^T = A_k^T \cdots A_2^T A_1^T$.

