# Solution: Exercise 4 — Matrix Multiplication and Noncommutativity

## 1. Problem Statement

For
$$A = \begin{pmatrix} 1 & 2 \\ 0 & 1 \end{pmatrix}, \qquad B = \begin{pmatrix} 2 & 0 \\ 3 & 1 \end{pmatrix}$$
compute $AB$ and $BA$. Is $AB = BA$? Use this example to explain what noncommutativity of matrix multiplication means.

---

## 2. Step-by-Step Mathematical Explanation

### Definition of Matrix Multiplication
For matrices $A \in \mathbb{R}^{m \times p}$ and $B \in \mathbb{R}^{p \times n}$, the $(i, j)$-entry of $C = AB$ is the dot product of the $i$-th row of $A$ and the $j$-th column of $B$:
$$c_{ij} = \sum_{k=1}^p a_{ik} b_{kj}$$

---

### Step 1: Compute $AB$
$$AB = \begin{pmatrix} 1 & 2 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} 2 & 0 \\ 3 & 1 \end{pmatrix}$$

Calculating each entry:
- **Row 1, Column 1:** $(1)(2) + (2)(3) = 2 + 6 = 8$
- **Row 1, Column 2:** $(1)(0) + (2)(1) = 0 + 2 = 2$
- **Row 2, Column 1:** $(0)(2) + (1)(3) = 0 + 3 = 3$
- **Row 2, Column 2:** $(0)(0) + (1)(1) = 0 + 1 = 1$

$$AB = \begin{pmatrix} 8 & 2 \\ 3 & 1 \end{pmatrix}$$

---

### Step 2: Compute $BA$
$$BA = \begin{pmatrix} 2 & 0 \\ 3 & 1 \end{pmatrix} \begin{pmatrix} 1 & 2 \\ 0 & 1 \end{pmatrix}$$

Calculating each entry:
- **Row 1, Column 1:** $(2)(1) + (0)(0) = 2 + 0 = 2$
- **Row 1, Column 2:** $(2)(2) + (0)(1) = 4 + 0 = 4$
- **Row 2, Column 1:** $(3)(1) + (1)(0) = 3 + 0 = 3$
- **Row 2, Column 2:** $(3)(2) + (1)(1) = 6 + 1 = 7$

$$BA = \begin{pmatrix} 2 & 4 \\ 3 & 7 \end{pmatrix}$$

---

### Step 3: Comparison and Meaning of Noncommutativity
Comparing the results:
$$AB = \begin{pmatrix} 8 & 2 \\ 3 & 1 \end{pmatrix} \neq \begin{pmatrix} 2 & 4 \\ 3 & 7 \end{pmatrix} = BA$$

**Mathematical Meaning of Noncommutativity:**
1. In arithmetic over real numbers $\mathbb{R}$, multiplication is commutative: $a \cdot b = b \cdot a$ for all $a, b \in \mathbb{R}$.
2. In matrix algebra, matrix multiplication corresponds to the composition of linear transformations. The order in which operations or transformations are applied matters fundamentally:
   $$(T_A \circ T_B)(x) \neq (T_B \circ T_A)(x) \quad \text{in general.}$$
3. Hence, matrix multiplication is **noncommutative**. You cannot rearrange the order of factors in a matrix product without altering the result.

---

## 3. Python Implementation

```python
import numpy as np

def solve_exercise_4():
    A = np.array([
        [1, 2],
        [0, 1]
    ], dtype=int)

    B = np.array([
        [2, 0],
        [3, 1]
    ], dtype=int)

    # Compute products using the @ operator (matrix multiplication)
    AB = A @ B
    BA = B @ A

    print("Matrix A:\n", A)
    print("Matrix B:\n", B)
    print("\nAB =\n", AB)
    print("\nBA =\n", BA)
    print("\nAre AB and BA equal?", np.array_equal(AB, BA))

if __name__ == "__main__":
    solve_exercise_4()
```

---

## 4. Key Takeaways
- Even when both $AB$ and $BA$ are square matrices of the exact same size, $AB \neq BA$ in general.
- Algebraic identities known for numbers, such as $(A+B)^2 = A^2 + 2AB + B^2$, fail for matrices because $(A+B)^2 = A^2 + AB + BA + B^2$.

