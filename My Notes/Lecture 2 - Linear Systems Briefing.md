# Lecture 0b: Linear Systems and Matrix Rank
## Comprehensive Briefing Document

---

# EXECUTIVE SUMMARY

## Critical Takeaways

1. **Row Echelon Form (REF)** is the intermediate step; **Reduced Row Echelon Form (RREF)** is unique and reveals all system information
2. **Rank** = number of non-zero rows in REF = number of independent equations
3. **Consistency Rule:** A system has solutions iff rank($A$) = rank($[A|b]$)
4. **Solution Types:**
   - Unique: rank = number of unknowns
   - Infinite: rank < number of unknowns (free variables exist)
   - None: rank($A$) < rank($[A|b]$) (inconsistency detected)

## Topics Covered
- Row Echelon Form (REF) and Reduced Row Echelon Form (RREF)
- Matrix Rank definition and computation
- Solving linear systems using Gaussian elimination
- Classifying solutions: unique, infinite, or no solution
- Pivot variables vs. free variables

---

# PART 1: ROW ECHELON FORM (REF)

## 1.1 Definition of Row Echelon Form

### Definition
> A matrix is in **Row Echelon Form (REF)** if it satisfies ALL of these conditions:

| # | Condition | Meaning |
|---|-----------|---------|
| 1 | Zero rows at bottom | All rows of entirely zeros are below all non-zero rows |
| 2 | Leading entries staircase | The first non-zero entry in each row (the **leading entry**) is to the RIGHT of the leading entry in the row above |
| 3 | Zeros below leading entries | All entries in a column below a leading entry are **zero** |

### Visual Understanding
A matrix in REF looks like a "staircase" pattern:
$$
\begin{bmatrix} 
\boxed{*} & * & * & * & * \\
0 & \boxed{*} & * & * & * \\
0 & 0 & 0 & \boxed{*} & * \\
0 & 0 & 0 & 0 & 0
\end{bmatrix}
$$
- $\boxed{*}$ = leading entry (first non-zero in row)
- Each leading entry is to the RIGHT of the one above
- Zeros everywhere below leading entries
- Zero row(s) at bottom

### Examples

**✓ Valid REF:**
$$
\begin{bmatrix} 
2 & 3 & 1 & 5 \\
0 & 1 & 4 & 2 \\
0 & 0 & 3 & 1 \\
0 & 0 & 0 & 0
\end{bmatrix}
$$

**✗ NOT in REF:**
$$
\begin{bmatrix} 
2 & 3 & 1 \\
0 & 1 & 4 \\
0 & 2 & 5
\end{bmatrix}
$$
(The entry at position (3,2) should be zero — it's below a leading entry)

**✗ NOT in REF:**
$$
\begin{bmatrix} 
0 & 0 & 0 \\
1 & 2 & 3 \\
0 & 4 & 5
\end{bmatrix}
$$
(Zero row is NOT at the bottom)

---

## 1.2 What is a Leading Entry?

### Definition
> The **leading entry** (also called **pivot**) is the **first non-zero entry** in a row, reading from left to right.

### Example
$$
\begin{bmatrix} 
0 & \boxed{3} & 1 & 5 \\
0 & 0 & \boxed{2} & 4 \\
0 & 0 & 0 & \boxed{7}
\end{bmatrix}
$$
- Row 1: Leading entry is 3 (column 2)
- Row 2: Leading entry is 2 (column 3)
- Row 3: Leading entry is 7 (column 4)

---

## 1.3 Important Fact About REF

> **REF is NOT unique.** Different sequences of row operations can produce different REF forms for the same matrix.

Example: The same matrix could reduce to:
$$
\begin{bmatrix} 2 & 4 \\ 0 & 3 \end{bmatrix} \quad \text{or} \quad \begin{bmatrix} 1 & 2 \\ 0 & 1 \end{bmatrix}
$$
Both are valid REF forms of the same original matrix.

---

# PART 2: REDUCED ROW ECHELON FORM (RREF)

## 2.1 Definition of RREF

### Definition
> A matrix is in **Reduced Row Echelon Form (RREF)** if it is in REF **AND** satisfies these additional conditions:

| # | Additional Condition | Meaning |
|---|---------------------|---------|
| 4 | Leading entries are 1 | Every leading entry equals **1** |
| 5 | Leading 1 is alone in column | Each leading 1 is the **ONLY non-zero entry** in its entire column |

### Visual Understanding
$$
\begin{bmatrix} 
\boxed{1} & 0 & * & 0 & * \\
0 & \boxed{1} & * & 0 & * \\
0 & 0 & 0 & \boxed{1} & * \\
0 & 0 & 0 & 0 & 0
\end{bmatrix}
$$
- All leading entries are 1
- Each column with a leading 1 has zeros everywhere else
- The $*$ entries can be any values

### Example of RREF
$$
\begin{bmatrix} 
1 & 0 & 0 & 2 \\
0 & 1 & 0 & 3 \\
0 & 0 & 1 & 1 \\
0 & 0 & 0 & 0
\end{bmatrix}
$$

### Key Fact
> **RREF is UNIQUE.** For any given matrix, there is exactly ONE RREF form.

This is why RREF is preferred for solving systems — the solution can be read directly.

---

## 2.2 Comparison: REF vs RREF

| Property | REF | RREF |
|----------|-----|------|
| Zero rows at bottom | ✓ | ✓ |
| Staircase pattern | ✓ | ✓ |
| Zeros below leading entries | ✓ | ✓ |
| Leading entries are 1 | Not required | ✓ Required |
| Zeros ABOVE leading entries | Not required | ✓ Required |
| Uniqueness | Not unique | **UNIQUE** |

---

# PART 3: CONVERTING TO REF/RREF (GAUSSIAN ELIMINATION)

## 3.1 Algorithm for REF

### Step-by-Step Process

**Goal:** Transform matrix into REF using elementary row operations.

```
1. Start with column 1
2. Find a row with non-zero entry in this column (pivot row)
3. If needed, swap this row to the top (among remaining rows)
4. Use row addition to make all entries BELOW the pivot = 0
5. Move to next column, repeat for remaining rows
6. Continue until all columns processed
```

### Detailed Example

**Original matrix:**
$$
A = \begin{bmatrix} 
0 & 1 & 2 \\
1 & 2 & 3 \\
2 & 3 & 4
\end{bmatrix}
$$

**Step 1:** Column 1 has a zero in row 1. Swap $R_1 \leftrightarrow R_2$:
$$
\begin{bmatrix} 
1 & 2 & 3 \\
0 & 1 & 2 \\
2 & 3 & 4
\end{bmatrix}
$$

**Step 2:** Eliminate below pivot (entry at (1,1)). Apply $R_3 \rightarrow R_3 - 2R_1$:
$$
\begin{bmatrix} 
1 & 2 & 3 \\
0 & 1 & 2 \\
0 & -1 & -2
\end{bmatrix}
$$

**Step 3:** Move to column 2, row 2. Pivot is 1. Eliminate below. Apply $R_3 \rightarrow R_3 + R_2$:
$$
\begin{bmatrix} 
1 & 2 & 3 \\
0 & 1 & 2 \\
0 & 0 & 0
\end{bmatrix}
$$

**Result:** Matrix is now in **REF**.

---

## 3.2 Algorithm for RREF (Gauss-Jordan Elimination)

### Additional Steps After REF

```
6. Starting from the rightmost pivot, work upward
7. Make each leading entry = 1 (divide row by leading entry)
8. Use row addition to make all entries ABOVE each pivot = 0
```

### Continuing the Example

From REF:
$$
\begin{bmatrix} 
1 & 2 & 3 \\
0 & 1 & 2 \\
0 & 0 & 0
\end{bmatrix}
$$

**Step 4:** Eliminate above pivot in column 2. Apply $R_1 \rightarrow R_1 - 2R_2$:
$$
\begin{bmatrix} 
1 & 0 & -1 \\
0 & 1 & 2 \\
0 & 0 & 0
\end{bmatrix}
$$

**Result:** Matrix is now in **RREF**.

---

## 3.3 Common Mistakes in Row Reduction

| Mistake | Why It's Wrong |
|---------|----------------|
| Operating on columns | Elementary operations are for **ROWS ONLY** |
| Forgetting to swap | If pivot is zero, must swap before continuing |
| Wrong multiplier | Calculate carefully: to eliminate $a_{ij}$, use $-\frac{a_{ij}}{a_{kj}}$ times pivot row |
| Undoing previous work | When eliminating, use the correct row to avoid changing already-fixed entries |
| Not completing all steps | Must process all columns for proper REF |

---

# PART 4: MATRIX RANK

## 4.1 Definition of Rank

### Definition
> The **rank** of a matrix is the **number of non-zero rows** in its Row Echelon Form.

### Notation
$$\text{rank}(A) \quad \text{or} \quad r(A)$$

### Computing Rank

**Step-by-step:**
1. Convert matrix to REF (or RREF)
2. Count rows that have at least one non-zero entry
3. This count is the rank

### Example
$$
A = \begin{bmatrix} 
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{bmatrix}
\xrightarrow{\text{REF}}
\begin{bmatrix} 
1 & 2 & 3 \\
0 & -3 & -6 \\
0 & 0 & 0
\end{bmatrix}
$$

Non-zero rows: 2

Therefore: $\text{rank}(A) = 2$

---

## 4.2 Key Properties of Rank

### Invariance Property
> **Rank is invariant under elementary row operations.**
> 
> No matter which sequence of row operations you use, you'll get the same rank.

### Maximum Possible Rank
For an $m \times n$ matrix:
$$\text{rank}(A) \leq \min(m, n)$$

The rank cannot exceed the number of rows OR the number of columns.

### Full Rank
> A matrix has **full row rank** if rank = $m$ (number of rows)
> 
> A matrix has **full column rank** if rank = $n$ (number of columns)
>
> A square matrix has **full rank** if rank = $n$ (the matrix is invertible)

---

## 4.3 Professor's Analogy for Rank

> Finding the rank of a matrix is like **distilling a story down to its unique plot points**.
> 
> Even if you reword the sentences (apply row operations), the number of truly unique, independent ideas (non-zero rows) remains the same.

This means:
- Some rows might be "combinations" of other rows
- Rank tells you how many "truly independent" pieces of information exist
- Redundant information gets eliminated (becomes zero rows)

---

## 4.4 Common Mistakes with Rank

| Mistake | Correction |
|---------|------------|
| Counting before full REF | Must complete row reduction first |
| Counting rows with any numbers | Only count **non-zero** rows |
| Confusing with dimension | Rank is about independent rows, not matrix size |
| Ignoring zero rows | Zero rows don't count toward rank |

---

# PART 5: SOLVING LINEAR SYSTEMS

## 5.1 Linear System Basics

### Definition
> A **linear system** is a set of $m$ linear equations with $n$ unknowns $(x_1, x_2, \ldots, x_n)$.

### Example
$$
\begin{cases}
x_1 + 2x_2 + 3x_3 = 9 \\
4x_1 + 5x_2 + 6x_3 = 24 \\
7x_1 + 8x_2 + 9x_3 = 39
\end{cases}
$$

### Matrix Form
$$Ax = b$$
where:
- $A$ = coefficient matrix
- $x$ = unknown vector
- $b$ = constants vector

---

## 5.2 Augmented Matrix

### Definition
> The **augmented matrix** $[A|b]$ combines the coefficient matrix $A$ and constants $b$ into one matrix, separated by a vertical line.

### Example
For the system above:
$$
[A|b] = \left[\begin{array}{ccc|c}
1 & 2 & 3 & 9 \\
4 & 5 & 6 & 24 \\
7 & 8 & 9 & 39
\end{array}\right]
$$

### Why Use It?
- Compact notation for row operations
- Apply same operations to both $A$ and $b$ simultaneously
- Reveals inconsistencies directly

---

## 5.3 Homogeneous vs Non-Homogeneous

| Type | Definition | Form | Always Has Solution? |
|------|------------|------|---------------------|
| **Homogeneous** | All constants are zero | $Ax = 0$ | Yes (at least $x = 0$) |
| **Non-Homogeneous** | At least one constant non-zero | $Ax = b$ | Not always |

---

## 5.4 The Fundamental Consistency Rule

### Theorem (Rouché-Capelli)
> A linear system is **consistent** (has at least one solution) **if and only if**:
> $$\text{rank}(A) = \text{rank}([A|b])$$

### What This Means
- If ranks are equal: solutions exist
- If rank($[A|b]$) > rank($A$): **no solution** (inconsistent)

### How Inconsistency Appears
An inconsistent system will have a row in RREF that looks like:
$$
[0 \quad 0 \quad 0 \quad \cdots \quad 0 \quad | \quad c] \quad \text{where } c \neq 0
$$

This represents the equation $0 = c$, which is impossible!

---

## 5.5 Classifying Solutions

### Complete Classification Table

| Condition | Result | Description |
|-----------|--------|-------------|
| rank($A$) < rank($[A\|b]$) | **No solution** | System is inconsistent |
| rank($A$) = rank($[A\|b]$) = $n$ | **Unique solution** | Exactly one solution |
| rank($A$) = rank($[A\|b]$) < $n$ | **Infinite solutions** | Free variables exist |

Where $n$ = number of unknowns.

### Number of Free Variables
$$\text{Free variables} = n - \text{rank}(A)$$

---

## 5.6 Pivot Variables vs Free Variables

### Definitions
> **Pivot variable:** Corresponds to a column that contains a leading entry (pivot)
> 
> **Free variable:** Corresponds to a column that does NOT contain a leading entry

### Example
Consider this RREF augmented matrix:
$$
\left[\begin{array}{cccc|c}
1 & 2 & 0 & 3 & 5 \\
0 & 0 & 1 & 4 & 2 \\
0 & 0 & 0 & 0 & 0
\end{array}\right]
$$

**Analysis:**
- Column 1: Has leading 1 → $x_1$ is **pivot variable**
- Column 2: No leading entry → $x_2$ is **free variable**
- Column 3: Has leading 1 → $x_3$ is **pivot variable**
- Column 4: No leading entry → $x_4$ is **free variable**

**Solution with parameters:**
Let $x_2 = s$ and $x_4 = t$ (free variables are parameters)

From row 2: $x_3 + 4t = 2 \Rightarrow x_3 = 2 - 4t$
From row 1: $x_1 + 2s + 3t = 5 \Rightarrow x_1 = 5 - 2s - 3t$

**General solution:**
$$
\begin{pmatrix} x_1 \\ x_2 \\ x_3 \\ x_4 \end{pmatrix} = 
\begin{pmatrix} 5 - 2s - 3t \\ s \\ 2 - 4t \\ t \end{pmatrix}
$$

---

## 5.7 Complete Solving Process

### Algorithm

```
1. Write system as augmented matrix [A|b]
2. Apply row operations to get RREF
3. Check consistency:
   - Look for rows of form [0 0 ... 0 | c] with c ≠ 0
   - If found: NO SOLUTION (stop here)
4. Identify pivot and free variables
5. If no free variables: UNIQUE SOLUTION
   - Read values directly from RREF
6. If free variables exist: INFINITE SOLUTIONS
   - Assign parameters to free variables
   - Express pivot variables in terms of parameters
```

---

## 5.8 Worked Examples

### Example 1: Unique Solution

**System:**
$$
\begin{cases}
x + y + z = 6 \\
2x + y + z = 8 \\
x + 2y + z = 9
\end{cases}
$$

**Augmented matrix:**
$$
\left[\begin{array}{ccc|c}
1 & 1 & 1 & 6 \\
2 & 1 & 1 & 8 \\
1 & 2 & 1 & 9
\end{array}\right]
$$

**Row operations:**
$R_2 \rightarrow R_2 - 2R_1$, $R_3 \rightarrow R_3 - R_1$:
$$
\left[\begin{array}{ccc|c}
1 & 1 & 1 & 6 \\
0 & -1 & -1 & -4 \\
0 & 1 & 0 & 3
\end{array}\right]
$$

$R_3 \rightarrow R_3 + R_2$:
$$
\left[\begin{array}{ccc|c}
1 & 1 & 1 & 6 \\
0 & -1 & -1 & -4 \\
0 & 0 & -1 & -1
\end{array}\right]
$$

**To RREF:** (divide rows, eliminate above)
$$
\left[\begin{array}{ccc|c}
1 & 0 & 0 & 2 \\
0 & 1 & 0 & 3 \\
0 & 0 & 1 & 1
\end{array}\right]
$$

**Solution:** $x = 2, y = 3, z = 1$ ✓ **Unique**

---

### Example 2: No Solution

**System:**
$$
\begin{cases}
x + y = 3 \\
x + y = 5
\end{cases}
$$

**Augmented matrix:**
$$
\left[\begin{array}{cc|c}
1 & 1 & 3 \\
1 & 1 & 5
\end{array}\right]
$$

**Row operation:** $R_2 \rightarrow R_2 - R_1$:
$$
\left[\begin{array}{cc|c}
1 & 1 & 3 \\
0 & 0 & 2
\end{array}\right]
$$

**Analysis:**
- Row 2 says: $0x + 0y = 2$, i.e., $0 = 2$ ✗
- rank($A$) = 1, rank($[A|b]$) = 2
- Ranks not equal!

**Result:** No solution (inconsistent)

---

### Example 3: Infinite Solutions

**System:**
$$
\begin{cases}
x + 2y + z = 4 \\
2x + 4y + 2z = 8
\end{cases}
$$

**Augmented matrix:**
$$
\left[\begin{array}{ccc|c}
1 & 2 & 1 & 4 \\
2 & 4 & 2 & 8
\end{array}\right]
$$

**Row operation:** $R_2 \rightarrow R_2 - 2R_1$:
$$
\left[\begin{array}{ccc|c}
1 & 2 & 1 & 4 \\
0 & 0 & 0 & 0
\end{array}\right]
$$

**Analysis:**
- rank($A$) = 1, rank($[A|b]$) = 1 ✓ (consistent)
- But 3 unknowns, rank = 1
- Free variables = 3 - 1 = 2 (both $y$ and $z$)

**General solution:**
Let $y = s$, $z = t$:
$$x = 4 - 2s - t$$

Solution: $(4 - 2s - t, s, t)$ for any real $s, t$

---

# PART 6: OCTAVE IMPLEMENTATION

```octave
% ========== DEFINE AUGMENTED MATRIX ==========
A = [1 2 3; 4 5 6; 7 8 9];
b = [6; 15; 24];
Aug = [A b];    % Create augmented matrix

% ========== ROW ECHELON FORM ==========
% Note: Octave doesn't have a direct REF command
% But rref() gives the RREF which is sufficient

% ========== REDUCED ROW ECHELON FORM ==========
rref(Aug)       % Returns RREF of augmented matrix

% ========== RANK ==========
rank(A)         % Rank of coefficient matrix
rank(Aug)       % Rank of augmented matrix

% Compare to check consistency:
if rank(A) == rank(Aug)
    disp('System is consistent')
else
    disp('System is inconsistent - no solution')
end

% ========== SOLVING SYSTEMS ==========
% For consistent systems with unique solution:
x = A \ b;      % Solves Ax = b (if unique solution exists)

% ========== VERIFY SOLUTION ==========
A * x           % Should equal b
```

---

# PART 7: PRACTICE PROBLEMS

## Problem 1: Identify REF

Which matrices are in REF?

a) $\begin{bmatrix} 1 & 2 & 3 \\ 0 & 1 & 4 \\ 0 & 0 & 5 \end{bmatrix}$

b) $\begin{bmatrix} 1 & 2 \\ 0 & 0 \\ 0 & 3 \end{bmatrix}$

c) $\begin{bmatrix} 0 & 0 & 0 \\ 0 & 1 & 2 \\ 0 & 0 & 1 \end{bmatrix}$

<details>
<summary>Solution</summary>

a) ✓ **Yes** - Proper staircase, zeros below pivots

b) ✗ **No** - Zero row not at bottom

c) ✗ **No** - Zero row not at bottom
</details>

---

## Problem 2: Compute Rank

Find the rank of:
$$A = \begin{bmatrix} 1 & 2 & 3 \\ 2 & 4 & 6 \\ 1 & 1 & 1 \end{bmatrix}$$

<details>
<summary>Solution</summary>

$R_2 \rightarrow R_2 - 2R_1$, $R_3 \rightarrow R_3 - R_1$:
$$\begin{bmatrix} 1 & 2 & 3 \\ 0 & 0 & 0 \\ 0 & -1 & -2 \end{bmatrix}$$

$R_2 \leftrightarrow R_3$:
$$\begin{bmatrix} 1 & 2 & 3 \\ 0 & -1 & -2 \\ 0 & 0 & 0 \end{bmatrix}$$

Non-zero rows: 2

**rank($A$) = 2**
</details>

---

## Problem 3: Classify Solution Type

For each system, determine: unique, infinite, or no solution.

a) $\begin{cases} x + y = 2 \\ 2x + 2y = 4 \end{cases}$

b) $\begin{cases} x + y = 2 \\ x - y = 0 \end{cases}$

c) $\begin{cases} x + y = 2 \\ x + y = 3 \end{cases}$

<details>
<summary>Solution</summary>

a) Reduce: $\begin{bmatrix} 1 & 1 & 2 \\ 0 & 0 & 0 \end{bmatrix}$
   - rank($A$) = 1, rank($[A|b]$) = 1, unknowns = 2
   - **Infinite solutions** (free variable $y$)

b) Reduce: $\begin{bmatrix} 1 & 0 & 1 \\ 0 & 1 & 1 \end{bmatrix}$
   - rank($A$) = 2, rank($[A|b]$) = 2, unknowns = 2
   - **Unique solution** ($x = 1, y = 1$)

c) Reduce: $\begin{bmatrix} 1 & 1 & 2 \\ 0 & 0 & 1 \end{bmatrix}$
   - Row 2: $0 = 1$ — contradiction!
   - rank($A$) = 1, rank($[A|b]$) = 2
   - **No solution**
</details>

---

## Problem 4: Find General Solution

Solve:
$$\begin{cases} x + 2y + 3z = 4 \\ 2x + 4y + 6z = 8 \end{cases}$$

<details>
<summary>Solution</summary>

Augmented matrix:
$$\left[\begin{array}{ccc|c} 1 & 2 & 3 & 4 \\ 2 & 4 & 6 & 8 \end{array}\right]$$

$R_2 \rightarrow R_2 - 2R_1$:
$$\left[\begin{array}{ccc|c} 1 & 2 & 3 & 4 \\ 0 & 0 & 0 & 0 \end{array}\right]$$

- Pivot: column 1 ($x$)
- Free: columns 2, 3 ($y$, $z$)

Let $y = s$, $z = t$:
$$x = 4 - 2s - 3t$$

**General solution:** $(4 - 2s - 3t, s, t)$ for all $s, t \in \mathbb{R}$
</details>

---

## Problem 5: Back-Substitution

Given this RREF, find the solution:
$$\left[\begin{array}{ccc|c} 1 & 0 & 2 & 7 \\ 0 & 1 & -1 & 3 \\ 0 & 0 & 0 & 0 \end{array}\right]$$

<details>
<summary>Solution</summary>

- $x_1$ = pivot, $x_2$ = pivot, $x_3$ = **free variable**

Let $x_3 = t$:
- From row 2: $x_2 - t = 3 \Rightarrow x_2 = 3 + t$
- From row 1: $x_1 + 2t = 7 \Rightarrow x_1 = 7 - 2t$

**Solution:** $(7 - 2t, 3 + t, t)$ for any $t \in \mathbb{R}$
</details>

---

# KEY TAKEAWAYS

| Concept | Key Point |
|---------|-----------|
| REF | Staircase pattern; not unique |
| RREF | Leading 1s, alone in columns; **unique** |
| Rank | # of non-zero rows in REF; **invariant** |
| Consistency | rank($A$) = rank($[A\|b]$) for solutions to exist |
| Unique Solution | Consistent AND rank = # of unknowns |
| Infinite Solutions | Consistent AND rank < # of unknowns |
| No Solution | rank($A$) < rank($[A\|b]$), i.e., $0 = c$ appears |
| Free Variables | Columns without pivots become parameters |

---

**Previous:** Lecture 0a - Matrix Fundamentals  
**Next:** Lecture 0c - Determinants, Inverses, and Eigenvalues
