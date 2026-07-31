# Next Permutation (LeetCode 31)

## Problem Statement

Given an array of integers, find the **next lexicographically greater permutation**.

If such a permutation does not exist (the array is in descending order), rearrange it into the **lowest possible order (ascending order)**.

---

## Example 1

### Input

```text
[1,2,3]
```

### Output

```text
[1,3,2]
```

---

## Example 2

### Input

```text
[3,2,1]
```

### Output

```text
[1,2,3]
```

---

# Idea

The algorithm consists of **3 simple steps**:

1. Find the **Pivot** (first decreasing element from the right).
2. Find the **next greater element** than the pivot from the right and swap.
3. Reverse everything after the pivot.

---

# Code

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& A) {

        int pivot = -1;
        int n = A.size();

        // Step 1: Find Pivot
        for(int i = n-2; i >=0; i--){
            if(A[i] < A[i+1]){
                pivot = i;
                break;
            }
        }

        // Step 2: If no pivot exists
        if(pivot == -1){
            reverse(A.begin(),A.end());
            return;
        }

        // Step 3: Find next greater element
        for(int i=n-1;i>pivot;i--){
            if(A[i] > A[pivot]){
                swap(A[i],A[pivot]);
                break;
            }
        }

        // Step 4: Reverse right part
        reverse(A.begin()+pivot+1,A.end());
    }
};
```

---

# Example

Input

```text
A = [1,2,7,4,3,1]
```

---

# Step 1 : Find the Pivot

Start from the right side.

```
Index

0   1   2   3   4   5

1   2   7   4   3   1
                ↑
```

Compare from right

```
3 > 1  ❌

4 > 3  ❌

7 > 4  ❌

2 < 7  ✅
```

So,

```
Pivot = Index 1

Value = 2
```

Diagram

```
0   1   2   3   4   5

1   2   7   4   3   1
    ↑
  Pivot
```

---

# Why do we find the Pivot?

Everything to the right of the pivot is already in **descending order**.

```
7 4 3 1
```

Since it is the largest arrangement possible,
we must change the pivot.

---

# Step 2 : Find Next Greater Element

Search from the **right side**.

Need number greater than **2**

```
1 ❌

3 ✅

4

7
```

The first greater element from the right is **3**.

Diagram

```
1   2   7   4   3   1
    ↑           ↑
 Pivot      Greater Element
```

Swap

```
1   3   7   4   2   1
```

---

# Step 3 : Reverse Right Side

Current array

```
1   3   7   4   2   1
```

Right side after pivot

```
7 4 2 1
```

Reverse it

```
1 2 4 7
```

Final array

```
1   3   1   2   4   7
```

Answer

```
[1,3,1,2,4,7]
```

---

# Complete Dry Run

Input

```
1 2 7 4 3 1
```

Find Pivot

```
2 < 7

Pivot = 2
```

Swap

```
1 3 7 4 2 1
```

Reverse suffix

```
1 3 1 2 4 7
```

Output

```
1 3 1 2 4 7
```

---

# Example 2

Input

```
1 3 2
```

Find Pivot

```
3 > 2 ❌

1 < 3 ✅
```

Pivot

```
1
```

Swap with

```
2
```

After Swap

```
2 3 1
```

Reverse Right

```
2 1 3
```

Output

```
2 1 3
```

---

# Example 3

Input

```
3 2 1
```

Find Pivot

```
3>2

2>1

No Pivot
```

Diagram

```
3   2   1

Descending Order
```

Since there is **no greater permutation**, reverse the whole array.

```
1 2 3
```

Output

```
[1,2,3]
```

---

# Visualization

```
                Start

                  │

                  ▼

       Traverse From Right

                  │

                  ▼

        Find First A[i]<A[i+1]

                  │

        ┌─────────┴──────────┐

        │                    │

      Found              Not Found

        │                    │

        ▼                    ▼

 Find Greater Element     Reverse Whole Array

        │

        ▼

      Swap

        │

        ▼

 Reverse Everything
 After Pivot

        │

        ▼

 Return Answer
```

---

# Why Reverse?

After swapping,

the right side is still in **descending order**.

Example

```
7 4 2 1
```

To obtain the **smallest possible** permutation greater than the current one,

convert it into ascending order.

```
1 2 4 7
```

The easiest way is

```
reverse()
```

because it is already sorted in descending order.

---

# Complexity Analysis

| Operation | Complexity |
|-----------|------------|
| Find Pivot | **O(N)** |
| Find Greater Element | **O(N)** |
| Reverse | **O(N)** |
| Overall Time | **O(N)** |
| Extra Space | **O(1)** |

---

# Key Points

- ✅ Traverse from the right.
- ✅ Find the first decreasing element (Pivot).
- ✅ Find the smallest greater element from the right.
- ✅ Swap them.
- ✅ Reverse the suffix.
- ✅ If no pivot exists, reverse the whole array.
- ✅ Time Complexity: **O(N)**.
- ✅ Space Complexity: **O(1)**.
