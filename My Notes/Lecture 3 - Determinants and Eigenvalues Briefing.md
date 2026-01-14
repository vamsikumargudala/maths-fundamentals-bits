# Lecture 0c: Determinants, Inverses, and Eigenvalues
## Comprehensive Briefing Document

---

# EXECUTIVE SUMMARY

## Critical Takeaways

1. **Determinant** measures if a matrix is invertible: $\det(A) = 0$ means singular (no inverse)
2. **Matrix Inverse** exists only for square matrices with non-zero determinant
3. **Eigenvalues** solve $\det(A - \lambda I) = 0$; they reveal fundamental matrix behavior
4. **Eigenvectors** are special directions that only get scaled (not rotated) by the matrix

## Topics Covered
- Determinant computation (2×2, 3×3, general)
- Properties of determinants
- Matrix inverse and invertibility
- Eigenvalues and eigenvectors
- Characteristic polynomial

## AI/ML Applications
| Topic | AI/ML Use Case |
|-------|----------------|
| Determinant | Check if covariance matrix is valid |
| Inverse | Solve normal equations in linear regression |
| Eigenvalues | PCA, spectral clustering, stability analysis |
| Eigenvectors | Principal components, feature directions |

---

# PART 1: DETERMINANTS

## 1.1 What is a Determinant?

### Definition
> The **determinant** is a scalar value that can be computed from a **square matrix**. It provides information about the matrix's properties, especially whether it's invertible.

### Notation
$$\det(A) \quad \text{or} \quad |A|$$

### Key Fact
> A matrix is **invertible (non-singular)** if and only if $\det(A) \neq 0$.

---

## 1.2 Determinant of 2×2 Matrix

### Formula
For a $2 \times 2$ matrix:
$$
A = \begin{bmatrix} a & b \\ c & d \end{bmatrix}
$$

$$
\det(A) = ad - bc
$$

### Memory Aid
> Main diagonal minus anti-diagonal: ↘ minus ↗

### Examples

**Example 1:**
$$
A = \begin{bmatrix} 3 & 2 \\ 1 & 4 \end{bmatrix}
$$
$$\det(A) = (3)(4) - (2)(1) = 12 - 2 = 10$$

**Example 2:**
$$
B = \begin{bmatrix} 2 & 4 \\ 1 & 2 \end{bmatrix}
$$
$$\det(B) = (2)(2) - (4)(1) = 4 - 4 = 0$$

Matrix $B$ is singular (no inverse exists).

---

## 1.3 Determinant of 3×3 Matrix

### Cofactor Expansion Method

For a $3 \times 3$ matrix:
$$
A = \begin{bmatrix} a & b & c \\ d & e & f \\ g & h & i \end{bmatrix}
$$

**Expand along the first row:**
$$
\det(A) = a \cdot \det\begin{bmatrix} e & f \\ h & i \end{bmatrix} - b \cdot \det\begin{bmatrix} d & f \\ g & i \end{bmatrix} + c \cdot \det\begin{bmatrix} d & e \\ g & h \end{bmatrix}
$$

$$
\det(A) = a(ei - fh) - b(di - fg) + c(dh - eg)
$$

### Sign Pattern
The signs alternate in a checkerboard pattern:
$$
\begin{bmatrix} + & - & + \\ - & + & - \\ + & - & + \end{bmatrix}
$$

### Detailed Example

$$
A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{bmatrix}
$$

**Expand along row 1:**

$\det(A) = 1 \cdot \det\begin{bmatrix} 5 & 6 \\ 8 & 9 \end{bmatrix} - 2 \cdot \det\begin{bmatrix} 4 & 6 \\ 7 & 9 \end{bmatrix} + 3 \cdot \det\begin{bmatrix} 4 & 5 \\ 7 & 8 \end{bmatrix}$

$= 1(5 \cdot 9 - 6 \cdot 8) - 2(4 \cdot 9 - 6 \cdot 7) + 3(4 \cdot 8 - 5 \cdot 7)$

$= 1(45 - 48) - 2(36 - 42) + 3(32 - 35)$

$= 1(-3) - 2(-6) + 3(-3)$

$= -3 + 12 - 9$

$= 0$

**Conclusion:** $\det(A) = 0$, so this matrix is singular.

---

## 1.4 Sarrus' Rule (3×3 only)

An alternative method for 3×3 determinants:

### Method
1. Write the matrix
2. Copy the first two columns to the right
3. Add products of diagonals going ↘
4. Subtract products of diagonals going ↗

### Visual
$$
\begin{array}{|ccc|cc}
a & b & c & a & b \\
d & e & f & d & e \\
g & h & i & g & h
\end{array}
$$

$$\det(A) = (aei + bfg + cdh) - (ceg + afh + bdi)$$

---

## 1.5 Properties of Determinants

### Fundamental Properties

| Property | Statement | Example |
|----------|-----------|---------|
| **Identity** | $\det(I) = 1$ | $\det\begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} = 1$ |
| **Transpose** | $\det(A^\top) = \det(A)$ | Transpose doesn't change determinant |
| **Product** | $\det(AB) = \det(A) \cdot \det(B)$ | Determinant of product = product of determinants |
| **Inverse** | $\det(A^{-1}) = \frac{1}{\det(A)}$ | If inverse exists |
| **Scalar** | $\det(cA) = c^n \det(A)$ | For $n \times n$ matrix |
| **Power** | $\det(A^k) = (\det(A))^k$ | Determinant raised to power |

### Row Operation Effects

| Row Operation | Effect on Determinant |
|---------------|----------------------|
| Swap two rows | **Multiplies by $-1$** |
| Multiply row by $c$ | **Multiplies by $c$** |
| Add multiple of one row to another | **No change** |

### Special Cases

| Matrix Type | Determinant Formula |
|-------------|-------------------|
| **Triangular** (upper or lower) | Product of diagonal entries |
| **Diagonal** | Product of diagonal entries |
| **Zero row/column** | $\det = 0$ |
| **Two identical rows/columns** | $\det = 0$ |
| **Proportional rows/columns** | $\det = 0$ |

---

## 1.6 Computing Determinant via Row Reduction

### Method
1. Reduce matrix to triangular form using row operations
2. Track sign changes from swaps
3. Track multipliers from row scaling
4. Determinant = (product of diagonal) × (adjustment factor)

### Example

$$
A = \begin{bmatrix} 2 & 4 \\ 3 & 5 \end{bmatrix}
$$

**Direct:** $\det(A) = 2(5) - 4(3) = 10 - 12 = -2$

**Via row ops:**
$R_2 \rightarrow R_2 - \frac{3}{2}R_1$:
$$\begin{bmatrix} 2 & 4 \\ 0 & -1 \end{bmatrix}$$

Diagonal product: $2 \times (-1) = -2$ ✓

---

# PART 2: MATRIX INVERSE

## 2.1 Definition of Inverse

### Definition
> For a square matrix $A$, the **inverse** $A^{-1}$ (if it exists) satisfies:
> $$AA^{-1} = A^{-1}A = I$$

### When Does Inverse Exist?
> A matrix $A$ is **invertible** (or **non-singular**) if and only if:
> $$\det(A) \neq 0$$

If $\det(A) = 0$, the matrix is **singular** and has no inverse.

---

## 2.2 Inverse of 2×2 Matrix

### Formula
For:
$$
A = \begin{bmatrix} a & b \\ c & d \end{bmatrix}
$$

The inverse is:
$$
A^{-1} = \frac{1}{\det(A)} \begin{bmatrix} d & -b \\ -c & a \end{bmatrix} = \frac{1}{ad-bc} \begin{bmatrix} d & -b \\ -c & a \end{bmatrix}
$$

### Memory Aid
1. Swap diagonal elements ($a \leftrightarrow d$)
2. Negate off-diagonal elements ($b \rightarrow -b$, $c \rightarrow -c$)
3. Divide by determinant

### Example
$$
A = \begin{bmatrix} 4 & 7 \\ 2 & 6 \end{bmatrix}
$$

**Step 1:** $\det(A) = 4(6) - 7(2) = 24 - 14 = 10$

**Step 2:** Swap and negate:
$$\begin{bmatrix} 6 & -7 \\ -2 & 4 \end{bmatrix}$$

**Step 3:** Divide by determinant:
$$
A^{-1} = \frac{1}{10} \begin{bmatrix} 6 & -7 \\ -2 & 4 \end{bmatrix} = \begin{bmatrix} 0.6 & -0.7 \\ -0.2 & 0.4 \end{bmatrix}
$$

**Verify:** $AA^{-1} = I$ ✓

---

## 2.3 Inverse via Gauss-Jordan Method

### Method for Any Square Matrix
1. Create augmented matrix $[A | I]$
2. Apply row operations to transform $A$ into $I$
3. The right side becomes $A^{-1}$: $[I | A^{-1}]$

### Example
Find inverse of:
$$
A = \begin{bmatrix} 1 & 2 \\ 3 & 7 \end{bmatrix}
$$

**Step 1:** Set up $[A | I]$:
$$
\left[\begin{array}{cc|cc} 1 & 2 & 1 & 0 \\ 3 & 7 & 0 & 1 \end{array}\right]
$$

**Step 2:** $R_2 \rightarrow R_2 - 3R_1$:
$$
\left[\begin{array}{cc|cc} 1 & 2 & 1 & 0 \\ 0 & 1 & -3 & 1 \end{array}\right]
$$

**Step 3:** $R_1 \rightarrow R_1 - 2R_2$:
$$
\left[\begin{array}{cc|cc} 1 & 0 & 7 & -2 \\ 0 & 1 & -3 & 1 \end{array}\right]
$$

**Result:**
$$
A^{-1} = \begin{bmatrix} 7 & -2 \\ -3 & 1 \end{bmatrix}
$$

---

## 2.4 Properties of Inverse

| Property | Formula |
|----------|---------|
| **Uniqueness** | If inverse exists, it's unique |
| **Double inverse** | $(A^{-1})^{-1} = A$ |
| **Product** | $(AB)^{-1} = B^{-1}A^{-1}$ ⚠️ **Order reverses!** |
| **Transpose** | $(A^\top)^{-1} = (A^{-1})^\top$ |
| **Scalar** | $(cA)^{-1} = \frac{1}{c}A^{-1}$ |
| **Power** | $(A^n)^{-1} = (A^{-1})^n$ |

### The Reversal Rule (Important!)
$$
(AB)^{-1} = B^{-1}A^{-1}
$$

Just like transpose: the order reverses!

---

## 2.5 Solving Systems with Inverse

If $A$ is invertible, the system $Ax = b$ has unique solution:
$$x = A^{-1}b$$

### Example
Solve:
$$
\begin{bmatrix} 4 & 7 \\ 2 & 6 \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix} = \begin{bmatrix} 5 \\ 3 \end{bmatrix}
$$

Using $A^{-1}$ from earlier:
$$
\begin{bmatrix} x \\ y \end{bmatrix} = \begin{bmatrix} 0.6 & -0.7 \\ -0.2 & 0.4 \end{bmatrix} \begin{bmatrix} 5 \\ 3 \end{bmatrix} = \begin{bmatrix} 0.9 \\ 0.2 \end{bmatrix}
$$

---

## 2.6 When Inverse Doesn't Exist

**Checklist for Non-Invertible (Singular) Matrix:**
- $\det(A) = 0$
- Matrix has a zero row or column
- Two rows/columns are identical
- Two rows/columns are proportional
- Rank is less than the size of the matrix
- Rows reduce to a zero row

---

# PART 3: EIGENVALUES AND EIGENVECTORS

## 3.1 Motivation: Why Eigenvalues?

### The Key Question
> When we multiply a matrix $A$ by a vector $x$, the result $Ax$ is usually a completely different vector (different direction and length).
>
> But sometimes, $Ax$ points in the **same direction** as $x$, just scaled!

### Definition
> An **eigenvector** $v$ of matrix $A$ is a non-zero vector where:
> $$Av = \lambda v$$
>
> The scalar $\lambda$ is called the **eigenvalue**.

### Intuition
- Eigenvector: A "special direction" that the matrix only stretches/compresses
- Eigenvalue: The stretch/compression factor

---

## 3.2 Finding Eigenvalues

### The Characteristic Equation

Starting from $Av = \lambda v$:
$$Av - \lambda v = 0$$
$$Av - \lambda I v = 0$$
$$(A - \lambda I)v = 0$$

For non-zero $v$ to exist, we need:
$$\det(A - \lambda I) = 0$$

This is called the **characteristic equation**.

### The Characteristic Polynomial
$\det(A - \lambda I)$ is a polynomial in $\lambda$ of degree $n$ (for $n \times n$ matrix).

The eigenvalues are the **roots** of this polynomial.

---

## 3.3 Example: Finding Eigenvalues of 2×2 Matrix

Find eigenvalues of:
$$
A = \begin{bmatrix} 4 & 1 \\ 2 & 3 \end{bmatrix}
$$

**Step 1:** Form $A - \lambda I$:
$$
A - \lambda I = \begin{bmatrix} 4 - \lambda & 1 \\ 2 & 3 - \lambda \end{bmatrix}
$$

**Step 2:** Compute determinant:
$$\det(A - \lambda I) = (4-\lambda)(3-\lambda) - (1)(2)$$
$$= 12 - 4\lambda - 3\lambda + \lambda^2 - 2$$
$$= \lambda^2 - 7\lambda + 10$$

**Step 3:** Solve $\lambda^2 - 7\lambda + 10 = 0$:
$$(\lambda - 5)(\lambda - 2) = 0$$

**Eigenvalues:** $\lambda_1 = 5$ and $\lambda_2 = 2$

---

## 3.4 Finding Eigenvectors

Once you have eigenvalue $\lambda$, find eigenvector by solving:
$$(A - \lambda I)v = 0$$

### Continuing the Example

**For $\lambda_1 = 5$:**
$$
A - 5I = \begin{bmatrix} -1 & 1 \\ 2 & -2 \end{bmatrix}
$$

Solve $(A - 5I)v = 0$:
$$\begin{bmatrix} -1 & 1 \\ 2 & -2 \end{bmatrix} \begin{bmatrix} v_1 \\ v_2 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \end{bmatrix}$$

From row 1: $-v_1 + v_2 = 0 \Rightarrow v_2 = v_1$

**Eigenvector:** $v_1 = \begin{bmatrix} 1 \\ 1 \end{bmatrix}$ (or any scalar multiple)

**For $\lambda_2 = 2$:**
$$
A - 2I = \begin{bmatrix} 2 & 1 \\ 2 & 1 \end{bmatrix}
$$

From row 1: $2v_1 + v_2 = 0 \Rightarrow v_2 = -2v_1$

**Eigenvector:** $v_2 = \begin{bmatrix} 1 \\ -2 \end{bmatrix}$

---

## 3.5 Properties of Eigenvalues

| Property | Formula/Statement |
|----------|-------------------|
| **Sum of eigenvalues** | $\sum \lambda_i = \text{trace}(A) = \sum a_{ii}$ |
| **Product of eigenvalues** | $\prod \lambda_i = \det(A)$ |
| **Eigenvalues of $A^{-1}$** | $\frac{1}{\lambda_i}$ (with same eigenvectors) |
| **Eigenvalues of $A^k$** | $\lambda_i^k$ (with same eigenvectors) |
| **Eigenvalues of $A + cI$** | $\lambda_i + c$ (with same eigenvectors) |
| **Symmetric matrices** | All eigenvalues are **real** |
| **Positive definite** | All eigenvalues are **positive** |

### Trace Definition
> **Trace** of a matrix = sum of diagonal elements
> $$\text{trace}(A) = a_{11} + a_{22} + \cdots + a_{nn}$$

---

## 3.6 Complete Example: 3×3 Matrix

Find eigenvalues of:
$$
A = \begin{bmatrix} 2 & 0 & 0 \\ 0 & 3 & 0 \\ 0 & 0 & 5 \end{bmatrix}
$$

**Observation:** This is a diagonal matrix!

**For diagonal matrices:**
$$
A - \lambda I = \begin{bmatrix} 2-\lambda & 0 & 0 \\ 0 & 3-\lambda & 0 \\ 0 & 0 & 5-\lambda \end{bmatrix}
$$

$$\det(A - \lambda I) = (2-\lambda)(3-\lambda)(5-\lambda) = 0$$

**Eigenvalues:** $\lambda_1 = 2$, $\lambda_2 = 3$, $\lambda_3 = 5$

> **Key Insight:** For diagonal matrices, eigenvalues are simply the diagonal entries!

---

## 3.7 Special Cases

### Repeated Eigenvalues
If the characteristic polynomial has repeated roots, we have **repeated eigenvalues**.

Example: $\lambda^2 - 4\lambda + 4 = (\lambda - 2)^2 = 0$ gives $\lambda = 2$ with multiplicity 2.

### Complex Eigenvalues
For real matrices, complex eigenvalues always come in **conjugate pairs**.

Example: If $\lambda = 2 + 3i$ is an eigenvalue, then $\lambda = 2 - 3i$ is also an eigenvalue.

### Zero Eigenvalue
If $\lambda = 0$ is an eigenvalue, then:
- $\det(A) = 0$ (since product of eigenvalues = determinant)
- Matrix is singular
- System $Ax = 0$ has non-trivial solutions

---

## 3.8 AI/ML Applications of Eigenvalues

### Principal Component Analysis (PCA)
1. Compute covariance matrix of data
2. Find eigenvalues and eigenvectors
3. Eigenvectors with largest eigenvalues = principal components
4. Project data onto these directions for dimensionality reduction

### Spectral Clustering
1. Build graph Laplacian matrix
2. Find eigenvectors for smallest eigenvalues
3. Use these eigenvectors to cluster data

### PageRank Algorithm
1. Model web as a transition matrix
2. Find the dominant eigenvector (eigenvalue = 1)
3. This gives importance ranking of web pages

### Stability Analysis
- System is stable if all eigenvalues have negative real parts
- Used in control systems and recurrent neural networks

---

# PART 4: OCTAVE IMPLEMENTATION

```octave
% ========== DETERMINANTS ==========
A = [1 2; 3 4];
det(A)                  % Returns determinant

% For 3×3:
B = [1 2 3; 4 5 6; 7 8 9];
det(B)                  % Returns 0 (singular)

% ========== MATRIX INVERSE ==========
A = [4 7; 2 6];
inv(A)                  % Returns inverse

% Check if invertible first:
if det(A) ~= 0
    A_inv = inv(A);
else
    disp('Matrix is singular')
end

% Verify: A * inv(A) should equal I
A * inv(A)

% ========== EIGENVALUES AND EIGENVECTORS ==========
A = [4 1; 2 3];

% Eigenvalues only:
eig(A)                  % Returns column vector of eigenvalues

% Eigenvalues AND eigenvectors:
[V, D] = eig(A)         % V = eigenvectors (columns)
                        % D = diagonal matrix of eigenvalues

% Verify: A * V should equal V * D
A * V
V * D

% ========== TRACE ==========
trace(A)                % Sum of diagonal elements

% ========== USEFUL CHECKS ==========
% For symmetric matrices:
issymmetric(A)

% Check eigenvalue properties:
sum(eig(A))             % Should equal trace(A)
prod(eig(A))            % Should equal det(A)
```

---

# PART 5: PRACTICE PROBLEMS

## Problem 1: 2×2 Determinant

Compute:
$$\det\begin{bmatrix} 5 & 3 \\ 2 & 4 \end{bmatrix}$$

<details>
<summary>Solution</summary>

$\det(A) = (5)(4) - (3)(2) = 20 - 6 = 14$
</details>

---

## Problem 2: 3×3 Determinant

Compute:
$$\det\begin{bmatrix} 2 & 0 & 1 \\ 1 & 3 & 2 \\ 0 & 1 & 4 \end{bmatrix}$$

<details>
<summary>Solution</summary>

Expand along row 1:
$$= 2 \cdot \det\begin{bmatrix} 3 & 2 \\ 1 & 4 \end{bmatrix} - 0 + 1 \cdot \det\begin{bmatrix} 1 & 3 \\ 0 & 1 \end{bmatrix}$$

$$= 2(12 - 2) - 0 + 1(1 - 0)$$
$$= 2(10) + 1 = 21$$
</details>

---

## Problem 3: 2×2 Inverse

Find the inverse of:
$$A = \begin{bmatrix} 3 & 1 \\ 5 & 2 \end{bmatrix}$$

<details>
<summary>Solution</summary>

$\det(A) = 3(2) - 1(5) = 6 - 5 = 1$

$$A^{-1} = \frac{1}{1}\begin{bmatrix} 2 & -1 \\ -5 & 3 \end{bmatrix} = \begin{bmatrix} 2 & -1 \\ -5 & 3 \end{bmatrix}$$

Verify: $AA^{-1} = \begin{bmatrix} 3 & 1 \\ 5 & 2 \end{bmatrix}\begin{bmatrix} 2 & -1 \\ -5 & 3 \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}$ ✓
</details>

---

## Problem 4: Invertibility Check

Is this matrix invertible?
$$A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{bmatrix}$$

<details>
<summary>Solution</summary>

Compute determinant (from earlier example): $\det(A) = 0$

**Not invertible** (singular matrix)

Alternative check: Row 3 = Row 1 + Row 2 (dependent rows)
</details>

---

## Problem 5: Find Eigenvalues

Find the eigenvalues of:
$$A = \begin{bmatrix} 3 & 1 \\ 0 & 2 \end{bmatrix}$$

<details>
<summary>Solution</summary>

This is upper triangular! For triangular matrices, eigenvalues = diagonal entries.

**Eigenvalues:** $\lambda_1 = 3$, $\lambda_2 = 2$

Verify with characteristic equation:
$$\det(A - \lambda I) = (3-\lambda)(2-\lambda) - 0 = 0$$
$$\lambda = 3 \text{ or } \lambda = 2$$ ✓
</details>

---

## Problem 6: Find Eigenvalues and Eigenvectors

For:
$$A = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix}$$

<details>
<summary>Solution</summary>

**Characteristic equation:**
$$\det(A - \lambda I) = (2-\lambda)^2 - 1 = 0$$
$$\lambda^2 - 4\lambda + 3 = 0$$
$$(\lambda - 3)(\lambda - 1) = 0$$

**Eigenvalues:** $\lambda_1 = 3$, $\lambda_2 = 1$

**For $\lambda = 3$:**
$(A - 3I)v = 0$:
$$\begin{bmatrix} -1 & 1 \\ 1 & -1 \end{bmatrix}v = 0$$
$v_1 = v_2$ → Eigenvector: $\begin{bmatrix} 1 \\ 1 \end{bmatrix}$

**For $\lambda = 1$:**
$(A - I)v = 0$:
$$\begin{bmatrix} 1 & 1 \\ 1 & 1 \end{bmatrix}v = 0$$
$v_1 = -v_2$ → Eigenvector: $\begin{bmatrix} 1 \\ -1 \end{bmatrix}$
</details>

---

## Problem 7: Verify Eigenvalue Properties

For:
$$A = \begin{bmatrix} 4 & 1 \\ 2 & 3 \end{bmatrix}$$

with eigenvalues $\lambda_1 = 5$, $\lambda_2 = 2$, verify:
a) Sum of eigenvalues = trace
b) Product of eigenvalues = determinant

<details>
<summary>Solution</summary>

a) Sum: $5 + 2 = 7$
   Trace: $4 + 3 = 7$ ✓

b) Product: $5 \times 2 = 10$
   Det: $4(3) - 1(2) = 12 - 2 = 10$ ✓
</details>

---

# KEY TAKEAWAYS

| Concept | Key Point |
|---------|-----------|
| **2×2 Determinant** | $ad - bc$ |
| **3×3 Determinant** | Cofactor expansion or Sarrus' rule |
| **Singular Matrix** | $\det(A) = 0$, no inverse |
| **2×2 Inverse** | Swap diagonals, negate off-diagonals, divide by det |
| **General Inverse** | Gauss-Jordan: $[A\|I] \rightarrow [I\|A^{-1}]$ |
| **Characteristic Equation** | $\det(A - \lambda I) = 0$ |
| **Eigenvalue Properties** | Sum = trace, Product = det |
| **Triangular/Diagonal** | Eigenvalues = diagonal entries |
| **Symmetric Matrices** | Real eigenvalues, orthogonal eigenvectors |

---

# QUICK REFERENCE CARD

## Formulas to Memorize

**2×2 Determinant:**
$$\det\begin{pmatrix} a & b \\ c & d \end{pmatrix} = ad - bc$$

**2×2 Inverse:**
$$A^{-1} = \frac{1}{ad-bc}\begin{pmatrix} d & -b \\ -c & a \end{pmatrix}$$

**Characteristic Equation:**
$$\det(A - \lambda I) = 0$$

**Eigenvalue-Eigenvector Equation:**
$$Av = \lambda v$$

**Trace-Determinant Relationships:**
$$\sum \lambda_i = \text{tr}(A), \quad \prod \lambda_i = \det(A)$$

---

**Previous:** Lecture 0b - Linear Systems and Rank  
**Ready for:** Mathematics for ML Course (January 17th)
