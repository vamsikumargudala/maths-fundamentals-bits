# Lecture 0a: Matrix Fundamentals and Operations
## Comprehensive Briefing Document

---

# EXECUTIVE SUMMARY

## Critical Takeaways

1. **Matrices are the foundation of AI/ML** - All data (images, audio, text) must be converted to matrix form for GPU processing
2. **Matrix multiplication is NOT commutative** - $AB \neq BA$ in general; this is the #1 mistake students make
3. **Three elementary row operations** preserve linear system solutions - interchange, addition, and scalar multiplication (ROWS ONLY)
4. **Special matrix types** (symmetric, sparse, positive definite) have specific applications in ML algorithms

## Topics Covered
- Matrix definition, notation, and dimensions
- Matrix operations (addition, scalar multiplication, matrix multiplication, transposition)
- Special matrix types
- Elementary row operations

---

# PART 1: MATRIX FUNDAMENTALS

## 1.1 What is a Matrix?

### Definition
> A **matrix** is a rectangular array of numbers (or functions) enclosed in brackets. The individual numbers are called **entries** or **elements**.

### Visual Representation
$$
A = \begin{bmatrix} 
a_{11} & a_{12} & a_{13} \\
a_{21} & a_{22} & a_{23} \\
a_{31} & a_{32} & a_{33}
\end{bmatrix}
$$

**Entry notation:** $a_{jk}$ means the element in row $j$, column $k$

### Example
$$
A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix}
$$
- $a_{11} = 1$ (row 1, column 1)
- $a_{12} = 2$ (row 1, column 2)
- $a_{21} = 4$ (row 2, column 1)
- $a_{23} = 6$ (row 2, column 3)

---

## 1.2 Matrix Dimensions (Size)

### Definition
> A matrix with $m$ rows and $n$ columns is called an **$m \times n$ matrix** (read "$m$ by $n$").

### Critical Rule
> **Rows ALWAYS come first** in dimension notation.

### Examples
| Matrix | Dimensions | Description |
|--------|------------|-------------|
| $\begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix}$ | $2 \times 3$ | 2 rows, 3 columns |
| $\begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}$ | $3 \times 1$ | Column vector |
| $\begin{bmatrix} 1 & 2 & 3 \end{bmatrix}$ | $1 \times 3$ | Row vector |
| $\begin{bmatrix} 1 & 2 \\ 3 & 4 \\ 5 & 6 \end{bmatrix}$ | $3 \times 2$ | 3 rows, 2 columns |

---

## 1.3 Vectors as Special Matrices

### Definition
> A **vector** is a matrix with only one row or only one column.

| Type | Definition | Example | Dimension |
|------|------------|---------|-----------|
| **Row Vector** | Matrix with 1 row | $\begin{bmatrix} 1 & 2 & 3 \end{bmatrix}$ | $1 \times n$ |
| **Column Vector** | Matrix with 1 column | $\begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}$ | $m \times 1$ |

### AI/ML Context
> In machine learning, data points are typically represented as **column vectors**, and a dataset is a matrix where each column is one data sample.

---

## 1.4 Matrix Equality

### Definition
> Two matrices $A$ and $B$ are **equal** if and only if:
> 1. They have the **same dimensions** ($m \times n$)
> 2. **Every corresponding entry is identical**: $a_{jk} = b_{jk}$ for all $j, k$

### Example
$$
\begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix} = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix} \quad \checkmark
$$

$$
\begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix} \neq \begin{bmatrix} 1 & 2 & 0 \\ 3 & 4 & 0 \end{bmatrix} \quad \text{(different dimensions)}
$$

$$
\begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix} \neq \begin{bmatrix} 1 & 2 \\ 3 & 5 \end{bmatrix} \quad \text{(different entry at } a_{22}\text{)}
$$

---

## 1.5 Why Matrices Matter in AI/ML

### Professor's Explanation
> Matrices are the **backbone of AI** because all real-world data must be converted into matrix form for processing.

| Data Type | Matrix Representation |
|-----------|----------------------|
| **Images** | Pixel values in a 2D grid (or 3D for RGB) |
| **Audio** | Amplitude values over time samples |
| **Text** | Word embeddings (vectors for each word) |
| **Tabular Data** | Rows = samples, Columns = features |

### Why Matrices Enable AI
- **Parallel Processing:** GPUs are optimized for matrix operations
- **Batch Processing:** Process thousands of samples simultaneously
- **Mathematical Framework:** Linear algebra provides optimization tools

---

# PART 2: MATRIX OPERATIONS

## 2.1 Matrix Addition

### Definition
> The sum $C = A + B$ is defined **only if** $A$ and $B$ have the **same dimensions**.
> Each entry is computed as: $c_{jk} = a_{jk} + b_{jk}$

### Example
$$
\begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix} + \begin{bmatrix} 5 & 6 \\ 7 & 8 \end{bmatrix} = \begin{bmatrix} 1+5 & 2+6 \\ 3+7 & 4+8 \end{bmatrix} = \begin{bmatrix} 6 & 8 \\ 10 & 12 \end{bmatrix}
$$

### Properties
| Property | Formula | Meaning |
|----------|---------|---------|
| **Commutative** | $A + B = B + A$ | Order doesn't matter |
| **Associative** | $(A + B) + C = A + (B + C)$ | Grouping doesn't matter |
| **Zero Matrix** | $A + O = A$ | Adding zero matrix gives same matrix |

### ⚠️ Common Mistake
> **Cannot add matrices of different dimensions!**
> 
> $\begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}_{2 \times 2} + \begin{bmatrix} 1 & 2 & 3 \end{bmatrix}_{1 \times 3}$ is **UNDEFINED**

---

## 2.2 Scalar Multiplication

### Definition
> Multiplying matrix $A$ by scalar (number) $c$ means multiplying **every entry** by $c$.
> 
> If $B = cA$, then $b_{jk} = c \cdot a_{jk}$

### Example
$$
3 \times \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix} = \begin{bmatrix} 3 \times 1 & 3 \times 2 \\ 3 \times 3 & 3 \times 4 \end{bmatrix} = \begin{bmatrix} 3 & 6 \\ 9 & 12 \end{bmatrix}
$$

### Properties
- $c(A + B) = cA + cB$ (distributive over addition)
- $(c + d)A = cA + dA$ (distributive over scalar addition)
- $c(dA) = (cd)A$ (associative with scalars)
- $1 \cdot A = A$ (identity)
- $0 \cdot A = O$ (zero matrix)

---

## 2.3 Matrix Multiplication

### Definition
> The product $C = AB$ is defined **if and only if** the **number of columns in $A$ equals the number of rows in $B$**.

### Dimension Rule
$$
A_{m \times \boxed{n}} \times B_{\boxed{n} \times p} = C_{m \times p}
$$

The **inner dimensions** must match. The result has the **outer dimensions**.

### How to Compute Entry $c_{jk}$
> Take the **dot product** of row $j$ of $A$ with column $k$ of $B$.

$$
c_{jk} = \sum_{i=1}^{n} a_{ji} \cdot b_{ik} = a_{j1}b_{1k} + a_{j2}b_{2k} + \cdots + a_{jn}b_{nk}
$$

### Step-by-Step Example

**Given:**
$$
A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix}_{2 \times 3}, \quad B = \begin{bmatrix} 7 & 8 \\ 9 & 10 \\ 11 & 12 \end{bmatrix}_{3 \times 2}
$$

**Check compatibility:** Columns of $A$ = 3, Rows of $B$ = 3 ✓

**Result dimensions:** $C$ will be $2 \times 2$

**Compute $c_{11}$:** (Row 1 of $A$) · (Column 1 of $B$)
$$c_{11} = (1)(7) + (2)(9) + (3)(11) = 7 + 18 + 33 = 58$$

**Compute $c_{12}$:** (Row 1 of $A$) · (Column 2 of $B$)
$$c_{12} = (1)(8) + (2)(10) + (3)(12) = 8 + 20 + 36 = 64$$

**Compute $c_{21}$:** (Row 2 of $A$) · (Column 1 of $B$)
$$c_{21} = (4)(7) + (5)(9) + (6)(11) = 28 + 45 + 66 = 139$$

**Compute $c_{22}$:** (Row 2 of $A$) · (Column 2 of $B$)
$$c_{22} = (4)(8) + (5)(10) + (6)(12) = 32 + 50 + 72 = 154$$

**Result:**
$$
C = AB = \begin{bmatrix} 58 & 64 \\ 139 & 154 \end{bmatrix}
$$

### ⚠️ Critical Properties

| Property | Truth | Explanation |
|----------|-------|-------------|
| **Commutative** | ❌ FALSE | $AB \neq BA$ in general |
| **Associative** | ✓ TRUE | $(AB)C = A(BC)$ |
| **Distributive** | ✓ TRUE | $A(B+C) = AB + AC$ |
| **Zero Products** | ⚠️ TRICKY | $AB = 0$ does NOT mean $A = 0$ or $B = 0$ |

### Why $AB \neq BA$?
1. If $A$ is $m \times n$ and $B$ is $n \times p$, then $AB$ exists
2. But $BA$ requires $B$ to have same columns as $A$ has rows
3. Even if both exist, the entries are different!

### Example of Non-Commutativity
$$
A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}, \quad B = \begin{bmatrix} 0 & 1 \\ 0 & 0 \end{bmatrix}
$$

$$
AB = \begin{bmatrix} 0 & 1 \\ 0 & 3 \end{bmatrix} \neq BA = \begin{bmatrix} 3 & 4 \\ 0 & 0 \end{bmatrix}
$$

---

## 2.4 Transposition

### Definition
> The **transpose** $A^\top$ (or $A^T$) is formed by **interchanging rows and columns**.
> - Row 1 of $A$ becomes Column 1 of $A^\top$
> - Row 2 of $A$ becomes Column 2 of $A^\top$
> - And so on...

### Formula
> If $B = A^\top$, then $b_{jk} = a_{kj}$

### Example
$$
A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix}_{2 \times 3} \quad \Rightarrow \quad A^\top = \begin{bmatrix} 1 & 4 \\ 2 & 5 \\ 3 & 6 \end{bmatrix}_{3 \times 2}
$$

### Properties of Transpose
| Property | Formula |
|----------|---------|
| Double transpose | $(A^\top)^\top = A$ |
| Sum transpose | $(A + B)^\top = A^\top + B^\top$ |
| Scalar transpose | $(cA)^\top = cA^\top$ |
| **Product transpose** | $(AB)^\top = B^\top A^\top$ ⚠️ **Order reverses!** |

### The Reversal Rule (Important!)
$$
(AB)^\top = B^\top A^\top
$$

This is used frequently in gradient computations in neural networks.

---

# PART 3: SPECIAL MATRIX TYPES

## 3.1 Square Matrix
> A matrix where **rows = columns** ($n \times n$).
> Only square matrices have determinants and can have inverses.

$$
\begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{bmatrix}_{3 \times 3}
$$

---

## 3.2 Symmetric Matrix

### Definition
> A square matrix where $A^\top = A$.
> 
> Equivalently: $a_{jk} = a_{kj}$ for all entries (mirror across diagonal).

### Example
$$
A = \begin{bmatrix} 1 & 2 & 3 \\ 2 & 4 & 5 \\ 3 & 5 & 6 \end{bmatrix} = A^\top \quad \checkmark \text{ Symmetric}
$$

### AI/ML Applications
- **Covariance matrices** are always symmetric
- **Distance matrices** are symmetric
- Many kernels in SVM are symmetric

---

## 3.3 Skew-Symmetric Matrix

### Definition
> A square matrix where $A^\top = -A$.
> 
> **Critical fact:** Diagonal entries must be **zero** (since $a_{jj} = -a_{jj}$ implies $a_{jj} = 0$).

### Example
$$
A = \begin{bmatrix} 0 & 2 & -3 \\ -2 & 0 & 5 \\ 3 & -5 & 0 \end{bmatrix}
$$

Check: $a_{12} = 2$ and $a_{21} = -2$ ✓

---

## 3.4 Triangular Matrices

### Upper Triangular
> All entries **below** the main diagonal are zero.

$$
\begin{bmatrix} 1 & 2 & 3 \\ 0 & 4 & 5 \\ 0 & 0 & 6 \end{bmatrix}
$$

### Lower Triangular
> All entries **above** the main diagonal are zero.

$$
\begin{bmatrix} 1 & 0 & 0 \\ 2 & 3 & 0 \\ 4 & 5 & 6 \end{bmatrix}
$$

### Why Important?
- Easy to compute determinant (product of diagonal)
- Easy to solve triangular systems (forward/back substitution)
- LU decomposition produces triangular matrices

---

## 3.5 Diagonal Matrix

### Definition
> All off-diagonal entries are zero. Only $a_{ii}$ can be non-zero.

$$
D = \begin{bmatrix} 3 & 0 & 0 \\ 0 & 7 & 0 \\ 0 & 0 & 2 \end{bmatrix}
$$

### Properties
- Determinant = product of diagonal entries: $\det(D) = 3 \times 7 \times 2 = 42$
- Inverse (if exists) = reciprocals on diagonal: $D^{-1} = \text{diag}(1/3, 1/7, 1/2)$
- Powers are easy: $D^n = \text{diag}(3^n, 7^n, 2^n)$

---

## 3.6 Identity Matrix

### Definition
> Diagonal matrix with all 1s on the diagonal. Denoted $I$ or $I_n$.

$$
I_3 = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}
$$

### Property
$$AI = IA = A$$

The identity matrix is the **multiplicative identity** for matrices.

---

## 3.7 Sparse Matrix

### Definition
> A matrix containing **mostly zeros** with very few non-zero entries.

### Example (Sparse)
$$
\begin{bmatrix} 0 & 0 & 3 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 2 & 0 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}
$$

### AI/ML Applications
| Application | Why Sparse |
|-------------|-----------|
| **NLP (Bag of Words)** | Most words don't appear in a document |
| **Social Networks** | Most people aren't connected to each other |
| **Recommendation Systems** | Users rate only few items |

### Why Important?
- Special storage formats (CSR, COO) save memory
- Special algorithms for sparse matrix operations
- Essential for scaling to large datasets

---

## 3.8 Positive Definite Matrix

### Definition
> A real symmetric matrix $A$ where $x^\top A x > 0$ for **any** non-zero vector $x$.

### AI/ML Applications
- **PCA:** Covariance matrices are positive semi-definite
- **Optimization:** Convex functions have positive definite Hessians
- **Gaussian Processes:** Kernel matrices must be positive semi-definite

---

# PART 4: ELEMENTARY ROW OPERATIONS

## 4.1 The Three Permitted Operations

### Definition
> There are exactly **three elementary row operations** that can be applied to a matrix:

| Operation | Description | Notation |
|-----------|-------------|----------|
| **1. Interchange** | Swap two rows | $R_i \leftrightarrow R_j$ |
| **2. Scalar Multiplication** | Multiply a row by non-zero constant | $R_i \rightarrow cR_i$ (where $c \neq 0$) |
| **3. Row Addition** | Add multiple of one row to another | $R_i \rightarrow R_i + cR_j$ |

### ⚠️ CRITICAL RULE
> These operations apply **ONLY TO ROWS**, never to columns!

---

## 4.2 Why These Operations?

### Key Theorem
> Elementary row operations **do not change the solutions** of a linear system.

This means we can simplify a system of equations using these operations and still get the same answer.

---

## 4.3 Examples of Each Operation

### Operation 1: Interchange
$$
\begin{bmatrix} 0 & 1 & 2 \\ 3 & 4 & 5 \\ 6 & 7 & 8 \end{bmatrix} 
\xrightarrow{R_1 \leftrightarrow R_2}
\begin{bmatrix} 3 & 4 & 5 \\ 0 & 1 & 2 \\ 6 & 7 & 8 \end{bmatrix}
$$

### Operation 2: Scalar Multiplication
$$
\begin{bmatrix} 2 & 4 & 6 \\ 1 & 2 & 3 \end{bmatrix}
\xrightarrow{R_1 \rightarrow \frac{1}{2}R_1}
\begin{bmatrix} 1 & 2 & 3 \\ 1 & 2 & 3 \end{bmatrix}
$$

### Operation 3: Row Addition
$$
\begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix}
\xrightarrow{R_2 \rightarrow R_2 - 4R_1}
\begin{bmatrix} 1 & 2 & 3 \\ 0 & -3 & -6 \end{bmatrix}
$$

---

## 4.4 Common Mistakes

| Mistake | Problem |
|---------|---------|
| Applying to columns | **Wrong!** Operations are for rows only |
| Multiplying by zero | **Invalid!** Scalar must be non-zero |
| Wrong reference row | Can accidentally undo previous work |
| Not tracking operations | Makes it hard to verify work |

---

# PART 5: OCTAVE IMPLEMENTATION

```octave
% ========== MATRIX CREATION ==========
A = [1 2 3; 4 5 6]          % 2×3 matrix (semicolons separate rows)
B = [1; 2; 3]               % Column vector
C = [1 2 3]                 % Row vector
zeros(3, 4)                 % 3×4 zero matrix
ones(2, 3)                  % 2×3 matrix of ones
eye(4)                      % 4×4 identity matrix

% ========== MATRIX INFO ==========
size(A)                     % Returns [rows, cols]
[m, n] = size(A)            % Store dimensions separately

% ========== MATRIX OPERATIONS ==========
A + B                       % Addition (same size required)
3 * A                       % Scalar multiplication
A * B                       % Matrix multiplication (check dimensions!)
A'                          % Transpose

% ========== SPECIAL CHECKS ==========
issymmetric(A)              % Returns 1 if symmetric, 0 otherwise

% ========== ROW OPERATIONS ==========
% Interchange rows 1 and 2:
A([1 2], :) = A([2 1], :)

% Multiply row 1 by scalar c:
A(1, :) = c * A(1, :)

% Add c times row 2 to row 1:
A(1, :) = A(1, :) + c * A(2, :)
```

---

# PART 6: PRACTICE PROBLEMS

## Problem 1: Dimension Identification
Given: $A = \begin{bmatrix} 1 & 2 & 3 & 4 \\ 5 & 6 & 7 & 8 \end{bmatrix}$

What is the dimension of $A$?

<details>
<summary>Solution</summary>

$A$ is a $2 \times 4$ matrix (2 rows, 4 columns)
</details>

---

## Problem 2: Matrix Multiplication Compatibility

Given $A$ is $3 \times 3$ and $B$ is $3 \times 4$:
- Is $AB$ defined? If so, what size?
- Is $BA$ defined? If so, what size?

<details>
<summary>Solution</summary>

- $AB$: Yes, defined. Columns of $A$ (3) = Rows of $B$ (3). Result is $3 \times 4$.
- $BA$: No, undefined. Columns of $B$ (4) ≠ Rows of $A$ (3).
</details>

---

## Problem 3: Compute a Product Entry

Given:
$$A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}, \quad B = \begin{bmatrix} 5 & 6 \\ 7 & 8 \end{bmatrix}$$

Find $c_{12}$ of $C = AB$.

<details>
<summary>Solution</summary>

$c_{12}$ = (Row 1 of $A$) · (Column 2 of $B$)
$$c_{12} = (1)(6) + (2)(8) = 6 + 16 = 22$$
</details>

---

## Problem 4: Transpose

Find $A^\top$ for:
$$A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix}$$

<details>
<summary>Solution</summary>

$$A^\top = \begin{bmatrix} 1 & 4 \\ 2 & 5 \\ 3 & 6 \end{bmatrix}$$
</details>

---

## Problem 5: Identify Matrix Type

Classify each matrix:

a) $\begin{bmatrix} 1 & 2 \\ 2 & 3 \end{bmatrix}$

b) $\begin{bmatrix} 0 & -2 \\ 2 & 0 \end{bmatrix}$

c) $\begin{bmatrix} 1 & 0 & 0 \\ 2 & 3 & 0 \\ 4 & 5 & 6 \end{bmatrix}$

<details>
<summary>Solution</summary>

a) **Symmetric** ($A^\top = A$)

b) **Skew-symmetric** ($A^\top = -A$, diagonals are 0)

c) **Lower triangular** (zeros above diagonal)
</details>

---

## Problem 6: Row Operation

Apply $R_2 \rightarrow R_2 - 3R_1$ to:
$$\begin{bmatrix} 1 & 2 & 3 \\ 3 & 5 & 7 \end{bmatrix}$$

<details>
<summary>Solution</summary>

New $R_2 = [3, 5, 7] - 3[1, 2, 3] = [3-3, 5-6, 7-9] = [0, -1, -2]$

$$\begin{bmatrix} 1 & 2 & 3 \\ 0 & -1 & -2 \end{bmatrix}$$
</details>

---

# KEY TAKEAWAYS

| Concept | Key Point |
|---------|-----------|
| Matrix Size | Always $\text{rows} \times \text{columns}$ |
| Addition | Same dimensions required |
| Multiplication | Inner dimensions must match; result has outer dimensions |
| Non-Commutativity | $AB \neq BA$ — most important rule! |
| Transpose | Rows become columns; $(AB)^\top = B^\top A^\top$ |
| Row Operations | Three types, ROWS ONLY, preserve solutions |
| Sparse Matrices | Essential for NLP, social networks, recommendations |

---

**Next:** Lecture 0b - Row Echelon Form, Rank, and Solving Linear Systems
