# Solution: Exercise 15 — Associativity of Multiplication and Different Calculation Paths

## 1. Problem Statement

Given
$$A = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 1 \end{pmatrix}, \qquad B = \begin{pmatrix} 1 & 0 \\ 2 & 1 \\ -1 & 3 \end{pmatrix}, \qquad C = \begin{pmatrix} 2 & 1 \\ 0 & -1 \end{pmatrix}$$

Compute $(AB)C$ and $A(BC)$. Compare the results and the number of intermediate operations. Explain what associativity of matrix multiplication means in this example.

---

## 2. Step-by-Step Mathematical Explanation

### Matrix Dimensions
- $A$ is $2 \times 3$
- $B$ is $3 \times 2$
- $C$ is $2 \times 2$

---

### Path 1: Compute $(AB)C$

#### Step 1A: Compute $AB$
$A$ is $2 \times 3$ and $B$ is $3 \times 2$, so $AB$ is $2 \times 2$:
$$AB = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 1 \end{pmatrix} \begin{pmatrix} 1 & 0 \\ 2 & 1 \\ -1 & 3 \end{pmatrix}$$

Entries of $AB$:
- $(AB)_{11} = 1(1) + 2(2) + 0(-1) = 1 + 4 + 0 = 5$
- $(AB)_{12} = 1(0) + 2(1) + 0(3) = 0 + 2 + 0 = 2$
- $(AB)_{21} = 0(1) + 1(2) + 1(-1) = 0 + 2 - 1 = 1$
- $(AB)_{22} = 0(0) + 1(1) + 1(3) = 0 + 1 + 3 = 4$

$$AB = \begin{pmatrix} 5 & 2 \\ 1 & 4 \end{pmatrix}$$

#### Step 1B: Compute $(AB)C$
$(AB)$ is $2 \times 2$ and $C$ is $2 \times 2$, so $(AB)C$ is $2 \times 2$:
$$(AB)C = \begin{pmatrix} 5 & 2 \\ 1 & 4 \end{pmatrix} \begin{pmatrix} 2 & 1 \\ 0 & -1 \end{pmatrix}$$

Entries of $(AB)C$:
- Entry $(1, 1) = 5(2) + 2(0) = 10 + 0 = 10$
- Entry $(1, 2) = 5(1) + 2(-1) = 5 - 2 = 3$
- Entry $(2, 1) = 1(2) + 4(0) = 2 + 0 = 2$
- Entry $(2, 2) = 1(1) + 4(-1) = 1 - 4 = -3$

$$(AB)C = \begin{pmatrix} 10 & 3 \\ 2 & -3 \end{pmatrix}$$

---

### Path 2: Compute $A(BC)$

#### Step 2A: Compute $BC$
$B$ is $3 \times 2$ and $C$ is $2 \times 2$, so $BC$ is $3 \times 2$:
$$BC = \begin{pmatrix} 1 & 0 \\ 2 & 1 \\ -1 & 3 \end{pmatrix} \begin{pmatrix} 2 & 1 \\ 0 & -1 \end{pmatrix}$$

Entries of $BC$:
- Row 1:
  - $(BC)_{11} = 1(2) + 0(0) = 2$
  - $(BC)_{12} = 1(1) + 0(-1) = 1$
- Row 2:
  - $(BC)_{21} = 2(2) + 1(0) = 4 + 0 = 4$
  - $(BC)_{22} = 2(1) + 1(-1) = 2 - 1 = 1$
- Row 3:
  - $(BC)_{31} = -1(2) + 3(0) = -2 + 0 = -2$
  - $(BC)_{32} = -1(1) + 3(-1) = -1 - 3 = -4$

$$BC = \begin{pmatrix} 2 & 1 \\ 4 & 1 \\ -2 & -4 \end{pmatrix}$$

#### Step 2B: Compute $A(BC)$
$A$ is $2 \times 3$ and $BC$ is $3 \times 2$, so $A(BC)$ is $2 \times 2$:
$$A(BC) = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & 1 \end{pmatrix} \begin{pmatrix} 2 & 1 \\ 4 & 1 \\ -2 & -4 \end{pmatrix}$$

Entries of $A(BC)$:
- $(A(BC))_{11} = 1(2) + 2(4) + 0(-2) = 2 + 8 + 0 = 10$
- $(A(BC))_{12} = 1(1) + 2(1) + 0(-4) = 1 + 2 + 0 = 3$
- $(A(BC))_{21} = 0(2) + 1(4) + 1(-2) = 0 + 4 - 2 = 2$
- $(A(BC))_{22} = 0(1) + 1(1) + 1(-4) = 0 + 1 - 4 = -3$

$$A(BC) = \begin{pmatrix} 10 & 3 \\ 2 & -3 \end{pmatrix}$$

---

### Step 3: Comparison and Operation Counts

1. **Equivalence:**
   $$(AB)C = A(BC) = \begin{pmatrix} 10 & 3 \\ 2 & -3 \end{pmatrix}$$
   This confirms that matrix multiplication is **associative**.

2. **Arithmetic Operation Count (FLOPs):**
   Multiplying a $p \times q$ matrix by a $q \times r$ matrix requires:
   - $p \cdot q \cdot r$ scalar multiplications
   - $p \cdot (q - 1) \cdot r$ scalar additions

   - **For Path 1: $(AB)C$**
     - Step 1: $AB$ has dimensions $(2 \times 3) \cdot (3 \times 2)$:
       - Multiplications: $2 \times 3 \times 2 = 12$
       - Additions: $2 \times 2 \times 2 = 8$
     - Step 2: $(AB)C$ has dimensions $(2 \times 2) \cdot (2 \times 2)$:
       - Multiplications: $2 \times 2 \times 2 = 8$
       - Additions: $2 \times 1 \times 2 = 4$
     - **Total for $(AB)C$:** $12 + 8 = \mathbf{20}$ multiplications, $8 + 4 = \mathbf{12}$ additions ($\mathbf{32}$ FLOPs total).

   - **For Path 2: $A(BC)$**
     - Step 1: $BC$ has dimensions $(3 \times 2) \cdot (2 \times 2)$:
       - Multiplications: $3 \times 2 \times 2 = 12$
       - Additions: $3 \times 1 \times 2 = 6$
     - Step 2: $A(BC)$ has dimensions $(2 \times 3) \cdot (3 \times 2)$:
       - Multiplications: $2 \times 3 \times 2 = 12$
       - Additions: $2 \times 2 \times 2 = 8$
     - **Total for $A(BC)$:** $12 + 12 = \mathbf{24}$ multiplications, $6 + 8 = \mathbf{14}$ additions ($\mathbf{38}$ FLOPs total).

**Meaning of Associativity:**
- Algebraically, the grouping of parentheses does not change the final resulting linear transformation: $(AB)C = A(BC) = ABC$.
- Computationally, however, the choice of parenthesization changes the sizes of intermediate matrices and the overall computational cost ($32$ FLOPs vs $38$ FLOPs). This property is the motivation for the famous **Matrix Chain Multiplication** dynamic programming algorithm in computer science.

---

## 3. Python Implementation

```python
import numpy as np

def solve_exercise_15():
    A = np.array([
        [1, 2, 0],
        [0, 1, 1]
    ], dtype=int)

    B = np.array([
        [ 1, 0],
        [ 2, 1],
        [-1, 3]
    ], dtype=int)

    C = np.array([
        [2,  1],
        [0, -1]
    ], dtype=int)

    # Path 1: (AB)C
    AB = A @ B
    path1 = AB @ C

    # Path 2: A(BC)
    BC = B @ C
    path2 = A @ BC

    print("Matrix AB =\n", AB)
    print("\nMatrix BC =\n", BC)
    print("\nPath 1 (AB)C =\n", path1)
    print("\nPath 2 A(BC) =\n", path2)

    # Verify mathematical equality
    assert np.array_equal(path1, path2), "Associativity failed!"
    print("\nVerified: (AB)C == A(BC).")

    # Flop count analysis
    def flops(p, q, r):
        mults = p * q * r
        adds = p * (q - 1) * r
        return mults, adds

    m1_ab, a1_ab = flops(2, 3, 2)
    m1_c,  a1_c  = flops(2, 2, 2)
    tot1 = (m1_ab + m1_c, a1_ab + a1_c)

    m2_bc, a2_bc = flops(3, 2, 2)
    m2_a,  a2_a  = flops(2, 3, 2)
    tot2 = (m2_bc + m2_a, a2_bc + a2_a)

    print(f"\nComplexity Path 1 (AB)C: {tot1[0]} mults + {tot1[1]} adds = {sum(tot1)} FLOPs")
    print(f"Complexity Path 2 A(BC): {tot2[0]} mults + {tot2[1]} adds = {sum(tot2)} FLOPs")
    print(f"Path 1 is more efficient by {sum(tot2) - sum(tot1)} operations.")

if __name__ == "__main__":
    solve_exercise_15()
```

---

## 4. Key Takeaways
- Matrix multiplication is strictly associative: $(AB)C = A(BC)$.
- Parenthesization matters for execution time and memory footprint in numerical computing.

