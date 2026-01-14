# Session 1: Matrix Fundamentals and Row Operations
**Course:** Zero Level Mathematical Foundation - M.Tech AI/ML  
**Session Type:** Bridge Session (0th Session)  
**Purpose:** Prepare students for Mathematical Foundations of AI/ML

---

# PART A: DEFINITIONS (What Was Presented)

---

## 1. Matrix - Definition and Notation

### What is a Matrix?
> **Definition:** A matrix is a **rectangular array** of numbers or functions enclosed in brackets. The individual numbers or functions inside are called **entries** or **elements**.

**Example:**
$$
A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix}
$$
This matrix has entries: $a_{11}=1$, $a_{12}=2$, $a_{13}=3$, $a_{21}=4$, $a_{22}=5$, $a_{23}=6$

### Matrix Size (Dimension)
> **Definition:** A matrix with $m$ rows and $n$ columns is called an **$m \times n$ matrix** (read as "$m$ by $n$").

**Rule:** Rows ALWAYS come first in notation.

**Example:** The matrix above is a $2 \times 3$ matrix (2 rows, 3 columns)

### What is a Vector?
> **Definition:** A vector is a special matrix that has either:
> - **Only one row** → called a **row vector**
> - **Only one column** → called a **column vector**

**Examples:**
- Row vector ($1 \times 3$): $\begin{bmatrix} 1 & 2 & 3 \end{bmatrix}$
- Column vector ($3 \times 1$): $\begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}$

### Matrix Equality
> **Definition:** Two matrices $A$ and $B$ are equal **if and only if**:
> 1. They have the **same size** (same number of rows AND columns)
> 2. **Every corresponding entry is identical** (i.e., $a_{jk} = b_{jk}$ for all $j, k$)

---

## 2. Matrix Operations - Definitions

### Matrix Addition
> **Definition:** The sum of two matrices $A + B$ is defined **only if** they are the **same size**. You add corresponding entries element-by-element.

**Formula:** If $C = A + B$, then $c_{jk} = a_{jk} + b_{jk}$

**Example:**
$$
\begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix} + \begin{bmatrix} 5 & 6 \\ 7 & 8 \end{bmatrix} = \begin{bmatrix} 1+5 & 2+6 \\ 3+7 & 4+8 \end{bmatrix} = \begin{bmatrix} 6 & 8 \\ 10 & 12 \end{bmatrix}
$$

**Properties:**
- **Commutative:** $A + B = B + A$
- **Associative:** $(A + B) + C = A + (B + C)$

### Scalar Multiplication
> **Definition:** Multiplying a matrix by a scalar (number) $c$ means multiplying **every entry** in the matrix by that number.

**Formula:** If $B = cA$, then $b_{jk} = c \cdot a_{jk}$

**Example:**
$$
3 \times \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix} = \begin{bmatrix} 3 \times 1 & 3 \times 2 \\ 3 \times 3 & 3 \times 4 \end{bmatrix} = \begin{bmatrix} 3 & 6 \\ 9 & 12 \end{bmatrix}
$$

### Matrix Multiplication
> **Definition:** The product $C = AB$ is defined **if and only if** the **number of columns in $A$ equals the number of rows in $B$**.

**Size Rule:** If $A$ is $m \times n$ and $B$ is $n \times p$, then $C = AB$ is $m \times p$

**How to compute entry $c_{jk}$:**
> Take the **dot product** of the $j$-th row of $A$ and the $k$-th column of $B$.

**Step-by-step for $c_{jk}$:**
1. Take row $j$ from matrix $A$
2. Take column $k$ from matrix $B$
3. Multiply corresponding elements and sum them up

**Example:** For matrices $A$ ($2 \times 3$) and $B$ ($3 \times 2$):
$$
A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix}, \quad B = \begin{bmatrix} 7 & 8 \\ 9 & 10 \\ 11 & 12 \end{bmatrix}
$$

To find $c_{11}$: Row 1 of $A$ · Column 1 of $B$ = $(1)(7) + (2)(9) + (3)(11) = 7 + 18 + 33 = 58$

### Transposition
> **Definition:** The transpose $A^\top$ is formed by **interchanging rows and columns**:
> - The 1st row of $A$ becomes the 1st column of $A^\top$
> - The 2nd row of $A$ becomes the 2nd column of $A^\top$
> - And so on...

**Formula:** If $B = A^\top$, then $b_{jk} = a_{kj}$

**Example:**
$$
A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix} \quad \Rightarrow \quad A^\top = \begin{bmatrix} 1 & 4 \\ 2 & 5 \\ 3 & 6 \end{bmatrix}
$$

**Reversal Rule for Products:**
> $(AB)^\top = B^\top A^\top$ (the order is **reversed**)

---

## 3. Special Matrix Types - Definitions

### Symmetric Matrix
> **Definition:** A square matrix $A$ where $A^\top = A$.
> 
> In other words: $a_{jk} = a_{kj}$ for all entries (matrix is mirror image across diagonal).

**Example:**
$$
\begin{bmatrix} 1 & 2 & 3 \\ 2 & 4 & 5 \\ 3 & 5 & 6 \end{bmatrix}
$$

### Skew-Symmetric Matrix
> **Definition:** A square matrix $A$ where $A^\top = -A$.
> 
> **Important fact:** The diagonal elements **must be zero** (since $a_{jj} = -a_{jj}$ implies $a_{jj} = 0$).

**Example:**
$$
\begin{bmatrix} 0 & 2 & -3 \\ -2 & 0 & 5 \\ 3 & -5 & 0 \end{bmatrix}
$$

### Triangular Matrices
> **Upper Triangular:** All entries **below the main diagonal** are zero.
> 
> **Lower Triangular:** All entries **above the main diagonal** are zero.

**Examples:**
$$
\text{Upper: } \begin{bmatrix} 1 & 2 & 3 \\ 0 & 4 & 5 \\ 0 & 0 & 6 \end{bmatrix} \quad \text{Lower: } \begin{bmatrix} 1 & 0 & 0 \\ 2 & 3 & 0 \\ 4 & 5 & 6 \end{bmatrix}
$$

### Diagonal Matrix
> **Definition:** All entries above AND below the main diagonal are zero. Only diagonal entries can be non-zero.

**Example:**
$$
\begin{bmatrix} 3 & 0 & 0 \\ 0 & 7 & 0 \\ 0 & 0 & 2 \end{bmatrix}
$$

### Sparse Matrix
> **Definition:** A matrix that contains **many zeros** and very few non-zero entries.

### Positive Definite Matrix
> **Definition:** A real symmetric matrix where $x^\top A x > 0$ for **any** non-zero vector $x$.

---

## 4. Elementary Row Operations - Definition

> **Definition:** There are exactly **three permitted operations** to transform a matrix:

| Operation | Description | Notation Example |
|-----------|-------------|------------------|
| **1. Interchange** | Swap any two rows | $R_1 \leftrightarrow R_2$ |
| **2. Addition** | Add a constant multiple of one row to another row | $R_2 \rightarrow R_2 + 3R_1$ |
| **3. Multiplication** | Multiply a row by a **non-zero** constant $c$ | $R_1 \rightarrow 2R_1$ |

> **Critical Rule:** These operations apply to **ROWS ONLY**, never to columns.

---

## 5. Row Echelon Form (REF) - Definition

> **Definition:** A matrix is in **Row Echelon Form (REF)** if it satisfies ALL three conditions:

| Condition | Meaning |
|-----------|---------|
| **1** | All rows consisting entirely of zeros are at the **bottom** of the matrix |
| **2** | The first non-zero entry in each row (called the **leading entry**) is in a column **to the right of** the leading entry of the row above it |
| **3** | All entries in a column **below** a leading entry are **zeros** |

**Example of REF:**
$$
\begin{bmatrix} 2 & 3 & 1 & 5 \\ 0 & 1 & 4 & 2 \\ 0 & 0 & 3 & 1 \\ 0 & 0 & 0 & 0 \end{bmatrix}
$$

### Reduced Row Echelon Form (RREF) - Definition

> **Definition:** A matrix is in **RREF** if it is in REF **AND** satisfies two additional conditions:

| Additional Condition | Meaning |
|---------------------|---------|
| **4** | The leading entry in every non-zero row is **1** |
| **5** | Each leading 1 is the **only non-zero entry** in its entire column |

**Example of RREF:**
$$
\begin{bmatrix} 1 & 0 & 0 & 2 \\ 0 & 1 & 0 & 3 \\ 0 & 0 & 1 & 1 \\ 0 & 0 & 0 & 0 \end{bmatrix}
$$

> **Key Fact:** While REF is NOT unique (different row operations can give different REF forms), **RREF is always UNIQUE** for any given matrix.

---

## 6. Matrix Rank - Definition

> **Definition:** The **rank** of a matrix is the **number of non-zero rows** in its Row Echelon Form (REF).

**Example:** If a matrix reduces to:
$$
\begin{bmatrix} 1 & 2 & 3 \\ 0 & 1 & 4 \\ 0 & 0 & 0 \end{bmatrix}
$$
The rank is **2** (two non-zero rows).

> **Key Property (Invariance):** The rank does NOT change no matter which elementary row operations you perform. It is **invariant**.

---

## 7. Linear Systems - Definitions

### Linear System
> **Definition:** A set of $m$ linear equations with $n$ unknowns ($x_1, x_2, \ldots, x_n$).

**Example:**
$$
\begin{cases}
x_1 + 2x_2 + 3x_3 = 9 \\
4x_1 + 5x_2 + 6x_3 = 24
\end{cases}
$$

### Augmented Matrix
> **Definition:** A compact representation $[A | b]$ containing the coefficient matrix $A$ and the constants vector $b$ separated by a vertical line.

**Example:** For the system above:
$$
\left[\begin{array}{ccc|c} 1 & 2 & 3 & 9 \\ 4 & 5 & 6 & 24 \end{array}\right]
$$

### Homogeneous vs Non-Homogeneous
> **Homogeneous System:** All constant values ($b_j$) are **zero**. Form: $Ax = 0$
> 
> **Non-Homogeneous System:** At least one constant value is **non-zero**. Form: $Ax = b$ where $b \neq 0$

### Pivot Variables vs Free Variables
> **Pivot Variables:** Variables corresponding to columns with leading entries (leading 1s in RREF)
> 
> **Free Variables:** Variables corresponding to columns WITHOUT leading entries

---

## 8. Consistency of Linear Systems - Rules

> **Fundamental Rule:** A system is **consistent** (has at least one solution) **if and only if**:
> $$\text{rank}(A) = \text{rank}([A|b])$$

### Complete Classification:

| Condition | Result |
|-----------|--------|
| $\text{rank}(A) < \text{rank}([A\|b])$ | **No solution** (inconsistent) |
| $\text{rank}(A) = \text{rank}([A\|b]) = n$ (number of unknowns) | **Unique solution** |
| $\text{rank}(A) = \text{rank}([A\|b]) < n$ | **Infinite solutions** (free variables exist) |

> **How to detect inconsistency:** If any row reduces to $[0 \quad 0 \quad \cdots \quad 0 \quad | \quad c]$ where $c \neq 0$, the system has **no solution**.
> 
> This represents the equation $0 = c$ which is impossible.

---

# PART B: PROFESSOR'S EXPLANATIONS (What Was Discussed)

---

## Why Matrices Matter in AI/ML

**Professor's Explanation:**
> Matrices are the **backbone of AI** because all real-world data must be converted into matrix form for processing:
> - **Images** → Pixels stored as matrix values
> - **Audio** → Amplitude values over time
> - **Text** → Word embeddings (vector representations)
>
> This matrix representation allows **parallel processing on GPUs**, which is essential for training large models.

---

## Analogy for Understanding Rank

**Professor's Analogy:**
> Finding the rank of a matrix is like **distilling a story down to its unique plot points**.
> 
> Even if you reword the sentences (apply row operations), the number of truly unique, independent ideas (non-zero rows) remains the same.

---

## Why Sparse Matrices are Important

**Professor's Explanation:**
> Sparse matrices (mostly zeros) are essential for efficiency in:
> - **NLP:** Bag-of-words representations (most words don't appear in a given document)
> - **Social Networks:** Friendship graphs (most people aren't connected to each other)
>
> Special algorithms exist to store and process sparse matrices efficiently.

---

## Where Positive Definite Matrices Appear

**Professor's Explanation:**
> Positive definite matrices are critical for:
> - **PCA (Principal Component Analysis):** Covariance matrices must be positive semi-definite
> - **Optimization:** Convex optimization problems require positive definite Hessians

---

## Common Mistakes Students Make

**Professor highlighted these errors:**

| Mistake | Why It's Wrong |
|---------|----------------|
| Assuming $AB = BA$ | Matrix multiplication is **NOT commutative** |
| Adding matrices of different sizes | Addition requires **identical dimensions** |
| Multiplying when dimensions don't match | Need: columns of $A$ = rows of $B$ |
| Thinking $AB = 0$ means $A=0$ or $B=0$ | **False!** Non-zero matrices can multiply to zero |
| Applying operations to columns | Elementary operations are for **ROWS ONLY** |
| Using wrong row as reference | Can accidentally turn a zero back into non-zero |
| Counting rank before REF is complete | Must fully reduce to REF first |

---

## Process for Solving Linear Systems

**Professor's Step-by-Step Method:**
1. Write the system as an **augmented matrix** $[A|b]$
2. Apply row operations to reach **REF** (or RREF)
3. **Check for consistency:** Compare rank($A$) vs rank($[A|b]$)
4. **Identify variable types:**
   - If rank = number of unknowns → **unique solution**
   - If rank < number of unknowns → **infinite solutions** (assign parameters to free variables)
5. **Back-substitution:** Solve starting from the bottom row

---

## About GNU Octave

**Professor's Introduction:**
> Octave is a **free**, MATLAB-compatible tool for linear algebra. It's like a scientific calculator designed specifically for grids of numbers instead of single values.

**Why use it:**
- Automation is much faster and more accurate for large matrices ($1000 \times 1000$+) common in data science
- Commands are case-sensitive
- Forgetting semicolons to separate rows creates row vectors instead of matrices

---

# PART C: OCTAVE COMMAND REFERENCE

```octave
% ============ MATRIX CREATION ============
A = [1 2 3; 4 5 6]      % Define matrix (semicolons separate rows)
zeros(m, n)              % Create m×n matrix of zeros
eye(k)                   % Create k×k identity matrix
[r, c] = size(A)         % Get dimensions (rows in r, columns in c)

% ============ MATRIX OPERATIONS ============
A + B                    % Matrix addition
4 * A                    % Scalar multiplication
A * B                    % Matrix multiplication
A'                       % Transpose of A

% ============ ANALYSIS COMMANDS ============
rref(A)                  % Reduced Row Echelon Form
rank(A)                  % Find rank
det(A)                   % Calculate determinant
inv(A)                   % Find inverse (error if singular)
issymmetric(A)           % Returns 1 if symmetric, 0 if not

% ============ VISUALIZATION ============
plot(x, y)               % Generate 2D plot
```

**Cautions:**
- `inv(A)` will error if matrix is singular (determinant = 0)
- Commands are **case-sensitive**
- Missing semicolons between rows creates row vector, not matrix

---

# PART D: PRACTICE PROBLEM TYPES

| Topic | Example Problem |
|-------|-----------------|
| **Multiplication Compatibility** | Given $A$ ($3 \times 3$) and $B$ ($3 \times 4$), is $AB$ defined? Is $BA$ defined? |
| **Computing Entries** | Find $c_{23}$ from the product of two specific matrices |
| **REF Identification** | Determine if a given matrix is in REF |
| **Rank Calculation** | Reduce matrix to REF and count non-zero rows |
| **System Consistency** | Determine if a system has 0, 1, or infinite solutions |
| **Free Variables** | Express solution in terms of parameter $t$ |

---

**End of Session 1 Notes**
