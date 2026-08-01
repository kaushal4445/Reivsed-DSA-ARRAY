# Set Matrix Zeroes (Better Approach)

## Problem Statement

Given a matrix, if any element is `0`, set its **entire row** and **entire column** to `0`.

### Example

**Input**

```
1 1 1 1
2 0 2 2
3 3 3 3
4 4 0 4
```

**Output**

```
1 0 0 1
0 0 0 0
3 0 0 3
0 0 0 0
```

---

# Approach (Better)

Instead of immediately changing the matrix whenever we find a `0`, we first **remember** which rows and columns need to become zero.

We use two extra arrays:

- `row[]` → Stores which rows should become zero.
- `col[]` → Stores which columns should become zero.

---

# Algorithm

### Step 1

Create two arrays.

```cpp
vector<int> row(m,0);
vector<int> col(n,0);
```

Initially

```
row = [0,0,0,0]

col = [0,0,0,0]
```

---

### Step 2

Traverse the matrix.

Whenever a `0` is found:

```
row[i] = 1
col[j] = 1
```

This means:

- Entire row `i` should become zero.
- Entire column `j` should become zero.

---

### Step 3

Traverse the matrix again.

If

```
row[i] == 1
```

OR

```
col[j] == 1
```

then make

```
matrix[i][j] = 0
```

---

# Dry Run

## Initial Matrix

```
      C0 C1 C2 C3

R0    1  1  1  1
R1    2  0  2  2
R2    3  3  3  3
R3    4  4  0  4
```

There are two zeros:

- (1,1)
- (3,2)

---

## First Pass (Mark Rows & Columns)

### Zero found at (1,1)

Mark

```
row[1] = 1
col[1] = 1
```

```
row = [0,1,0,0]

col = [0,1,0,0]
```

---

### Zero found at (3,2)

Mark

```
row[3] = 1
col[2] = 1
```

Now

```
row = [0,1,0,1]

col = [0,1,1,0]
```

---

## Marker Diagram

```
Rows

R0  0
R1  1  ← Make this row zero
R2  0
R3  1  ← Make this row zero


Columns

C0  0
C1  1  ← Make this column zero
C2  1  ← Make this column zero
C3  0
```

---

## Second Pass

Now check every cell.

If either

```
row[i] == 1
```

or

```
col[j] == 1
```

then set it to zero.

Example

### Cell (0,1)

```
row[0] = 0

col[1] = 1
```

Column is marked.

```
1 → 0
```

---

### Cell (1,3)

```
row[1] = 1
```

Entire row becomes zero.

```
2 → 0
```

---

### Cell (2,2)

```
row[2] = 0

col[2] = 1
```

Column is marked.

```
3 → 0
```

---

Continue this for every cell.

---

# Final Matrix

```
1 0 0 1
0 0 0 0
3 0 0 3
0 0 0 0
```

---

# Flow Diagram

```
                Initial Matrix

        1 1 1 1
        2 0 2 2
        3 3 3 3
        4 4 0 4
                │
                │
                ▼

       Traverse Matrix Once

       Found Zero at (1,1)
       Found Zero at (3,2)
                │
                ▼

        Create Marker Arrays

row = [0,1,0,1]

col = [0,1,1,0]
                │
                ▼

 Traverse Matrix Again

If row[i]==1 OR col[j]==1

        ↓

Make matrix[i][j] = 0
                │
                ▼

          Final Matrix

        1 0 0 1
        0 0 0 0
        3 0 0 3
        0 0 0 0
```

---

# Why Not Change the Matrix Immediately?

Consider

```
1 0 1
1 1 1
1 1 1
```

If we immediately make row 0 and column 1 zero, the matrix becomes

```
0 0 0
1 0 1
1 0 1
```

Now the **newly created zeros** would also be processed, causing incorrect results.

Therefore, we first **mark** all affected rows and columns, and only then update the matrix.

---

# Code

```cpp
class Solution {
public:
    void setMatrixZeroes(vector<vector<int>> &mat) {

        int m = mat.size();
        int n = mat[0].size();

        vector<int> row(m, 0);
        vector<int> col(n, 0);

        // First Pass
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {

                if (mat[i][j] == 0) {
                    row[i] = 1;
                    col[j] = 1;
                }

            }
        }

        // Second Pass
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {

                if (row[i] == 1 || col[j] == 1) {
                    mat[i][j] = 0;
                }

            }
        }

    }
};
```

---

# Complexity Analysis

### Time Complexity

- First traversal → **O(M × N)**
- Second traversal → **O(M × N)**

Overall

```
O(M × N)
```

---

### Space Complexity

Extra arrays:

- `row[]` → **O(M)**
- `col[]` → **O(N)**

Overall

```
O(M + N)
```

---

# Key Idea

Instead of modifying the matrix immediately, **mark** all rows and columns that should become zero using two helper arrays. After all markers are recorded, perform a second traversal to update the matrix. This avoids incorrect cascading zeros while keeping the implementation simple and easy to understand.
