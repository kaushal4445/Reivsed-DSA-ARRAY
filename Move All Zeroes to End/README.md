# 🚀 Move Zeroes (LeetCode 283)

<p align="center">
  <img src="https://img.shields.io/badge/Language-C%2B%2B-blue.svg" />
  <img src="https://img.shields.io/badge/Time-O(n)-brightgreen.svg" />
  <img src="https://img.shields.io/badge/Space-O(n)-orange.svg" />
  <img src="https://img.shields.io/badge/Approach-Temporary%20Array-red.svg" />
</p>

---

# 📌 Problem Statement

Given an integer array `nums`, move all the **0's** to the **end** of the array while maintaining the **relative order of the non-zero elements**.

---

## Example

### Input

```text
nums = [0,1,0,3,12]
```

### Output

```text
[1,3,12,0,0]
```

---

# 💡 Intuition

Instead of swapping elements multiple times, we:

1. Store all **non-zero elements** in a temporary array.
2. Copy them back into the original array.
3. Fill the remaining positions with `0`.

This makes the solution simple and easy to understand.

---

# 📝 Algorithm

### Step 1

Create a temporary array.

```cpp
vector<int> temp;
```

---

### Step 2

Traverse the original array.

If the current element is **not zero**, store it in the temporary array.

```cpp
if(nums[i] != 0)
    temp.push_back(nums[i]);
```

---

### Step 3

Copy all elements from the temporary array back into the original array.

---

### Step 4

Fill the remaining positions with `0`.

---

# 🔍 Dry Run

## Input

```text
nums = [0,1,0,3,12]
```

---

# 🔹 Step 1 : Original Array

```text
+----+----+----+----+-----+
| 0  | 1  | 0  | 3  | 12  |
+----+----+----+----+-----+
```

Temporary Array

```text
temp = [ ]
```

---

# 🔹 Step 2 : Traverse the Array

### i = 0

```text
nums[0] = 0
```

Zero found ❌

Ignore it.

```text
temp = [ ]
```

---

### i = 1

```text
nums[1] = 1
```

Non-zero ✅

Store in temp.

```text
temp = [1]
```

---

### i = 2

```text
nums[2] = 0
```

Ignore.

```text
temp = [1]
```

---

### i = 3

```text
nums[3] = 3
```

Store.

```text
temp = [1,3]
```

---

### i = 4

```text
nums[4] = 12
```

Store.

```text
temp = [1,3,12]
```

---

# 📦 Temporary Array After Traversal

```text
+----+----+-----+
| 1  | 3  | 12  |
+----+----+-----+
```

Number of non-zero elements

```text
nz = 3
```

---

# 🔹 Step 3 : Copy Temp into Original Array

```cpp
for(int i=0;i<nz;i++)
    nums[i]=temp[i];
```

Array becomes

```text
+----+----+-----+----+----+
| 1  | 3  | 12  | 3  | 12 |
+----+----+-----+----+----+
```

Notice that only the **first three positions** are updated.

The remaining values are still old values.

---

# 🔹 Step 4 : Fill Remaining Positions with Zero

```cpp
for(int i=nz;i<nums.size();i++)
    nums[i]=0;
```

Final Array

```text
+----+----+-----+----+----+
| 1  | 3  | 12  | 0  | 0  |
+----+----+-----+----+----+
```

🎉 Output

```text
[1,3,12,0,0]
```

---

# 🎯 Complete Visualization

```text
Original Array

0   1   0   3   12
│   │   │   │    │
│   ▼   │   ▼    ▼
│   1   │   3   12
│       │
▼       ▼
Ignore  Ignore

Temp Array

1   3   12

        │
        ▼

Copy Back

1   3   12   ?   ?

        │
        ▼

Fill Remaining with 0

1   3   12   0   0
```

---

# 🧠 Why Does This Work?

We first collect **all non-zero elements**.

```text
Original

0 1 0 3 12

↓

Collect Non-zero

1 3 12

↓

Copy Back

1 3 12 _ _

↓

Fill Remaining

1 3 12 0 0
```

The order of the non-zero elements never changes.

So the answer is correct.

---

# 💻 C++ Solution

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {

        vector<int> temp;

        // Store all non-zero elements
        for(int i = 0; i < nums.size(); i++) {
            if(nums[i] != 0)
                temp.push_back(nums[i]);
        }

        int nz = temp.size();

        // Copy non-zero elements back
        for(int i = 0; i < nz; i++) {
            nums[i] = temp[i];
        }

        // Fill remaining positions with zero
        for(int i = nz; i < nums.size(); i++) {
            nums[i] = 0;
        }
    }
};
```

---

# 📊 Complexity Analysis

| Operation | Complexity |
|-----------|------------|
| Traverse Array | **O(n)** |
| Copy Elements | **O(n)** |
| Fill Zeroes | **O(n)** |

### ⏱️ Time Complexity

```text
O(n)
```

Although there are three loops, each processes the array linearly, so the total time complexity remains **O(n)**.

### 💾 Space Complexity

```text
O(n)
```

A temporary array is used to store all non-zero elements.

---

# 🧠 Memory Trick

Remember these **3 simple steps**:

```text
Collect Non-Zero
        │
        ▼
Copy Back
        │
        ▼
Fill Zeroes
```

Or simply:

> **Collect ➜ Copy ➜ Fill**

---

# ✅ Key Takeaways

- ✔️ Store all non-zero elements in a temporary array.
- ✔️ Copy them back to the original array.
- ✔️ Fill the remaining positions with `0`.
- ✔️ Maintains the relative order of non-zero elements.
- ✔️ Easy to understand and implement.
- ✔️ Time Complexity: **O(n)**
- ✔️ Space Complexity: **O(n)**

---

<div align="center">

# ⭐ If this README helped you, consider giving the repository a ⭐!

### Happy Coding! 🚀

</div>
