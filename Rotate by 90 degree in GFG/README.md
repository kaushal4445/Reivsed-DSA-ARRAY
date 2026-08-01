# Rotate Matrix by 90° Anti-Clockwise (Optimal Approach)

## Problem Statement

Given an **N × N** matrix, rotate it by **90° Anti-Clockwise** **in-place**.

The rotation should be done **without using any extra matrix**.

---

## Example

### Input

```
0 1 2
3 4 5
6 7 8
```

### Output

```
2 5 8
1 4 7
0 3 6
```

---

# Intuition

A **90° Anti-Clockwise** rotation can be achieved in **two simple steps**:

1. **Transpose** the matrix.
2. **Reverse every column**.

Instead of creating another matrix, we rearrange the existing matrix itself.

This makes the solution **space efficient**.

---

# Algorithm

### Step 1

Transpose the matrix.

```cpp
for(int i=0;i<n-1;i++)
{
    for(int j=i+1;j<n;j++)
    {
        swap(mat[i][j],mat[j][i]);
    }
}
```

---

### Step 2

Reverse every column.

```cpp
for(int j=0;j<n;j++)
{
    int top=0;
    int bottom=n-1;

    while(top<bottom)
    {
        swap(mat[top][j],mat[bottom][j]);
        top++;
        bottom--;
    }
}
```

---

# Dry Run

## Initial Matrix

```
      C0 C1 C2

R0    0  1  2
R1    3  4  5
R2    6  7  8
```

---

# Step 1 : Transpose

A transpose converts **rows into columns**.

Swap

```
(0,1) ↔ (1,0)

(0,2) ↔ (2,0)

(1,2) ↔ (2,1)
```

### Before

```
0 1 2
3 4 5
6 7 8
```

### After Transpose

```
0 3 6
1 4 7
2 5 8
```

---

## Visual Diagram

```
Before Transpose

      C0 C1 C2

R0    0  1  2
R1    3  4  5
R2    6  7  8


↓

After Transpose

      C0 C1 C2

R0    0  3  6
R1    1  4  7
R2    2  5  8
```

---

# Step 2 : Reverse Every Column

Now reverse each column individually.

---

### Column 0

Before

```
0
1
2
```

After

```
2
1
0
```

---

### Column 1

Before

```
3
4
5
```

After

```
5
4
3
```

---

### Column 2

Before

```
6
7
8
```

After

```
8
7
6
```

---

## Matrix After Reversing Columns

```
2 5 8
1 4 7
0 3 6
```

This is the required **90° Anti-Clockwise Rotation**.

---

# Complete Flow Diagram

```
              Original Matrix

        0 1 2
        3 4 5
        6 7 8
              │
              │
              ▼

         Step 1 : Transpose

        0 3 6
        1 4 7
        2 5 8
              │
              │
              ▼

    Step 2 : Reverse Every Column

Column 0

0      2
1  →   1
2      0

Column 1

3      5
4  →   4
5      3

Column 2

6      8
7  →   7
8      6
              │
              ▼

        Final Matrix

        2 5 8
        1 4 7
        0 3 6
```

---

# Why Does This Work?

### After Transpose

Rows become columns.

```
0 3 6
1 4 7
2 5 8
```

But this is **not yet rotated**.

Reversing every column flips the matrix vertically.

That places every element in its correct **90° Anti-Clockwise** position.

---

# Why `j = i + 1`?

Notice

```cpp
for(int j=i+1;j<n;j++)
```

We only swap elements **above the main diagonal**.

Example

```
Swap

(0,1) ↔ (1,0)

(0,2) ↔ (2,0)

(1,2) ↔ (2,1)
```

If we started from `j = 0`, every pair would be swapped **twice**, and the matrix would return to its original form.

---

# Code

```cpp
class Solution {
public:
    void rotateMatrix(vector<vector<int>>& mat) {

        int n = mat.size();

        // Step 1 : Transpose
        for(int i = 0; i < n - 1; i++) {
            for(int j = i + 1; j < n; j++) {
                swap(mat[i][j], mat[j][i]);
            }
        }

        // Step 2 : Reverse Every Column
        for(int j = 0; j < n; j++) {

            int top = 0;
            int bottom = n - 1;

            while(top < bottom) {
                swap(mat[top][j], mat[bottom][j]);
                top++;
                bottom--;
            }
        }
    }
};
```

---

# Complexity Analysis

### Time Complexity

- Transpose → **O(N²)**
- Reverse Columns → **O(N²)**

Overall

```
O(N²)
```

---

### Space Complexity

No extra matrix is used.

```
O(1)
```

---

# Memory Trick

| Rotation | Step 1 | Step 2 |
|----------|---------|---------|
| **90° Clockwise** | Transpose | Reverse every **Row** |
| **90° Anti-Clockwise** | Transpose | Reverse every **Column** |

---

# Key Takeaway

Instead of creating a new matrix, we perform two in-place operations:

1. **Transpose** the matrix (convert rows into columns).
2. **Reverse every column** to complete the **90° Anti-Clockwise** rotation.

This approach is simple, efficient, and achieves **O(N²)** time with **O(1)** extra space.
