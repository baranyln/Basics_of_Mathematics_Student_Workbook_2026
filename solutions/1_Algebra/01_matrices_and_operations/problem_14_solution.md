# Solution: Exercise 14 — Rotation Matrices

## 1. Problem Statement

The matrix for a rotation through an angle $\theta$ is
$$R(\theta) = \begin{pmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{pmatrix}$$

Compute $R(\alpha)R(\beta)$ and, using the angle-sum formulas for sine and cosine, show that
$$R(\alpha)R(\beta) = R(\alpha + \beta).$$
Explain the result geometrically.

---

## 2. Step-by-Step Mathematical Explanation

### Recall Trigonometric Addition Formulas
1. $\cos(\alpha + \beta) = \cos\alpha\cos\beta - \sin\alpha\sin\beta$
2. $\sin(\alpha + \beta) = \sin\alpha\cos\beta + \cos\alpha\sin\beta$

---

### Step 1: Matrix Multiplication $R(\alpha)R(\beta)$
Set up the product:
$$R(\alpha)R(\beta) = \begin{pmatrix} \cos\alpha & -\sin\alpha \\ \sin\alpha & \cos\alpha \end{pmatrix} \begin{pmatrix} \cos\beta & -\sin\beta \\ \sin\beta & \cos\beta \end{pmatrix}$$

Calculate each entry individually:

1. **Entry $(1, 1)$:**
   $$\text{Row}_1(R(\alpha)) \cdot \text{Col}_1(R(\beta)) = \cos\alpha\cos\beta + (-\sin\alpha)\sin\beta = \cos\alpha\cos\beta - \sin\alpha\sin\beta$$
   Using the cosine sum formula:
   $$\text{Entry }(1, 1) = \cos(\alpha + \beta)$$

2. **Entry $(1, 2)$:**
   $$\text{Row}_1(R(\alpha)) \cdot \text{Col}_2(R(\beta)) = \cos\alpha(-\sin\beta) + (-\sin\alpha)\cos\beta = -(\sin\alpha\cos\beta + \cos\alpha\sin\beta)$$
   Using the sine sum formula:
   $$\text{Entry }(1, 2) = -\sin(\alpha + \beta)$$

3. **Entry $(2, 1)$:**
   $$\text{Row}_2(R(\alpha)) \cdot \text{Col}_1(R(\beta)) = \sin\alpha\cos\beta + \cos\alpha\sin\beta$$
   Using the sine sum formula:
   $$\text{Entry }(2, 1) = \sin(\alpha + \beta)$$

4. **Entry $(2, 2)$:**
   $$\text{Row}_2(R(\alpha)) \cdot \text{Col}_2(R(\beta)) = \sin\alpha(-\sin\beta) + \cos\alpha\cos\beta = \cos\alpha\cos\beta - \sin\alpha\sin\beta$$
   Using the cosine sum formula:
   $$\text{Entry }(2, 2) = \cos(\alpha + \beta)$$

---

### Step 2: Synthesis of the Product Matrix
Assembling the entries:
$$R(\alpha)R(\beta) = \begin{pmatrix} \cos(\alpha + \beta) & -\sin(\alpha + \beta) \\ \sin(\alpha + \beta) & \cos(\alpha + \beta) \end{pmatrix} = R(\alpha + \beta)$$

This establishes the identity rigorously.

---

### Step 3: Geometric Explanation

1. **Sequential Action:**
   - In the product $(R(\alpha)R(\beta))x = R(\alpha)(R(\beta)x)$, the matrix $R(\beta)$ acts first on vector $x$, rotating it counterclockwise around the origin by an angle $\beta$.
   - The matrix $R(\alpha)$ acts next on the resulting rotated vector, rotating it further counterclockwise by an angle $\alpha$.
2. **Total Angular Displacement:**
   - Because both rotations occur in the same plane ($\mathbb{R}^2$) and about the exact same origin, the angular displacements add together directly:
     $$\Delta\theta = \beta + \alpha = \alpha + \beta$$
   - Thus, the composite operation is precisely a single counterclockwise rotation by total angle $\alpha + \beta$.
3. **Commutativity of 2D Rotations:**
   - Since scalar addition is commutative ($\alpha + \beta = \beta + \alpha$), we have:
     $$R(\alpha)R(\beta) = R(\alpha + \beta) = R(\beta + \alpha) = R(\beta)R(\alpha)$$
   - Therefore, while matrix multiplication is generally noncommutative, 2D rotations form an **abelian (commutative) subgroup** of $GL(2, \mathbb{R})$, isomorphic to the circle group $\mathrm{SO}(2) \cong U(1)$.

---

## 3. Python Implementation

```python
import sympy as sp
import numpy as np

def solve_exercise_14_symbolic():
    # Symbolic proof using SymPy
    alpha, beta = sp.symbols('alpha beta', real=True)

    def rot(theta):
        return sp.Matrix([
            [sp.cos(theta), -sp.sin(theta)],
            [sp.sin(theta),  sp.cos(theta)]
        ])

    R_alpha = rot(alpha)
    R_beta = rot(beta)
    R_combined = sp.trigsimp(R_alpha * R_beta)
    R_expected = rot(alpha + beta)

    print("R(alpha) * R(beta) simplified:\n", R_combined)
    print("\nR(alpha + beta):\n", R_expected)
    print("\nSymbolic identity holds:", sp.simplify(R_combined - R_expected) == sp.zeros(2, 2))

def solve_exercise_14_numeric():
    # Numerical demonstration with angles 30 deg and 45 deg
    def rot_num(deg):
        rad = np.radians(deg)
        return np.array([
            [np.cos(rad), -np.sin(rad)],
            [np.sin(rad),  np.cos(rad)]
        ])

    a_deg, b_deg = 30.0, 45.0
    R_a = rot_num(a_deg)
    R_b = rot_num(b_deg)
    R_prod = R_a @ R_b
    R_sum = rot_num(a_deg + b_deg)

    print("\nNumerical comparison (alpha=30 deg, beta=45 deg):")
    print("R(30) @ R(45) =\n", R_prod)
    print("R(75) =\n", R_sum)
    assert np.allclose(R_prod, R_sum), "Numerical verification failed!"
    print("Numerical verification successful.")

if __name__ == "__main__":
    solve_exercise_14_symbolic()
    solve_exercise_14_numeric()
```

---

## 4. Key Takeaways
- The algebra of rotation matrices directly encodes trigonometry. In fact, Euler's formula $e^{i\alpha}e^{i\beta} = e^{i(\alpha+\beta)}$ is the complex number equivalent of this matrix relation.
- All rotation matrices in $\mathbb{R}^2$ commute with each other.

