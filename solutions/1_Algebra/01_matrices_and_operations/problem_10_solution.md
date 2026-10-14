# Solution: Exercise 10 — Columns of a Matrix Product

## 1. Problem Statement

Given
$$A = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 1 \end{pmatrix}, \qquad B = \begin{pmatrix} 1 & 2 \\ -1 & 0 \\ 3 & 1 \end{pmatrix}$$
Denote the columns of $B$ by $b_1, b_2$.

1. Compute $Ab_1$ and $Ab_2$.
2. Compute the matrix $AB$.
3. Compare the results and explain why the columns of $AB$ are exactly the vectors $Ab_1$ and $Ab_2$.

---

## 2. Step-by-Step Mathematical Explanation

### Column Decomposition of $B$
The matrix $B$ is a $3 \times 2$ matrix whose columns are:
$$b_1 = \begin{pmatrix} 1 \\ -1 \\ 3 \end{pmatrix}, \qquad b_2 = \begin{pmatrix} 2 \\ 0 \\ 1 \end{pmatrix}$$
We can represent $B$ in partitioned column form:
$$B = \begin{pmatrix} b_1 & b_2 \end{pmatrix}$$

---

### Step 1: Compute $Ab_1$ and $Ab_2$
- **Computing $Ab_1$:**
  $$Ab_1 = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 1 \end{pmatrix} \begin{pmatrix} 1 \\ -1 \\ 3 \end{pmatrix} = \begin{pmatrix} 1(1) + 2(-1) + 0(3) \\ 0(1) + 1(-1) + 1(3) \end{pmatrix} = \begin{pmatrix} 1 - 2 + 0 \\ 0 - 1 + 3 \end{pmatrix} = \begin{pmatrix} -1 \\ 2 \end{pmatrix}$$

- **Computing $Ab_2$:**
  $$Ab_2 = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 1 \end{pmatrix} \begin{pmatrix} 2 \\ 0 \\ 1 \end{pmatrix} = \begin{pmatrix} 1(2) + 2(0) + 0(1) \\ 0(2) + 1(0) + 1(1) \end{pmatrix} = \begin{pmatrix} 2 + 0 + 0 \\ 0 + 0 + 1 \end{pmatrix} = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$$

---

### Step 2: Compute the Full Product $AB$
$A$ is $2 \times 3$ and $B$ is $3 \times 2$, so $AB$ is $2 \times 2$:
$$AB = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 1 \end{pmatrix} \begin{pmatrix} 1 & 2 \\ -1 & 0 \\ 3 & 1 \end{pmatrix}$$

Computing each entry:
- $(AB)_{11} = 1(1) + 2(-1) + 0(3) = 1 - 2 + 0 = -1$
- $(AB)_{12} = 1(2) + 2(0) + 0(1) = 2 + 0 + 0 = 2$
- $(AB)_{21} = 0(1) + 1(-1) + 1(3) = 0 - 1 + 3 = 2$
- $(AB)_{22} = 0(2) + 1(0) + 1(1) = 0 + 0 + 1 = 1$

$$AB = \begin{pmatrix} -1 & 2 \\ 2 & 1 \end{pmatrix}$$

---

### Step 3: Comparison and Column-by-Column Interpretation

Notice that:
$$\text{Column 1 of } AB = \begin{pmatrix} -1 \\ 2 \end{pmatrix} = Ab_1$$
$$\text{Column 2 of } AB = \begin{pmatrix} 2 \\ 1 \end{pmatrix} = Ab_2$$
Thus:
$$AB = \begin{pmatrix} Ab_1 & Ab_2 \end{pmatrix}$$

**Mathematical Explanation:**
By definition of matrix multiplication, the entry in the $i$-th row and $j$-th column of $AB$ is the dot product of row $i$ of $A$ with column $j$ of $B$:
$$(AB)_{ij} = \text{row}_i(A) \cdot b_j$$
Since this holds for every row $i = 1, \dots, m$, the entire $j$-th column of $AB$ is simply the matrix $A$ applied to the $j$-th column vector of $B$:
$$\text{col}_j(AB) = A \cdot b_j$$

**Conceptual Meaning:**
Matrix multiplication $AB$ can be viewed as applying the linear transformation represented by matrix $A$ simultaneously to each column vector of $B$.

---

## 3. Python Implementation

```python
import numpy as np

def solve_exercise_10():
    A = np.array([
        [1, 2, 0],
        [0, 1, 1]
    ], dtype=int)

    B = np.array([
        [ 1, 2],
        [-1, 0],
        [ 3, 1]
    ], dtype=int)

    # 1. Column vectors of B
    b1 = B[:, 0]
    b2 = B[:, 1]

    # Compute A @ b1 and A @ b2
    Ab1 = A @ b1
    Ab2 = A @ b2

    # 2. Compute full matrix product AB
    AB = A @ B

    # 3. Assemble column-wise
    AB_from_cols = np.column_stack((Ab1, Ab2))

    print("Ab1:\n", Ab1)
    print("Ab2:\n", Ab2)
    print("\nFull product AB:\n", AB)
    print("\nAB reconstructed from columns [Ab1, Ab2]:\n", AB_from_cols)

    # Verification
    assert np.array_equal(AB, AB_from_cols), "Column property failed!"
    print("\nVerification successful: AB = [Ab1, Ab2].")

if __name__ == "__main__":
    solve_exercise_10()
```

---

## 4. Key Takeaways
- Matrix multiplication can be decomposed column-by-column: $A \begin{pmatrix} b_1 & \cdots & b_k \end{pmatrix} = \begin{pmatrix} Ab_1 & \cdots & Ab_k \end{pmatrix}$.
- This property is widely used in algorithms (e.g., parallelizing matrix operations across columns) and theoretical linear algebra.

