# Practice Problems Guide
## Zero Level Mathematical Foundation - M.Tech AI/ML

---

# OVERVIEW

This document provides a structured approach to the practice problems from:
- **Practice Problems I** - Covers Lecture 0a & 0b topics
- **Practice Problems II** - Covers Lecture 0b & 0c topics

**Source Files:**
- `Practice_Problems_I_Zero_Level_Mathematical_Foundation.pdf`
- `Practice_Problems_II_Zero_Level_Mathematical_Foundation.pdf`

---

# PART 1: MATRIX FUNDAMENTALS (Lecture 0a)

## Problem Type 1: Matrix Dimensions and Notation

### Approach
1. Count rows (horizontal) first
2. Count columns (vertical) second
3. Express as $m \times n$

### Practice Template
| Matrix | Rows | Columns | Dimension |
|--------|------|---------|-----------|
| Given matrix 1 | ? | ? | ? × ? |
| Given matrix 2 | ? | ? | ? × ? |

---

## Problem Type 2: Matrix Multiplication Compatibility

### Approach
1. Write dimensions of both matrices: $A_{m \times n}$ and $B_{p \times q}$
2. Check if inner dimensions match: $n = p$?
3. If yes, result is $m \times q$
4. If no, multiplication is undefined

### Quick Check Formula
$$A_{m \times \boxed{n}} \cdot B_{\boxed{n} \times q} = C_{m \times q}$$

### Practice Template
| $A$ size | $B$ size | $AB$ defined? | $AB$ size | $BA$ defined? | $BA$ size |
|----------|----------|---------------|-----------|---------------|-----------|
| $3 \times 3$ | $3 \times 4$ | Yes | $3 \times 4$ | No | - |
| $2 \times 5$ | $5 \times 3$ | ? | ? | ? | ? |
| $4 \times 2$ | $3 \times 4$ | ? | ? | ? | ? |

---

## Problem Type 3: Computing Matrix Products

### Approach
1. Verify dimensions are compatible
2. For entry $c_{jk}$: dot product of row $j$ of $A$ with column $k$ of $B$
3. $c_{jk} = \sum_{i} a_{ji} \cdot b_{ik}$

### Worked Example
$$A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}, \quad B = \begin{bmatrix} 5 & 6 \\ 7 & 8 \end{bmatrix}$$

**Find $AB$:**
- $c_{11} = (1)(5) + (2)(7) = 5 + 14 = 19$
- $c_{12} = (1)(6) + (2)(8) = 6 + 16 = 22$
- $c_{21} = (3)(5) + (4)(7) = 15 + 28 = 43$
- $c_{22} = (3)(6) + (4)(8) = 18 + 32 = 50$

$$AB = \begin{bmatrix} 19 & 22 \\ 43 & 50 \end{bmatrix}$$

---

## Problem Type 4: Transpose Operations

### Approach
1. Rows become columns
2. $(A^\top)_{ij} = A_{ji}$
3. For products: $(AB)^\top = B^\top A^\top$ (reversal!)

### Practice Template
Given $A = \begin{bmatrix} a & b & c \\ d & e & f \end{bmatrix}$, find $A^\top$:

$$A^\top = \begin{bmatrix} a & d \\ b & e \\ c & f \end{bmatrix}$$

---

## Problem Type 5: Special Matrix Identification

### Checklist
| Type | Check |
|------|-------|
| **Symmetric** | Is $A = A^\top$? |
| **Skew-symmetric** | Is $A = -A^\top$? Are diagonals 0? |
| **Upper triangular** | Are all entries below diagonal = 0? |
| **Lower triangular** | Are all entries above diagonal = 0? |
| **Diagonal** | Are all off-diagonal entries = 0? |

---

# PART 2: ROW OPERATIONS & REF/RREF (Lecture 0a-0b)

## Problem Type 6: Elementary Row Operations

### The Three Operations
1. **Swap**: $R_i \leftrightarrow R_j$
2. **Scale**: $R_i \rightarrow cR_i$ (where $c \neq 0$)
3. **Add**: $R_i \rightarrow R_i + cR_j$

### Practice Template
Apply $R_2 \rightarrow R_2 - 3R_1$ to:
$$\begin{bmatrix} 1 & 2 & 3 \\ 3 & 5 & 7 \end{bmatrix}$$

**Solution:**
- New $R_2 = [3, 5, 7] - 3[1, 2, 3] = [0, -1, -2]$
- Result: $\begin{bmatrix} 1 & 2 & 3 \\ 0 & -1 & -2 \end{bmatrix}$

---

## Problem Type 7: Converting to REF

### REF Criteria
1. Zero rows at bottom ✓
2. Leading entries staircase right ✓
3. Zeros below all leading entries ✓

### Algorithm
```
For each column (left to right):
  1. Find pivot (first non-zero in column, from current row down)
  2. Swap to bring pivot to current row if needed
  3. Use row addition to zero out all entries below pivot
  4. Move to next row and column
```

---

## Problem Type 8: Converting to RREF

### Additional RREF Criteria
4. All leading entries = 1 ✓
5. Leading 1s are ONLY non-zero in their column ✓

### After REF, continue:
```
For each pivot (right to left):
  1. Divide row to make leading entry = 1
  2. Use row addition to zero out all entries ABOVE pivot
```

---

## Problem Type 9: Finding Rank

### Definition
Rank = number of non-zero rows in REF

### Approach
1. Convert to REF (or RREF)
2. Count rows with at least one non-zero entry
3. That count is the rank

### Practice Template
| Matrix | REF form | Non-zero rows | Rank |
|--------|----------|---------------|------|
| Original | After reduction | Count | ? |

---

# PART 3: LINEAR SYSTEMS (Lecture 0b)

## Problem Type 10: Writing Augmented Matrix

### Approach
Given system:
$$\begin{cases} ax + by = e \\ cx + dy = f \end{cases}$$

Augmented matrix:
$$\left[\begin{array}{cc|c} a & b & e \\ c & d & f \end{array}\right]$$

---

## Problem Type 11: Determining Consistency

### Decision Tree
```
1. Reduce augmented matrix to REF
2. Look for row: [0 0 ... 0 | c] where c ≠ 0
   - If found: NO SOLUTION (inconsistent)
   - If not found: Continue...
3. Compare rank(A) with rank([A|b])
   - If equal: CONSISTENT (solutions exist)
```

---

## Problem Type 12: Classifying Solutions

### After confirming consistency:
| Condition | Result |
|-----------|--------|
| rank = # of unknowns | **Unique solution** |
| rank < # of unknowns | **Infinite solutions** |

### Free variables = (# unknowns) - rank

---

## Problem Type 13: Solving with Free Variables

### Approach
1. Identify pivot columns (have leading entries)
2. Identify free columns (no leading entries)
3. Assign parameters ($t$, $s$, etc.) to free variables
4. Express pivot variables in terms of free variables
5. Write general solution

### Example
RREF: $\left[\begin{array}{ccc|c} 1 & 2 & 0 & 5 \\ 0 & 0 & 1 & 3 \end{array}\right]$

- Pivot columns: 1, 3 → $x_1$, $x_3$ are pivot variables
- Free column: 2 → $x_2$ is free variable

Let $x_2 = t$:
- From row 2: $x_3 = 3$
- From row 1: $x_1 + 2t = 5 \Rightarrow x_1 = 5 - 2t$

**Solution:** $(5-2t, t, 3)$ for any $t \in \mathbb{R}$

---

# PART 4: DETERMINANTS (Lecture 0c)

## Problem Type 14: 2×2 Determinant

### Formula
$$\det\begin{pmatrix} a & b \\ c & d \end{pmatrix} = ad - bc$$

### Practice Problems
| Matrix | Calculation | Determinant |
|--------|-------------|-------------|
| $\begin{bmatrix} 3 & 4 \\ 2 & 5 \end{bmatrix}$ | $3(5) - 4(2)$ | $7$ |
| $\begin{bmatrix} 6 & 2 \\ 3 & 1 \end{bmatrix}$ | $6(1) - 2(3)$ | $0$ (singular!) |

---

## Problem Type 15: 3×3 Determinant (Cofactor Expansion)

### Formula (expand along row 1)
$$\det(A) = a_{11}C_{11} - a_{12}C_{12} + a_{13}C_{13}$$

Where $C_{ij}$ = determinant of 2×2 matrix after removing row $i$ and column $j$

### Worked Example
$$A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 0 \end{bmatrix}$$

$$\det(A) = 1\det\begin{bmatrix} 5 & 6 \\ 8 & 0 \end{bmatrix} - 2\det\begin{bmatrix} 4 & 6 \\ 7 & 0 \end{bmatrix} + 3\det\begin{bmatrix} 4 & 5 \\ 7 & 8 \end{bmatrix}$$

$$= 1(0-48) - 2(0-42) + 3(32-35)$$
$$= -48 + 84 - 9 = 27$$

---

## Problem Type 16: Determinant Properties

### Use these shortcuts:
| Property | Application |
|----------|-------------|
| Triangular matrix | det = product of diagonal |
| Row of zeros | det = 0 |
| Two identical rows | det = 0 |
| Row swap | det changes sign |
| Row × scalar | det × scalar |

---

# PART 5: MATRIX INVERSE (Lecture 0c)

## Problem Type 17: 2×2 Inverse

### Formula
$$A^{-1} = \frac{1}{ad-bc}\begin{pmatrix} d & -b \\ -c & a \end{pmatrix}$$

### Steps
1. Compute $\det(A) = ad - bc$
2. If $\det = 0$: No inverse exists
3. Swap diagonal entries
4. Negate off-diagonal entries
5. Divide by determinant

### Practice
$$A = \begin{bmatrix} 2 & 3 \\ 1 & 4 \end{bmatrix}$$

$\det(A) = 2(4) - 3(1) = 5$

$$A^{-1} = \frac{1}{5}\begin{bmatrix} 4 & -3 \\ -1 & 2 \end{bmatrix} = \begin{bmatrix} 0.8 & -0.6 \\ -0.2 & 0.4 \end{bmatrix}$$

---

## Problem Type 18: Inverse via Gauss-Jordan

### Steps
1. Form $[A | I]$
2. Row reduce until left side is $I$
3. Right side is now $A^{-1}$

---

# PART 6: EIGENVALUES & EIGENVECTORS (Lecture 0c)

## Problem Type 19: Finding Eigenvalues

### Steps
1. Form $A - \lambda I$
2. Compute $\det(A - \lambda I)$
3. Set equal to 0 (characteristic equation)
4. Solve for $\lambda$

### 2×2 Shortcut
For $A = \begin{bmatrix} a & b \\ c & d \end{bmatrix}$:

Characteristic equation: $\lambda^2 - (a+d)\lambda + (ad-bc) = 0$

Or: $\lambda^2 - \text{trace}\cdot\lambda + \det = 0$

### Practice
$$A = \begin{bmatrix} 5 & 2 \\ 2 & 2 \end{bmatrix}$$

- trace = $5 + 2 = 7$
- det = $5(2) - 2(2) = 6$

$\lambda^2 - 7\lambda + 6 = 0$
$(\lambda - 6)(\lambda - 1) = 0$

**Eigenvalues:** $\lambda_1 = 6$, $\lambda_2 = 1$

---

## Problem Type 20: Finding Eigenvectors

### Steps
1. For each eigenvalue $\lambda_i$
2. Solve $(A - \lambda_i I)v = 0$
3. Find the null space (non-trivial solutions)

### Practice (continuing above)
For $\lambda = 6$:
$$A - 6I = \begin{bmatrix} -1 & 2 \\ 2 & -4 \end{bmatrix}$$

Row reduce: $\begin{bmatrix} 1 & -2 \\ 0 & 0 \end{bmatrix}$

$v_1 = 2v_2$, let $v_2 = 1$: **Eigenvector** = $\begin{bmatrix} 2 \\ 1 \end{bmatrix}$

---

## Problem Type 21: Verify Eigenvalue Properties

### Check
- Sum of eigenvalues = trace(A)
- Product of eigenvalues = det(A)

---

# OCTAVE VERIFICATION COMMANDS

```octave
% ===== Matrix Operations =====
A = [1 2; 3 4];
B = [5 6; 7 8];
A * B              % Matrix multiplication
A'                 % Transpose

% ===== REF/RREF and Rank =====
Aug = [1 2 3 6; 2 5 8 15; 1 3 5 10];
rref(Aug)          % RREF of augmented matrix
rank(Aug(:,1:3))   % Rank of coefficient matrix
rank(Aug)          % Rank of augmented matrix

% ===== Determinant and Inverse =====
A = [3 4; 2 5];
det(A)             % Determinant
inv(A)             % Inverse
A * inv(A)         % Should be identity

% ===== Eigenvalues =====
A = [5 2; 2 2];
eig(A)             % Eigenvalues
[V, D] = eig(A)    % V = eigenvectors, D = eigenvalues on diagonal

% Verify properties
trace(A)           % Should equal sum of eigenvalues
det(A)             % Should equal product of eigenvalues
```

---

# SELF-TEST CHECKLIST

Before January 17th, verify you can:

## Lecture 0a Topics
- [ ] Identify matrix dimensions
- [ ] Determine if multiplication is defined
- [ ] Compute matrix products entry-by-entry
- [ ] Compute transpose
- [ ] Identify special matrix types
- [ ] Apply all three row operations

## Lecture 0b Topics
- [ ] Convert matrix to REF
- [ ] Convert matrix to RREF
- [ ] Calculate rank
- [ ] Set up augmented matrix from system
- [ ] Determine if system is consistent
- [ ] Classify solution type (unique/infinite/none)
- [ ] Solve systems with free variables

## Lecture 0c Topics
- [ ] Calculate 2×2 determinant
- [ ] Calculate 3×3 determinant
- [ ] Use determinant properties
- [ ] Find 2×2 inverse
- [ ] Use Gauss-Jordan for inverse
- [ ] Find eigenvalues (2×2)
- [ ] Find eigenvectors
- [ ] Verify eigenvalue properties

---

**Good luck with your preparation!**  
**Target:** Ready for January 17th, 11 AM - 1 PM Lecture
