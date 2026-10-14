# Solution: Exercise 11 — When Do Matrices Commute?

## 1. Problem Statement

Given
$$A = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}, \qquad B = \begin{pmatrix} a & b \\ c & d \end{pmatrix}$$
Find the conditions on $a, b, c, d$ under which $AB = BA$. Describe the general form of all such matrices $B$.

---

## 2. Step-by-Step Mathematical Explanation

### Step 1: Compute $AB$
$$AB = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} a & b \\ c & d \end{pmatrix} = \begin{pmatrix} 1\cdot a + 1\cdot c & 1\cdot b + 1\cdot d \\ 0\cdot a + 1\cdot c & 0\cdot b + 1\cdot d \end{pmatrix} = \begin{pmatrix} a + c & b + d \\ c & d \end{pmatrix}$$

---

### Step 2: Compute $BA$
$$BA = \begin{pmatrix} a & b \\ c & d \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} a\cdot 1 + b\cdot 0 & a\cdot 1 + b\cdot 1 \\ c\cdot 1 + d\cdot 0 & c\cdot 1 + d\cdot 1 \end{pmatrix} = \begin{pmatrix} a & a + b \\ c & c + d \end{pmatrix}$$

---

### Step 3: Equate Entries of $AB$ and $BA$
For $AB = BA$, all corresponding entries must be equal:
$$\begin{pmatrix} a + c & b + d \\ c & d \end{pmatrix} = \begin{pmatrix} a & a + b \\ c & c + d \end{pmatrix}$$

This yields a system of four equations:
1. **Entry $(1, 1)$:** $a + c = a \implies c = 0$
2. **Entry $(1, 2)$:** $b + d = a + b \implies d = a$
3. **Entry $(2, 1)$:** $c = c$ (identically true for any $c$)
4. **Entry $(2, 2)$:** $d = c + d \implies c = 0$ (consistent with equation 1)

---

### Step 4: Necessary and Sufficient Conditions
The conditions for $AB = BA$ are:
$$c = 0 \quad \text{and} \quad d = a$$
where $a$ and $b$ are arbitrary real numbers ($a, b \in \mathbb{R}$).

---

### Step 5: General Form of Matrix $B$
Substituting $c = 0$ and $d = a$ into $B$:
$$B = \begin{pmatrix} a & b \\ 0 & a \end{pmatrix}, \qquad a, b \in \mathbb{R}$$

**Algebraic Insights:**
1. **Linear Combination Form:**
   $$B = a \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} + b \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix} = a I + b N$$
   where $N = A - I = \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}$.
2. **Polynomial in $A$:**
   Since $N = A - I$:
   $$B = a I + b(A - I) = (a - b)I + bA$$
   This illustrates a fundamental theorem of linear algebra: **the set of matrices that commute with a matrix $A$ having a single Jordan block (or distinct eigenvalues) consists precisely of polynomials in $A$**.

---

## 3. Python Implementation

```python
import sympy as sp

def solve_exercise_11():
    # Define symbolic variables
    a, b, c, d = sp.symbols('a b c d', real=True)

    A = sp.Matrix([
        [1, 1],
        [0, 1]
    ])

    B = sp.Matrix([
        [a, b],
        [c, d]
    ])

    # Compute products
    AB = A * B
    BA = B * A

    # Commutator [A, B] = AB - BA = 0
    comm = AB - BA

    # Solve the system of equations
    system = [comm[0, 0], comm[0, 1], comm[1, 0], comm[1, 1]]
    solution = sp.solve(system, (a, b, c, d))

    print("A * B =\n", AB)
    print("\nB * A =\n", BA)
    print("\nCommutator AB - BA =\n", comm)
    print("\nConditions for commutativity:", solution)

    # General form of B
    B_general = sp.Matrix([
        [a, b],
        [0, a]
    ])
    print("\nGeneral form of B:\n", B_general)
    print("Verification (A*B - B*A) for general form:\n", (A * B_general - B_general * A))

if __name__ == "__main__":
    solve_exercise_11()
```

---

## 4. Key Takeaways
- Matrices commute with $A = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix}$ if and only if they are upper-triangular with equal diagonal entries ($c=0$ and $d=a$).
- Any such matrix can be written as an affine combination of $I$ and $A$.

