# Complete Solutions: 01 — Matrices and Operations

This document contains full, rigorous mathematical solutions and Python implementations for all 15 exercises from [`exercises/1_Algebra/01_matrices_and_operations_en.md`](file:///c:/Users/sbara/OneDrive/Masa%C3%BCst%C3%BC/Basics_of_Mathematics_Student_Workbook_2026/exercises/1_Algebra/01_matrices_and_operations_en.md).

---

## Table of Contents
- [Basic Exercises](#basic-exercises)
  - [Exercise 1: Matrix Size and Entries](#exercise-1-matrix-size-and-entries)
  - [Exercise 2: Addition and Scalar Multiplication](#exercise-2-addition-and-scalar-multiplication)
  - [Exercise 3: When Can Matrices Be Multiplied?](#exercise-3-when-can-matrices-be-multiplied)
  - [Exercise 4: Matrix Multiplication and Noncommutativity](#exercise-4-matrix-multiplication-and-noncommutativity)
  - [Exercise 5: Matrix Times Vector](#exercise-5-matrix-times-vector)
  - [Exercise 6: Transpose](#exercise-6-transpose)
  - [Exercise 7: Identity Matrix, Zero Matrix, and Powers](#exercise-7-identity-matrix-zero-matrix-and-powers)
  - [Exercise 8: Row Operations and Their Reversibility](#exercise-8-row-operations-and-their-reversibility)
  - [Exercise 9: Composing Transformations](#exercise-9-composing-transformations)
  - [Exercise 10: Columns of a Matrix Product](#exercise-10-columns-of-a-matrix-product)
- [More Challenging Exercises](#more-challenging-exercises)
  - [Exercise 11: When Do Matrices Commute?](#exercise-11-when-do-matrices-commute)
  - [Exercise 12: Formula for a Matrix Power](#exercise-12-formula-for-a-matrix-power)
  - [Exercise 13: A Recurrence Written in Matrix Form](#exercise-13-a-recurrence-written-in-matrix-form)
  - [Exercise 14: Rotation Matrices](#exercise-14-rotation-matrices)
  - [Exercise 15: Associativity of Multiplication and Different Calculation Paths](#exercise-15-associativity-of-multiplication-and-different-calculation-paths)

---

## Basic Exercises

### Exercise 1: Matrix Size and Entries

#### Problem
Given
$$A = \begin{pmatrix} 2 & -1 & 3 \\ 0 & 4 & 5 \end{pmatrix}, \qquad B = \begin{pmatrix} 1 & 0 \\ -2 & 3 \\ 4 & 1 \end{pmatrix}$$
1. State the sizes of matrices $A$ and $B$.
2. Read off the entries $a_{12}$, $a_{23}$, $b_{21}$, and $b_{32}$.
3. Write the second row of $A$ and the first column of $B$ as vectors.

#### Mathematical Solution
1. **Matrix Sizes:**
   - Matrix $A$ has $2$ rows and $3$ columns $\implies \mathbf{2 \times 3}$.
   - Matrix $B$ has $3$ rows and $2$ columns $\implies \mathbf{3 \times 2}$.
2. **Entries:**
   - $a_{12} = -1$ (row 1, column 2 of $A$).
   - $a_{23} = 5$ (row 2, column 3 of $A$).
   - $b_{21} = -2$ (row 2, column 1 of $B$).
   - $b_{32} = 1$ (row 3, column 2 of $B$).
3. **Vectors:**
   - Second row of $A$: $r_2(A) = \begin{pmatrix} 0 & 4 & 5 \end{pmatrix}$ or $(0, 4, 5) \in \mathbb{R}^3$.
   - First column of $B$: $c_1(B) = \begin{pmatrix} 1 \\ -2 \\ 4 \end{pmatrix} \in \mathbb{R}^3$.

#### Python Code
```python
import numpy as np

A = np.array([[2, -1, 3], [0, 4, 5]])
B = np.array([[1, 0], [-2, 3], [4, 1]])

print("Size of A:", A.shape)
print("Size of B:", B.shape)
print("Entries: a12 =", A[0, 1], "a23 =", A[1, 2], "b21 =", B[1, 0], "b32 =", B[2, 1])
print("Row 2 of A:", A[1, :])
print("Col 1 of B:", B[:, 0])
```

---

### Exercise 2: Addition and Scalar Multiplication

#### Problem
For
$$A = \begin{pmatrix} 1 & 2 \\ -1 & 3 \end{pmatrix}, \qquad B = \begin{pmatrix} 4 & -2 \\ 0 & 5 \end{pmatrix}$$
compute $A+B$, $A-B$, and $3A-2B$. Explain why matrix addition is possible only for matrices of the same size.

#### Mathematical Solution
- **Sum $A+B$:**
  $$A+B = \begin{pmatrix} 1+4 & 2+(-2) \\ -1+0 & 3+5 \end{pmatrix} = \begin{pmatrix} 5 & 0 \\ -1 & 8 \end{pmatrix}$$
- **Difference $A-B$:**
  $$A-B = \begin{pmatrix} 1-4 & 2-(-2) \\ -1-0 & 3-5 \end{pmatrix} = \begin{pmatrix} -3 & 4 \\ -1 & -2 \end{pmatrix}$$
- **Linear Combination $3A-2B$:**
  $$3A - 2B = \begin{pmatrix} 3 & 6 \\ -3 & 9 \end{pmatrix} - \begin{pmatrix} 8 & -4 \\ 0 & 10 \end{pmatrix} = \begin{pmatrix} -5 & 10 \\ -3 & -1 \end{pmatrix}$$
- **Dimension requirement:**
  Matrix addition is defined element-wise: $(A+B)_{ij} = a_{ij} + b_{ij}$. This requires a strict one-to-one matching between entries of both matrices across all row and column indices.

#### Python Code
```python
import numpy as np

A = np.array([[1, 2], [-1, 3]])
B = np.array([[4, -2], [0, 5]])

print("A + B =\n", A + B)
print("A - B =\n", A - B)
print("3A - 2B =\n", 3 * A - 2 * B)
```

---

### Exercise 3: When Can Matrices Be Multiplied?

#### Problem
Sizes: $A_{2\times3}$, $B_{3\times4}$, $C_{4\times2}$, $D_{2\times2}$.
Determine whether $AB, BA, BC, CB, AC, CA, AD, DA$ are defined, give the size if defined, and justify using dimension compatibility.

#### Mathematical Solution
Rule: $M_{p \times q} N_{r \times s}$ is defined $\iff q = r$, resulting in dimension $p \times s$.

- **$AB$:** $(2\times 3)(3\times 4)$ $\implies$ **Defined**, size **$2 \times 4$** ($3 = 3$).
- **$BA$:** $(3\times 4)(2\times 3)$ $\implies$ **Undefined** ($4 \neq 2$).
- **$BC$:** $(3\times 4)(4\times 2)$ $\implies$ **Defined**, size **$3 \times 2$** ($4 = 4$).
- **$CB$:** $(4\times 2)(3\times 4)$ $\implies$ **Undefined** ($2 \neq 3$).
- **$AC$:** $(2\times 3)(4\times 2)$ $\implies$ **Undefined** ($3 \neq 4$).
- **$CA$:** $(4\times 2)(2\times 3)$ $\implies$ **Defined**, size **$4 \times 3$** ($2 = 2$).
- **$AD$:** $(2\times 3)(2\times 2)$ $\implies$ **Undefined** ($3 \neq 2$).
- **$DA$:** $(2\times 2)(2\times 3)$ $\implies$ **Defined**, size **$2 \times 3$** ($2 = 2$).

#### Python Code
```python
sizes = {'A': (2, 3), 'B': (3, 4), 'C': (4, 2), 'D': (2, 2)}
pairs = ['AB', 'BA', 'BC', 'CB', 'AC', 'CA', 'AD', 'DA']

for p in pairs:
    r1, c1 = sizes[p[0]]
    r2, c2 = sizes[p[1]]
    if c1 == r2:
        print(f"{p}: Defined, size {r1}x{c2}")
    else:
        print(f"{p}: Undefined (mismatch {c1} != {r2})")
```

---

### Exercise 4: Matrix Multiplication and Noncommutativity

#### Problem
For
$$A = \begin{pmatrix} 1 & 2 \\ 0 & 1 \end{pmatrix}, \qquad B = \begin{pmatrix} 2 & 0 \\ 3 & 1 \end{pmatrix}$$
compute $AB$ and $BA$. Is $AB = BA$? Explain noncommutativity.

#### Mathematical Solution
- **$AB$:**
  $$AB = \begin{pmatrix} 1(2)+2(3) & 1(0)+2(1) \\ 0(2)+1(3) & 0(0)+1(1) \end{pmatrix} = \begin{pmatrix} 8 & 2 \\ 3 & 1 \end{pmatrix}$$
- **$BA$:**
  $$BA = \begin{pmatrix} 2(1)+0(0) & 2(2)+0(1) \\ 3(1)+1(0) & 3(2)+1(1) \end{pmatrix} = \begin{pmatrix} 2 & 4 \\ 3 & 7 \end{pmatrix}$$
- **Noncommutativity:**
  $AB \neq BA$. In general linear algebra, the order of composition matters: applying transformation $B$ then $A$ is not identical to applying $A$ then $B$.

#### Python Code
```python
import numpy as np

A = np.array([[1, 2], [0, 1]])
B = np.array([[2, 0], [3, 1]])

AB = A @ B
BA = B @ A
print("AB =\n", AB)
print("BA =\n", BA)
print("AB == BA?", np.array_equal(AB, BA))
```

---

### Exercise 5: Matrix Times Vector

#### Problem
Let
$$A = \begin{pmatrix} 2 & -1 \\ 1 & 3 \end{pmatrix}, \qquad x = \begin{pmatrix} 4 \\ 2 \end{pmatrix}$$
Compute $Ax$, and express $Ax$ as a linear combination of the columns of $A$.

#### Mathematical Solution
- **Row-column product:**
  $$Ax = \begin{pmatrix} 2(4) + (-1)(2) \\ 1(4) + 3(2) \end{pmatrix} = \begin{pmatrix} 8 - 2 \\ 4 + 6 \end{pmatrix} = \begin{pmatrix} 6 \\ 10 \end{pmatrix}$$
- **Linear combination of columns:**
  Let columns be $a_1 = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$, $a_2 = \begin{pmatrix} -1 \\ 3 \end{pmatrix}$:
  $$Ax = 4 \begin{pmatrix} 2 \\ 1 \end{pmatrix} + 2 \begin{pmatrix} -1 \\ 3 \end{pmatrix} = \begin{pmatrix} 8 \\ 4 \end{pmatrix} + \begin{pmatrix} -2 \\ 6 \end{pmatrix} = \begin{pmatrix} 6 \\ 10 \end{pmatrix}$$

#### Python Code
```python
import numpy as np

A = np.array([[2, -1], [1, 3]])
x = np.array([4, 2])

Ax_dot = A @ x
Ax_comb = x[0] * A[:, 0] + x[1] * A[:, 1]
print("Ax (matrix mul) =", Ax_dot)
print("Ax (linear comb) =", Ax_comb)
```

---

### Exercise 6: Transpose

#### Problem
For
$$A = \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{pmatrix}, \qquad B = \begin{pmatrix} 1 & 0 \\ 2 & 1 \\ -1 & 3 \end{pmatrix}$$
compute $A^T, B^T, AB$, and verify $(AB)^T = B^T A^T$.

#### Mathematical Solution
- **Transposes:**
  $$A^T = \begin{pmatrix} 1 & 4 \\ 2 & 5 \\ 3 & 6 \end{pmatrix}, \qquad B^T = \begin{pmatrix} 1 & 2 & -1 \\ 0 & 1 & 3 \end{pmatrix}$$
- **Product $AB$:**
  $$AB = \begin{pmatrix} 1(1)+2(2)+3(-1) & 1(0)+2(1)+3(3) \\ 4(1)+5(2)+6(-1) & 4(0)+5(1)+6(3) \end{pmatrix} = \begin{pmatrix} 2 & 11 \\ 8 & 23 \end{pmatrix}$$
- **Transpose of Product:**
  $$(AB)^T = \begin{pmatrix} 2 & 8 \\ 11 & 23 \end{pmatrix}$$
- **Product of Transposes in Reverse Order:**
  $$B^T A^T = \begin{pmatrix} 1 & 2 & -1 \\ 0 & 1 & 3 \end{pmatrix} \begin{pmatrix} 1 & 4 \\ 2 & 5 \\ 3 & 6 \end{pmatrix} = \begin{pmatrix} 1+4-3 & 4+10-6 \\ 0+2+9 & 0+5+18 \end{pmatrix} = \begin{pmatrix} 2 & 8 \\ 11 & 23 \end{pmatrix}$$
  Identity $(AB)^T = B^T A^T$ holds.

#### Python Code
```python
import numpy as np

A = np.array([[1, 2, 3], [4, 5, 6]])
B = np.array([[1, 0], [2, 1], [-1, 3]])

AB = A @ B
print("(AB)^T =\n", AB.T)
print("B^T @ A^T =\n", B.T @ A.T)
assert np.array_equal(AB.T, B.T @ A.T)
```

---

### Exercise 7: Identity Matrix, Zero Matrix, and Powers

#### Problem
For $A = \begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix}$, compute $AI, IA, A+0, A^2, A^3$. Explain the roles of $I, 0$ and the power pattern.

#### Mathematical Solution
- $AI = IA = A$ (multiplicative identity).
- $A + 0 = A$ (additive identity).
- Powers:
  $$A^2 = \begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix}\begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix} = \begin{pmatrix} 4 & 4 \\ 0 & 4 \end{pmatrix}$$
  $$A^3 = A^2 A = \begin{pmatrix} 4 & 4 \\ 0 & 4 \end{pmatrix}\begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix} = \begin{pmatrix} 8 & 12 \\ 0 & 8 \end{pmatrix}$$
- **Pattern:**
  Notice $A = 2I + N$ with $N = \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}$ ($N^2 = 0$). By the binomial theorem:
  $$A^n = (2I + N)^n = 2^n I + n 2^{n-1} N = \begin{pmatrix} 2^n & n 2^{n-1} \\ 0 & 2^n \end{pmatrix}$$

#### Python Code
```python
import numpy as np

A = np.array([[2, 1], [0, 2]])
I = np.eye(2, dtype=int)
zero = np.zeros((2, 2), dtype=int)

print("A^2 =\n", A @ A)
print("A^3 =\n", A @ A @ A)
for n in range(1, 5):
    print(f"A^{n} formula match:", np.array_equal(np.linalg.matrix_power(A, n), [[2**n, n * 2**(n-1)], [0, 2**n]]))
```

---

### Exercise 8: Row Operations and Their Reversibility

#### Problem
For $A = \begin{pmatrix} 1 & 2 & -1 \\ 2 & 4 & 1 \\ -1 & 1 & 3 \end{pmatrix}$, perform:
1. $R_2 \leftarrow R_2 - 2R_1$,
2. $R_3 \leftarrow R_3 + R_1$,
3. Swap $R_2 \leftrightarrow R_3$.
State the reverse operations.

#### Mathematical Solution
1. **$R_2 \leftarrow R_2 - 2R_1$:**
   $$R_2 = (2, 4, 1) - 2(1, 2, -1) = (0, 0, 3) \implies A^{(1)} = \begin{pmatrix} 1 & 2 & -1 \\ 0 & 0 & 3 \\ -1 & 1 & 3 \end{pmatrix}$$
   *Inverse:* $R_2 \leftarrow R_2 + 2R_1$.
2. **$R_3 \leftarrow R_3 + R_1$:**
   $$R_3 = (-1, 1, 3) + (1, 2, -1) = (0, 3, 2) \implies A^{(2)} = \begin{pmatrix} 1 & 2 & -1 \\ 0 & 0 & 3 \\ 0 & 3 & 2 \end{pmatrix}$$
   *Inverse:* $R_3 \leftarrow R_3 - R_1$.
3. **Swap $R_2 \leftrightarrow R_3$:**
   $$A^{(3)} = \begin{pmatrix} 1 & 2 & -1 \\ 0 & 3 & 2 \\ 0 & 0 & 3 \end{pmatrix}$$
   *Inverse:* Swap $R_2 \leftrightarrow R_3$.

#### Python Code
```python
import numpy as np

A = np.array([[1, 2, -1], [2, 4, 1], [-1, 1, 3]], dtype=float)
A[1] = A[1] - 2 * A[0]
A[2] = A[2] + A[0]
A[[1, 2]] = A[[2, 1]]
print("Matrix after row operations (row echelon form):\n", A)
```

---

### Exercise 9: Composing Transformations

#### Problem
$S = \begin{pmatrix} 2 & 0 \\ 0 & 1 \end{pmatrix}$ (scale $x$ by 2), $R = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix}$ ($90^\circ$ CCW rotation), $x = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$. Compute $RSx$ and $SRx$. Explain geometrically.

#### Mathematical Solution
- **$RSx$ (Scale, then Rotate):**
  $$Sx = \begin{pmatrix} 2 \\ 2 \end{pmatrix} \implies RSx = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix}\begin{pmatrix} 2 \\ 2 \end{pmatrix} = \begin{pmatrix} -2 \\ 2 \end{pmatrix}$$
- **$SRx$ (Rotate, then Scale):**
  $$Rx = \begin{pmatrix} -2 \\ 1 \end{pmatrix} \implies SRx = \begin{pmatrix} 2 & 0 \\ 0 & 1 \end{pmatrix}\begin{pmatrix} -2 \\ 1 \end{pmatrix} = \begin{pmatrix} -4 \\ 1 \end{pmatrix}$$
- **Geometric explanation:**
  Nonuniform scaling acts specifically along the coordinate $x$-axis. If the vector is rotated first, its geometric components swap axes, causing different components to be doubled.

#### Python Code
```python
import numpy as np

S = np.array([[2, 0], [0, 1]])
R = np.array([[0, -1], [1, 0]])
x = np.array([1, 2])

print("RSx =", R @ (S @ x))
print("SRx =", S @ (R @ x))
```

---

### Exercise 10: Columns of a Matrix Product

#### Problem
$A = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 1 \end{pmatrix}, B = \begin{pmatrix} 1 & 2 \\ -1 & 0 \\ 3 & 1 \end{pmatrix}$. Columns of $B$ are $b_1, b_2$.
Compute $Ab_1, Ab_2, AB$, and compare.

#### Mathematical Solution
- $Ab_1 = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 1 \end{pmatrix}\begin{pmatrix} 1 \\ -1 \\ 3 \end{pmatrix} = \begin{pmatrix} -1 \\ 2 \end{pmatrix}$
- $Ab_2 = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 1 \end{pmatrix}\begin{pmatrix} 2 \\ 0 \\ 1 \end{pmatrix} = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$
- $AB = \begin{pmatrix} 1(1)+2(-1)+0(3) & 1(2)+2(0)+0(1) \\ 0(1)+1(-1)+1(3) & 0(2)+1(0)+1(1) \end{pmatrix} = \begin{pmatrix} -1 & 2 \\ 2 & 1 \end{pmatrix}$
- **Conclusion:** $AB = \begin{pmatrix} Ab_1 & Ab_2 \end{pmatrix}$. Applying matrix $A$ to matrix $B$ transforms each column of $B$ individually under $A$.

#### Python Code
```python
import numpy as np

A = np.array([[1, 2, 0], [0, 1, 1]])
B = np.array([[1, 2], [-1, 0], [3, 1]])

b1, b2 = B[:, 0], B[:, 1]
print("Ab1 =", A @ b1)
print("Ab2 =", A @ b2)
print("AB =\n", A @ B)
```

---

## More Challenging Exercises

### Exercise 11: When Do Matrices Commute?

#### Problem
Find conditions on $a, b, c, d$ such that $AB = BA$ for $A = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$ and $B = \begin{pmatrix} a & b \\ c & d \end{pmatrix}$.

#### Mathematical Solution
- $AB = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}\begin{pmatrix} a & b \\ c & d \end{pmatrix} = \begin{pmatrix} a+c & b+d \\ c & d \end{pmatrix}$
- $BA = \begin{pmatrix} a & b \\ c & d \end{pmatrix}\begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} a & a+b \\ c & c+d \end{pmatrix}$
- Setting $AB = BA$:
  - $a + c = a \implies c = 0$
  - $b + d = a + b \implies d = a$
- **General form:**
  $$B = \begin{pmatrix} a & b \\ 0 & a \end{pmatrix} = (a - b)I + bA, \qquad a, b \in \mathbb{R}$$
  The matrices commuting with $A$ are upper-triangular matrices with equal diagonal entries (polynomials in $A$).

#### Python Code
```python
import sympy as sp

a, b, c, d = sp.symbols('a b c d')
A = sp.Matrix([[1, 1], [0, 1]])
B = sp.Matrix([[a, b], [c, d]])
comm = A * B - B * A
print("Commutator equations:", sp.solve(list(comm), (a, b, c, d)))
```

---

### Exercise 12: Formula for a Matrix Power

#### Problem
For $A = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$, compute $A^2, A^3, A^4$, conjecture $A^n$, and prove by mathematical induction.

#### Mathematical Solution
- $A^1 = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}, A^2 = \begin{pmatrix} 1 & 2 \\ 0 & 1 \end{pmatrix}, A^3 = \begin{pmatrix} 1 & 3 \\ 0 & 1 \end{pmatrix}, A^4 = \begin{pmatrix} 1 & 4 \\ 0 & 1 \end{pmatrix}$.
- **Conjecture:** $A^n = \begin{pmatrix} 1 & n \\ 0 & 1 \end{pmatrix}$ for all $n \in \mathbb{N}$.
- **Induction proof:**
  - *Base step ($n=1$):* True since $A^1 = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$.
  - *Inductive step:* Assume $A^k = \begin{pmatrix} 1 & k \\ 0 & 1 \end{pmatrix}$.
    $$A^{k+1} = A^k A = \begin{pmatrix} 1 & k \\ 0 & 1 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} 1(1)+k(0) & 1(1)+k(1) \\ 0(1)+1(0) & 0(1)+1(1) \end{pmatrix} = \begin{pmatrix} 1 & k+1 \\ 0 & 1 \end{pmatrix}$$
    The formula holds for $k+1$. By mathematical induction, it holds for all $n \ge 1$.

#### Python Code
```python
import numpy as np

A = np.array([[1, 1], [0, 1]])
for n in range(1, 10):
    assert np.array_equal(np.linalg.matrix_power(A, n), [[1, n], [0, 1]])
print("Induction conjecture verified numerically up to n=10.")
```

---

### Exercise 13: A Recurrence Written in Matrix Form

#### Problem
Let $F = \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix}$. Compute $F^2, F^3, F^4, F^5$. Compare with Fibonacci numbers. Explain $F \begin{pmatrix} a \\ b \end{pmatrix}$.

#### Mathematical Solution
Fibonacci sequence: $f_0=0, f_1=1, f_2=1, f_3=2, f_4=3, f_5=5, f_6=8, \dots$
- $F^1 = \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix} = \begin{pmatrix} f_2 & f_1 \\ f_1 & f_0 \end{pmatrix}$
- $F^2 = \begin{pmatrix} 2 & 1 \\ 1 & 1 \end{pmatrix} = \begin{pmatrix} f_3 & f_2 \\ f_2 & f_1 \end{pmatrix}$
- $F^3 = \begin{pmatrix} 3 & 2 \\ 2 & 1 \end{pmatrix} = \begin{pmatrix} f_4 & f_3 \\ f_3 & f_2 \end{pmatrix}$
- $F^4 = \begin{pmatrix} 5 & 3 \\ 3 & 2 \end{pmatrix} = \begin{pmatrix} f_5 & f_4 \\ f_4 & f_3 \end{pmatrix}$
- $F^5 = \begin{pmatrix} 8 & 5 \\ 5 & 3 \end{pmatrix} = \begin{pmatrix} f_6 & f_5 \\ f_5 & f_4 \end{pmatrix}$
- **General form:** $F^n = \begin{pmatrix} f_{n+1} & f_n \\ f_n & f_{n-1} \end{pmatrix}$.
- **Recurrence step:**
  $$F \begin{pmatrix} a \\ b \end{pmatrix} = \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix}\begin{pmatrix} a \\ b \end{pmatrix} = \begin{pmatrix} a + b \\ a \end{pmatrix}$$
  The matrix sums the two most recent values for the new first entry, while shifting the previous first entry into the second position.

#### Python Code
```python
import numpy as np

F = np.array([[1, 1], [1, 0]], dtype=int)
curr = F.copy()
for p in range(1, 6):
    print(f"F^{p} =\n{curr}")
    curr = curr @ F
```

---

### Exercise 14: Rotation Matrices

#### Problem
For $R(\theta) = \begin{pmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{pmatrix}$, show $R(\alpha)R(\beta) = R(\alpha+\beta)$ and explain geometrically.

#### Mathematical Solution
$$R(\alpha)R(\beta) = \begin{pmatrix} \cos\alpha & -\sin\alpha \\ \sin\alpha & \cos\alpha \end{pmatrix} \begin{pmatrix} \cos\beta & -\sin\beta \\ \sin\beta & \cos\beta \end{pmatrix}$$
- $(1, 1): \cos\alpha\cos\beta - \sin\alpha\sin\beta = \cos(\alpha+\beta)$
- $(1, 2): -\cos\alpha\sin\beta - \sin\alpha\cos\beta = -\sin(\alpha+\beta)$
- $(2, 1): \sin\alpha\cos\beta + \cos\alpha\sin\beta = \sin(\alpha+\beta)$
- $(2, 2): -\sin\alpha\sin\beta + \cos\alpha\cos\beta = \cos(\alpha+\beta)$
$$R(\alpha)R(\beta) = \begin{pmatrix} \cos(\alpha+\beta) & -\sin(\alpha+\beta) \\ \sin(\alpha+\beta) & \cos(\alpha+\beta) \end{pmatrix} = R(\alpha+\beta)$$
- **Geometric explanation:**
  A rotation by $\beta$ followed by a rotation by $\alpha$ about the origin in $\mathbb{R}^2$ results in a single net rotation through angle $\alpha+\beta$. Since real angle addition is commutative, planar rotations commute: $R(\alpha)R(\beta) = R(\beta)R(\alpha)$.

#### Python Code
```python
import sympy as sp

alpha, beta = sp.symbols('alpha beta', real=True)
def R(t):
    return sp.Matrix([[sp.cos(t), -sp.sin(t)], [sp.sin(t), sp.cos(t)]])

prod = sp.trigsimp(R(alpha) * R(beta))
print("Simplified R(alpha) * R(beta):\n", prod)
assert prod == R(alpha + beta)
```

---

### Exercise 15: Associativity of Multiplication and Different Calculation Paths

#### Problem
$A_{2\times 3} = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 1 \end{pmatrix}, B_{3\times 2} = \begin{pmatrix} 1 & 0 \\ 2 & 1 \\ -1 & 3 \end{pmatrix}, C_{2\times 2} = \begin{pmatrix} 2 & 1 \\ 0 & -1 \end{pmatrix}$.
Compute $(AB)C$ and $A(BC)$. Compare operations and explain associativity.

#### Mathematical Solution
- **Path 1: $(AB)C$**
  $$AB = \begin{pmatrix} 1(1)+2(2)+0 & 1(0)+2(1)+0 \\ 0+1(2)+1(-1) & 0+1(1)+1(3) \end{pmatrix} = \begin{pmatrix} 5 & 2 \\ 1 & 4 \end{pmatrix}$$
  $$(AB)C = \begin{pmatrix} 5 & 2 \\ 1 & 4 \end{pmatrix} \begin{pmatrix} 2 & 1 \\ 0 & -1 \end{pmatrix} = \begin{pmatrix} 5(2)+0 & 5(1)+2(-1) \\ 1(2)+0 & 1(1)+4(-1) \end{pmatrix} = \begin{pmatrix} 10 & 3 \\ 2 & -3 \end{pmatrix}$$
- **Path 2: $A(BC)$**
  $$BC = \begin{pmatrix} 1 & 0 \\ 2 & 1 \\ -1 & 3 \end{pmatrix} \begin{pmatrix} 2 & 1 \\ 0 & -1 \end{pmatrix} = \begin{pmatrix} 2 & 1 \\ 4 & 1 \\ -2 & -4 \end{pmatrix}$$
  $$A(BC) = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 1 \end{pmatrix} \begin{pmatrix} 2 & 1 \\ 4 & 1 \\ -2 & -4 \end{pmatrix} = \begin{pmatrix} 1(2)+2(4)+0 & 1(1)+2(1)+0 \\ 0+1(4)+1(-2) & 0+1(1)+1(-4) \end{pmatrix} = \begin{pmatrix} 10 & 3 \\ 2 & -3 \end{pmatrix}$$
- **Operation comparison:**
  - $(AB)C$: $(2\times 3 \times 2) + (2 \times 2 \times 2) = 12 + 8 = \mathbf{20}$ multiplications.
  - $A(BC)$: $(3\times 2 \times 2) + (2 \times 3 \times 2) = 12 + 12 = \mathbf{24}$ multiplications.
  - While both paths yield the identical matrix (associativity), Path 1 requires fewer operations.

#### Python Code
```python
import numpy as np

A = np.array([[1, 2, 0], [0, 1, 1]])
B = np.array([[1, 0], [2, 1], [-1, 3]])
C = np.array([[2, 1], [0, -1]])

path1 = (A @ B) @ C
path2 = A @ (B @ C)

print("(AB)C =\n", path1)
print("A(BC) =\n", path2)
assert np.array_equal(path1, path2)
print("Associativity verified.")
```

