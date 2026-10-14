# Solution: Exercise 1 — Matrix Size and Entries

## 1. Problem Statement

Given the matrices:
$$A = \begin{pmatrix} 2 & -1 & 3 \\ 0 & 4 & 5 \end{pmatrix}, \qquad B = \begin{pmatrix} 1 & 0 \\ -2 & 3 \\ 4 & 1 \end{pmatrix}$$

1. State the sizes of matrices $A$ and $B$.
2. Read off the entries $a_{12}$, $a_{23}$, $b_{21}$, and $b_{32}$.
3. Write the second row of $A$ and the first column of $B$ as vectors.

---

## 2. Step-by-Step Mathematical Explanation

### Step 1: Matrix Sizes
A matrix with $m$ rows and $n$ columns has size $m \times n$ (read "$m$ by $n$").
- For matrix $A$:
  $$A = \begin{pmatrix} 2 & -1 & 3 \\ 0 & 4 & 5 \end{pmatrix}$$
  There are $2$ horizontal rows and $3$ vertical columns.
  $$\text{Size of } A = 2 \times 3$$

- For matrix $B$:
  $$B = \begin{pmatrix} 1 & 0 \\ -2 & 3 \\ 4 & 1 \end{pmatrix}$$
  There are $3$ horizontal rows and $2$ vertical columns.
  $$\text{Size of } B = 3 \times 2$$

### Step 2: Reading Matrix Entries
In standard mathematical notation, $m_{ij}$ denotes the entry in the $i$-th row and $j$-th column of matrix $M$.
- $a_{12}$: Entry of $A$ at row 1, column 2 $\implies a_{12} = -1$.
- $a_{23}$: Entry of $A$ at row 2, column 3 $\implies a_{23} = 5$.
- $b_{21}$: Entry of $B$ at row 2, column 1 $\implies b_{21} = -2$.
- $b_{32}$: Entry of $B$ at row 3, column 2 $\implies b_{32} = 1$.

### Step 3: Extracting Row and Column Vectors
- **Second row of $A$** (denoted $a_{2\cdot}$ or $r_2(A)$):
  $$r_2(A) = \begin{pmatrix} 0 & 4 & 5 \end{pmatrix} \quad \text{or as a tuple } (0, 4, 5) \in \mathbb{R}^3$$
- **First column of $B$** (denoted $b_{\cdot 1}$ or $c_1(B)$):
  $$c_1(B) = \begin{pmatrix} 1 \\ -2 \\ 4 \end{pmatrix} \quad \text{or } (1, -2, 4)^T \in \mathbb{R}^3$$

---

## 3. Python Implementation

```python
import numpy as np

def solve_exercise_1():
    # Define matrices A and B
    A = np.array([
        [2, -1, 3],
        [0,  4, 5]
    ])

    B = np.array([
        [ 1, 0],
        [-2, 3],
        [ 4, 1]
    ])

    # 1. Sizes (shapes)
    size_A = A.shape
    size_B = B.shape

    # 2. Reading entries (Note: Python uses 0-based indexing)
    # a_12 -> row 0, col 1
    # a_23 -> row 1, col 2
    # b_21 -> row 1, col 0
    # b_32 -> row 2, col 1
    a_12 = A[0, 1]
    a_23 = A[1, 2]
    b_21 = B[1, 0]
    b_32 = B[2, 1]

    # 3. Row and column vectors
    second_row_A = A[1, :]
    first_col_B = B[:, 0]

    # Verification / Output
    print(f"Size of A: {size_A[0]}x{size_A[1]}")
    print(f"Size of B: {size_B[0]}x{size_B[1]}")
    print(f"Entries: a_12 = {a_12}, a_23 = {a_23}, b_21 = {b_21}, b_32 = {b_32}")
    print(f"Second row of A: {second_row_A}")
    print(f"First col of B (as column):\n{first_col_B.reshape(-1, 1)}")

if __name__ == "__main__":
    solve_exercise_1()
```

---

## 4. Key Takeaways

1. **Size convention:** Always row count first, column count second ($m \times n$).
2. **Index offset:** In mathematics, indices are 1-based ($a_{11}$ is top-left), whereas in Python/NumPy, indices are 0-based (`A[0, 0]`).
3. **Vectors as matrices:** A row vector of length $n$ is a $1 \times n$ matrix, while a column vector of length $m$ is an $m \times 1$ matrix.

