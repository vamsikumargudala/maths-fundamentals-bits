# Zero Level Mathematical Foundation

## Purpose of This Document
You need to complete **Lecture 0a, 0b, and 0c** before the first Mathematics for ML lecture. This guide synthesizes all content from the professor's bridge sessions and lecture materials.

---

## The Three Pillars You Must Master

### Pillar 1: Matrix Algebra (Lecture 1)
**Core Competency:** Understand matrices as data structures and perform operations

| Topic | Why It Matters for AI/ML |
|-------|-------------------------|
| Matrix notation ($m \times n$) | All data (images, audio, text) is stored as matrices |
| Matrix multiplication | Neural network forward passes |
| Transposition | Gradient computations, covariance matrices |
| Special matrices (symmetric, sparse) | Efficiency in NLP, social networks, PCA |

### Pillar 2: Linear Systems (Lecture 2)
**Core Competency:** Solve systems of equations and determine solution existence

| Topic | Why It Matters for AI/ML |
|-------|-------------------------|
| Row Echelon Form (REF/RREF) | Foundation for matrix decomposition |
| Matrix Rank | Determines if systems are solvable |
| Consistency rules | Understanding when optimization has solutions |
| Free vs. pivot variables | Parameter spaces in models |

### Pillar 3: Matrix Properties (Lecture 3)
**Core Competency:** Compute determinants, inverses, and eigenvalues

| Topic | Why It Matters for AI/ML |
|-------|-------------------------|
| Determinant | Measures matrix "volume scaling", invertibility check |
| Matrix Inverse | Solving normal equations, closed-form solutions |
| Eigenvalues/Eigenvectors | PCA, spectral clustering, stability analysis |

---

## Quick Self-Assessment Checklist

**Lecture 1 - Matrix Fundamentals:**
- [ ] Define what a matrix is and identify its dimensions
- [ ] Perform matrix addition, scalar multiplication
- [ ] Compute matrix products (check dimension compatibility first)
- [ ] Compute transpose of a matrix
- [ ] Identify symmetric, skew-symmetric, triangular, diagonal, sparse matrices
- [ ] Apply the three elementary row operations

**Lecture 2 - Linear Systems:**
- [ ] Convert a system of linear equations to augmented matrix form
- [ ] Reduce a matrix to Row Echelon Form (REF)
- [ ] Reduce a matrix to Reduced Row Echelon Form (RREF)
- [ ] Calculate the rank of a matrix
- [ ] Determine if a system is consistent/inconsistent
- [ ] Identify unique solution vs. infinite solutions vs. no solution
- [ ] Use back-substitution to find solutions

**Lecture 3 - Determinants & Eigenvalues:**
- [ ] Calculate 2×2 and 3×3 determinants
- [ ] Use determinant properties (row operations, triangular matrices)
- [ ] Find the inverse of a matrix (if it exists)
- [ ] Determine when a matrix is invertible (non-singular)
- [ ] Find eigenvalues by solving characteristic equation
- [ ] Find eigenvectors for given eigenvalues

---

## Document Map

| Document | Content | Priority |
|----------|---------|----------|
| [Lecture 1 Briefing](Lecture%200a%20-%20Matrix%20Fundamentals%20Briefing.md) | Matrix notation, operations, special types, row operations | 🔴 HIGH |
| [Lecture 2 Briefing](Lecture%200b%20-%20Linear%20Systems%20Briefing.md) | REF, RREF, Rank, solving linear systems | 🔴 HIGH |
| [Lecture 3 Briefing](Lecture%200c%20-%20Determinants%20and%20Eigenvalues%20Briefing.md) | Determinants, inverses, eigenvalues | 🔴 HIGH |

---

## Recommended Study Order

```
Day 1: Lecture 1 (2-3 hours)
├── Matrix definitions and notation
├── Matrix operations (add, multiply, transpose)
├── Special matrix types
└── Elementary row operations

Day 2: Lecture 2 (2-3 hours)
├── Row Echelon Form
├── Reduced Row Echelon Form
├── Matrix Rank
└── Solving linear systems

Day 3: Lecture 3 (2-3 hours)
├── Determinants (2×2, 3×3, properties)
├── Matrix Inverse
└── Eigenvalues and Eigenvectors

Day 4: Practice Problems + Review
├── Work through Practice Problems I
├── Work through Practice Problems II
└── Use Octave to verify calculations
```

---

## Key Formulas to Memorize

### Matrix Multiplication Dimension Rule
$$A_{m \times n} \cdot B_{n \times p} = C_{m \times p}$$

### Consistency Condition
$$\text{System consistent} \iff \text{rank}(A) = \text{rank}([A|b])$$

### 2×2 Determinant
$$\det\begin{pmatrix} a & b \\ c & d \end{pmatrix} = ad - bc$$

### 2×2 Inverse
$$A^{-1} = \frac{1}{\det(A)} \begin{pmatrix} d & -b \\ -c & a \end{pmatrix}$$

### Characteristic Equation (for eigenvalues)
$$\det(A - \lambda I) = 0$$

---

## Common Pitfalls to Avoid

| Mistake | Correction |
|---------|------------|
| Assuming $AB = BA$ | Matrix multiplication is **NOT commutative** |
| Adding mismatched dimensions | Check sizes before adding |
| Multiplying incompatible matrices | Columns of A must equal rows of B |
| Thinking $AB = 0$ means $A=0$ or $B=0$ | False! Non-zero matrices can multiply to zero |
| Applying row operations to columns | **Rows only!** |
| Counting rank before full REF | Complete reduction first |
| Forgetting to check determinant before inverse | $\det(A) = 0$ means no inverse |

