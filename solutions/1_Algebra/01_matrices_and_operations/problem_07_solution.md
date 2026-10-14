# Solution: Exercise 7 — Identity Matrix, Zero Matrix, and Powers

## 1. Problem Statement

For
$$A = \begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix}$$
compute
$$AI, \qquad IA, \qquad A+0, \qquad A^2, \qquad A^3.$$
Explain the roles of the matrices $I$ and $0$, and describe the pattern you observe in successive powers of $A$.

---

## 2. Step-by-Step Mathematical Explanation

### Definitions
- **Identity Matrix $I_2$:** $I = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}$
- **Zero Matrix $0_{2\times 2}$:** $0 = \begin{pmatrix} 0 & 0 \\ 0 & 0 \end{pmatrix}$

---

### Step 1: Compute $AI$, $IA$, and $A + 0$
- **Product $AI$:**
  $$AI = \begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} 2(1)+1(0) & 2(0)+1(1) \\ 0(1)+2(0) & 0(0)+2(1) \end{pmatrix} = \begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix} = A$$

- **Product $IA$:**
  $$IA = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix} = \begin{pmatrix} 1(2)+0(0) & 1(1)+0(2) \\ 0(2)+1(0) & 0(1)+1(2) \end{pmatrix} = \begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix} = A$$

- **Sum $A + 0$:**
  $$A + 0 = \begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix} + \begin{pmatrix} 0 & 0 \\ 0 & 0 \end{pmatrix} = \begin{pmatrix} 2+0 & 1+0 \\ 0+0 & 2+0 \end{pmatrix} = \begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix} = A$$

**Roles of $I$ and $0$:**
- $I$ acts as the **multiplicative identity** (analogous to the number $1$ in real arithmetic): for any compatible matrix $M$, $MI = IM = M$.
- $0$ acts as the **additive identity** (analogous to the number $0$ in real arithmetic): $M + 0 = 0 + M = M$.

---

### Step 2: Compute $A^2$ and $A^3$
- **Square $A^2$:**
  $$A^2 = A \cdot A = \begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix} \begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix} = \begin{pmatrix} 2(2)+1(0) & 2(1)+1(2) \\ 0(2)+2(0) & 0(1)+2(2) \end{pmatrix} = \begin{pmatrix} 4 & 4 \\ 0 & 4 \end{pmatrix}$$

- **Cube $A^3$:**
  $$A^3 = A^2 \cdot A = \begin{pmatrix} 4 & 4 \\ 0 & 4 \end{pmatrix} \begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix} = \begin{pmatrix} 4(2)+4(0) & 4(1)+4(2) \\ 0(2)+4(0) & 0(1)+4(2) \end{pmatrix} = \begin{pmatrix} 8 & 12 \\ 0 & 8 \end{pmatrix}$$

---

### Step 3: Pattern in Successive Powers of $A$
Let us write the diagonal and off-diagonal entries in terms of powers of $2$:
- $A^1 = \begin{pmatrix} 2^1 & 1 \cdot 2^0 \\ 0 & 2^1 \end{pmatrix} = \begin{pmatrix} 2 & 1 \\ 0 & 2 \end{pmatrix}$
- $A^2 = \begin{pmatrix} 2^2 & 2 \cdot 2^1 \\ 0 & 2^2 \end{pmatrix} = \begin{pmatrix} 4 & 4 \\ 0 & 4 \end{pmatrix}$
- $A^3 = \begin{pmatrix} 2^3 & 3 \cdot 2^2 \\ 0 & 2^3 \end{pmatrix} = \begin{pmatrix} 8 & 12 \\ 0 & 8 \end{pmatrix}$

**General Formula:**
$$A^n = \begin{pmatrix} 2^n & n 2^{n-1} \\ 0 & 2^n \end{pmatrix}$$

**Algebraic Explanation (Jordan / Nilpotent Decomposition):**
Notice $A$ can be decomposed as:
$$A = 2I + N, \quad \text{where } N = \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}$$
Because $N^2 = \begin{pmatrix} 0 & 0 \\ 0 & 0 \end{pmatrix}$ and scalar multiples of the identity commute with any matrix ($2I \cdot N = N \cdot 2I$), we can apply the binomial theorem:
$$A^n = (2I + N)^n = \binom{n}{0}(2I)^n + \binom{n}{1}(2I)^{n-1}N + \sum_{k=2}^n \binom{n}{k}(2I)^{n-k}N^k$$
Since $N^k = 0$ for all $k \ge 2$, all terms from $k=2$ onwards vanish:
$$A^n = 2^n I + n 2^{n-1} N = \begin{pmatrix} 2^n & n 2^{n-1} \\ 0 & 2^n \end{pmatrix}$$

---

## 3. Python Implementation

```python
import numpy as np

def solve_exercise_7():
    A = np.array([
        [2, 1],
        [0, 2]
    ], dtype=int)

    I = np.eye(2, dtype=int)
    zero = np.zeros((2, 2), dtype=int)

    # Multiplicative and Additive Identities
    AI = A @ I
    IA = I @ A
    A_plus_0 = A + zero

    # Powers
    A2 = A @ A
    A3 = A2 @ A

    print("AI =\n", AI)
    print("IA =\n", IA)
    print("A + 0 =\n", A_plus_0)
    print("\nA^2 =\n", A2)
    print("\nA^3 =\n", A3)

    # Verification of general formula A^n
    for n in range(1, 6):
        expected = np.array([
            [2**n, n * 2**(n - 1)],
            [0,    2**n]
        ], dtype=int)
        actual = np.linalg.matrix_power(A, n)
        assert np.array_equal(actual, expected), f"Formula failed at n={n}"
        print(f"A^{n} matches formula:\n{actual}")

if __name__ == "__main__":
    solve_exercise_7()
```

---

## 4. Key Takeaways
- The identity matrix $I$ acts as neutral element for multiplication: $AI = IA = A$.
- The zero matrix $0$ acts as neutral element for addition: $A + 0 = A$.
- Nilpotent structures ($N^k = 0$) simplify matrix power calculations dramatically.

