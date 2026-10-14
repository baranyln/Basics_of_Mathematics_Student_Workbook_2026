# Solution: Exercise 12 — Formula for a Matrix Power

## 1. Problem Statement

Let
$$A = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$$
Compute $A^2$, $A^3$, and $A^4$, and use them to formulate a conjecture for $A^n$. Then do not stop after checking one more case: assume the formula is true for $n$, multiply by $A$, and explain why you obtain exactly the formula for $n+1$.

---

## 2. Step-by-Step Mathematical Explanation

### Step 1: Compute Initial Powers of $A$
- **$A^1$:**
  $$A^1 = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$$

- **$A^2 = A \cdot A$:**
  $$A^2 = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} 1\cdot 1 + 1\cdot 0 & 1\cdot 1 + 1\cdot 1 \\ 0\cdot 1 + 1\cdot 0 & 0\cdot 1 + 1\cdot 1 \end{pmatrix} = \begin{pmatrix} 1 & 2 \\ 0 & 1 \end{pmatrix}$$

- **$A^3 = A^2 \cdot A$:**
  $$A^3 = \begin{pmatrix} 1 & 2 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} 1\cdot 1 + 2\cdot 0 & 1\cdot 1 + 2\cdot 1 \\ 0\cdot 1 + 1\cdot 0 & 0\cdot 1 + 1\cdot 1 \end{pmatrix} = \begin{pmatrix} 1 & 3 \\ 0 & 1 \end{pmatrix}$$

- **$A^4 = A^3 \cdot A$:**
  $$A^4 = \begin{pmatrix} 1 & 3 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} 1\cdot 1 + 3\cdot 0 & 1\cdot 1 + 3\cdot 1 \\ 0\cdot 1 + 1\cdot 0 & 0\cdot 1 + 1\cdot 1 \end{pmatrix} = \begin{pmatrix} 1 & 4 \\ 0 & 1 \end{pmatrix}$$

---

### Step 2: Formulation of the Conjecture
Looking at the sequence:
$$A^1 = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}, \quad A^2 = \begin{pmatrix} 1 & 2 \\ 0 & 1 \end{pmatrix}, \quad A^3 = \begin{pmatrix} 1 & 3 \\ 0 & 1 \end{pmatrix}, \quad A^4 = \begin{pmatrix} 1 & 4 \\ 0 & 1 \end{pmatrix}$$

We formulate the conjecture:
$$A^n = \begin{pmatrix} 1 & n \\ 0 & 1 \end{pmatrix} \quad \text{for all } n \in \mathbb{N} = \{1, 2, 3, \dots\}$$

---

### Step 3: Proof by Mathematical Induction

#### Base Step ($n = 1$):
For $n = 1$:
$$A^1 = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$$
This matches the initial matrix $A$. The base step is verified.

#### Inductive Hypothesis:
Assume the formula holds for an arbitrary positive integer $n = k$:
$$A^k = \begin{pmatrix} 1 & k \\ 0 & 1 \end{pmatrix}$$

#### Inductive Step ($n = k + 1$):
We compute $A^{k+1}$ using the definition of power $A^{k+1} = A^k \cdot A$:
$$A^{k+1} = A^k \cdot A = \begin{pmatrix} 1 & k \\ 0 & 1 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$$

Performing the matrix multiplication:
$$\text{Entry } (1, 1): \quad 1 \cdot 1 + k \cdot 0 = 1$$
$$\text{Entry } (1, 2): \quad 1 \cdot 1 + k \cdot 1 = 1 + k = k + 1$$
$$\text{Entry } (2, 1): \quad 0 \cdot 1 + 1 \cdot 0 = 0$$
$$\text{Entry } (2, 2): \quad 0 \cdot 1 + 1 \cdot 1 = 1$$

Combining these entries:
$$A^{k+1} = \begin{pmatrix} 1 & k+1 \\ 0 & 1 \end{pmatrix}$$

This is precisely the expression predicted by the formula for $n = k + 1$.

**Conclusion:**
By the principle of mathematical induction, the formula holds for all integers $n \ge 1$:
$$A^n = \begin{pmatrix} 1 & n \\ 0 & 1 \end{pmatrix}$$
*(Note: It also holds for $n = 0$ giving $A^0 = I$, and for negative integers $n < 0$ giving $A^{-m} = (A^{-1})^m = \begin{pmatrix} 1 & -m \\ 0 & 1 \end{pmatrix}$).*

---

## 3. Python Implementation

```python
import numpy as np

def solve_exercise_12():
    A = np.array([
        [1, 1],
        [0, 1]
    ], dtype=int)

    # Compute first 4 powers
    A1 = A
    A2 = A1 @ A
    A3 = A2 @ A
    A4 = A3 @ A

    print("A^1 =\n", A1)
    print("\nA^2 =\n", A2)
    print("\nA^3 =\n", A3)
    print("\nA^4 =\n", A4)

    # Induction verification for a large range of powers
    for n in range(1, 101):
        actual = np.linalg.matrix_power(A, n)
        expected = np.array([
            [1, n],
            [0, 1]
        ], dtype=int)
        assert np.array_equal(actual, expected), f"Failed for n = {n}"

    print("\nVerified A^n = [[1, n], [0, 1]] for all n from 1 to 100 via induction & computation.")

if __name__ == "__main__":
    solve_exercise_12()
```

---

## 4. Key Takeaways
- The matrix $A = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$ represents a **horizontal shear**.
- Applying a shear $n$ times increases the displacement proportionally to $n$, explaining the entry $n$ in position $(1, 2)$ geometrically and algebraically.

