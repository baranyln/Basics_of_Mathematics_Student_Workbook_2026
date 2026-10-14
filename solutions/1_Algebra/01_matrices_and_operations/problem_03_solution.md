# Solution: Exercise 3 — When Can Matrices Be Multiplied?

## 1. Problem Statement

The matrix sizes are:
$$A_{2\times3}, \qquad B_{3\times4}, \qquad C_{4\times2}, \qquad D_{2\times2}$$

For the products:
$$AB, \quad BA, \quad BC, \quad CB, \quad AC, \quad CA, \quad AD, \quad DA$$
determine whether they are defined. If so, state the size of the result. Justify each decision using the dimension compatibility condition.

---

## 2. Step-by-Step Mathematical Explanation

### The Compatibility Condition for Matrix Multiplication
Matrix multiplication $M \cdot N$ is defined if and only if the **number of columns in the first matrix equals the number of rows in the second matrix**:
$$\text{If } M \text{ is } p \times q \text{ and } N \text{ is } r \times s, \text{ the product } MN \text{ is defined } \iff q = r.$$
When $q = r$, the resulting matrix has size **$p \times s$** (the outer dimensions):
$$(p \times \underbrace{q) \cdot (r}_{\text{must match}} \times s) \longrightarrow (p \times s)$$

---

### Step-by-Step Evaluation of Each Product

| Product | Matrix Dimensions | Inner Dimensions Check | Defined? | Resulting Size | Justification |
| :---: | :---: | :---: | :---: | :---: | :--- |
| **$AB$** | $(2\times 3) \cdot (3\times 4)$ | $3 = 3$ | **Yes** | $2 \times 4$ | Inner dimensions match ($3=3$). Outer dimensions determine size: $2 \times 4$. |
| **$BA$** | $(3\times 4) \cdot (2\times 3)$ | $4 \neq 2$ | **No** | *Undefined* | Inner dimensions do not match ($4 \neq 2$). |
| **$BC$** | $(3\times 4) \cdot (4\times 2)$ | $4 = 4$ | **Yes** | $3 \times 2$ | Inner dimensions match ($4=4$). Outer dimensions determine size: $3 \times 2$. |
| **$CB$** | $(4\times 2) \cdot (3\times 4)$ | $2 \neq 3$ | **No** | *Undefined* | Inner dimensions do not match ($2 \neq 3$). |
| **$AC$** | $(2\times 3) \cdot (4\times 2)$ | $3 \neq 4$ | **No** | *Undefined* | Inner dimensions do not match ($3 \neq 4$). |
| **$CA$** | $(4\times 2) \cdot (2\times 3)$ | $2 = 2$ | **Yes** | $4 \times 3$ | Inner dimensions match ($2=2$). Outer dimensions determine size: $4 \times 3$. |
| **$AD$** | $(2\times 3) \cdot (2\times 2)$ | $3 \neq 2$ | **No** | *Undefined* | Inner dimensions do not match ($3 \neq 2$). |
| **$DA$** | $(2\times 2) \cdot (2\times 3)$ | $2 = 2$ | **Yes** | $2 \times 3$ | Inner dimensions match ($2=2$). Outer dimensions determine size: $2 \times 3$. |

---

## 3. Python Implementation

```python
def check_matrix_multiplication(sizes, products):
    """
    Evaluates whether matrix products are defined based on their dimensions.
    """
    results = {}
    for prod in products:
        m1_name, m2_name = prod[0], prod[1]
        r1, c1 = sizes[m1_name]
        r2, c2 = sizes[m2_name]
        
        if c1 == r2:
            results[prod] = (True, (r1, c2), f"Defined: ({r1}x{c1}) * ({r2}x{c2}) -> {r1}x{c2}")
        else:
            results[prod] = (False, None, f"Undefined: inner dimensions mismatch ({c1} != {r2})")
            
    return results

def solve_exercise_3():
    matrix_sizes = {
        'A': (2, 3),
        'B': (3, 4),
        'C': (4, 2),
        'D': (2, 2)
    }
    
    product_list = ['AB', 'BA', 'BC', 'CB', 'AC', 'CA', 'AD', 'DA']
    evaluation = check_matrix_multiplication(matrix_sizes, product_list)
    
    for prod, (is_def, size, expl) in evaluation.items():
        status = f"Defined -> Size {size[0]}x{size[1]}" if is_def else "UNDEFINED"
        print(f"Product {prod}: {status} ({expl})")

if __name__ == "__main__":
    solve_exercise_3()
```

---

## 4. Key Takeaways
- Even if $MN$ is defined, $NM$ is not necessarily defined (e.g., $AB$ is $2\times 4$, but $BA$ is undefined).
- Even if both $MN$ and $NM$ are defined, they generally do not have the same size unless both matrices are square ($n \times n$).

