# Solution: Exercise 13 — A Recurrence Written in Matrix Form

## 1. Problem Statement

Let
$$F = \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix}$$
Compute $F^2$, $F^3$, $F^4$, and $F^5$. Compare the numbers obtained with the sequence:
$$0, 1, 1, 2, 3, 5, 8, \dots$$
and describe the relationship you observe.

Then compute
$$F \begin{pmatrix} a \\ b \end{pmatrix}$$
and explain how this multiplication performs one recurrence step: it creates the sum of two consecutive terms and keeps one of them for the next step.

---

## 2. Step-by-Step Mathematical Explanation

### Step 1: Definition of the Fibonacci Sequence
The standard Fibonacci sequence $(f_n)_{n \ge 0}$ is defined by:
$$f_0 = 0, \quad f_1 = 1, \quad f_n = f_{n-1} + f_{n-2} \quad \text{for } n \ge 2$$
The initial values are:
$$f_0 = 0, \quad f_1 = 1, \quad f_2 = 1, \quad f_3 = 2, \quad f_4 = 3, \quad f_5 = 5, \quad f_6 = 8, \quad f_7 = 13, \dots$$

---

### Step 2: Compute Powers of $F$
- **$F^1$:**
  $$F^1 = \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix} = \begin{pmatrix} f_2 & f_1 \\ f_1 & f_0 \end{pmatrix}$$

- **$F^2 = F \cdot F$:**
  $$F^2 = \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix} = \begin{pmatrix} 1(1)+1(1) & 1(1)+1(0) \\ 1(1)+0(1) & 1(1)+0(0) \end{pmatrix} = \begin{pmatrix} 2 & 1 \\ 1 & 1 \end{pmatrix} = \begin{pmatrix} f_3 & f_2 \\ f_2 & f_1 \end{pmatrix}$$

- **$F^3 = F^2 \cdot F$:**
  $$F^3 = \begin{pmatrix} 2 & 1 \\ 1 & 1 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix} = \begin{pmatrix} 2(1)+1(1) & 2(1)+1(0) \\ 1(1)+1(1) & 1(1)+1(0) \end{pmatrix} = \begin{pmatrix} 3 & 2 \\ 2 & 1 \end{pmatrix} = \begin{pmatrix} f_4 & f_3 \\ f_3 & f_2 \end{pmatrix}$$

- **$F^4 = F^3 \cdot F$:**
  $$F^4 = \begin{pmatrix} 3 & 2 \\ 2 & 1 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix} = \begin{pmatrix} 3(1)+2(1) & 3(1)+2(0) \\ 2(1)+1(1) & 2(1)+1(0) \end{pmatrix} = \begin{pmatrix} 5 & 3 \\ 3 & 2 \end{pmatrix} = \begin{pmatrix} f_5 & f_4 \\ f_4 & f_3 \end{pmatrix}$$

- **$F^5 = F^4 \cdot F$:**
  $$F^5 = \begin{pmatrix} 5 & 3 \\ 3 & 2 \end{pmatrix} \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix} = \begin{pmatrix} 5(1)+3(1) & 5(1)+3(0) \\ 3(1)+2(1) & 3(1)+2(0) \end{pmatrix} = \begin{pmatrix} 8 & 5 \\ 5 & 3 \end{pmatrix} = \begin{pmatrix} f_6 & f_5 \\ f_5 & f_4 \end{pmatrix}$$

---

### Step 3: General Relationship
For any integer $n \ge 1$:
$$F^n = \begin{pmatrix} f_{n+1} & f_n \\ f_n & f_{n-1} \end{pmatrix}$$

Notice that taking the determinant yields Cassini's identity directly:
$$\det(F^n) = (\det F)^n = (-1)^n \implies f_{n+1} f_{n-1} - f_n^2 = (-1)^n$$

---

### Step 4: One Recurrence Step
Now compute $F \begin{pmatrix} a \\ b \end{pmatrix}$:
$$F \begin{pmatrix} a \\ b \end{pmatrix} = \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix} \begin{pmatrix} a \\ b \end{pmatrix} = \begin{pmatrix} 1\cdot a + 1\cdot b \\ 1\cdot a + 0\cdot b \end{pmatrix} = \begin{pmatrix} a + b \\ a \end{pmatrix}$$

**Explanation of the Recurrence Mechanism:**
- **Top entry:** Computes $a + b$, which is the sum of the two previous consecutive terms.
- **Bottom entry:** Copies $a$, retaining the most recent term for the subsequent step.
- If we initialize with $\begin{pmatrix} f_1 \\ f_0 \end{pmatrix} = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$, each multiplication by $F$ advances the state vector by one step:
  $$\begin{pmatrix} f_1 \\ f_0 \end{pmatrix} \xrightarrow{F} \begin{pmatrix} f_2 \\ f_1 \end{pmatrix} \xrightarrow{F} \begin{pmatrix} f_3 \\ f_2 \end{pmatrix} \xrightarrow{F} \cdots \xrightarrow{F} \begin{pmatrix} f_{n+1} \\ f_n \end{pmatrix}$$
- Therefore:
  $$\begin{pmatrix} f_{n+1} \\ f_n \end{pmatrix} = F^n \begin{pmatrix} f_1 \\ f_0 \end{pmatrix} = F^n \begin{pmatrix} 1 \\ 0 \end{pmatrix}$$

---

## 3. Python Implementation

```python
import numpy as np

def fibonacci_iterative(n):
    fib = [0, 1]
    for i in range(2, n + 2):
        fib.append(fib[-1] + fib[-2])
    return fib

def solve_exercise_13():
    F = np.array([
        [1, 1],
        [1, 0]
    ], dtype=np.int64)

    # Compute powers F^1 to F^5
    powers = {}
    current = F.copy()
    powers[1] = current.copy()
    for p in range(2, 6):
        current = current @ F
        powers[p] = current.copy()

    for p, mat in powers.items():
        print(f"F^{p} =\n{mat}\n")

    # Verify connection to Fibonacci numbers
    fib = fibonacci_iterative(10)
    for p in range(1, 6):
        expected = np.array([
            [fib[p + 1], fib[p]],
            [fib[p],     fib[p - 1]]
        ])
        assert np.array_equal(powers[p], expected), f"Mismatch at power {p}"

    print("Verified: F^n contains [[f_{n+1}, f_n], [f_n, f_{n-1}]] for all powers.")

    # Matrix-vector recurrence step demo
    state = np.array([1, 0], dtype=np.int64)  # [f_1, f_0]
    print("\nState transitions using F @ [a, b]^T:")
    for step in range(1, 8):
        state = F @ state
        print(f"Step {step}: [f_{step+1}, f_{step}] = {state}")

if __name__ == "__main__":
    solve_exercise_13()
```

---

## 4. Key Takeaways
- Any linear recurrence of order $k$ can be represented as a matrix-vector system $\mathbf{x}_{n+1} = M \mathbf{x}_n$.
- Computing $F^n$ via fast matrix exponentiation allows computing the $n$-th Fibonacci number in $O(\log n)$ operations instead of $O(n)$ additions.

