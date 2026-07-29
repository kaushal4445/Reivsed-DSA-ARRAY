# 🔢 Single Number | XOR Approach (LeetCode 136)

<p align="center">
  <img src="https://img.shields.io/badge/Language-C%2B%2B-blue.svg" />
  <img src="https://img.shields.io/badge/Topic-Array-orange.svg" />
  <img src="https://img.shields.io/badge/Algorithm-XOR-red.svg" />
  <img src="https://img.shields.io/badge/Time%20Complexity-O(n)-brightgreen.svg" />
  <img src="https://img.shields.io/badge/Space%20Complexity-O(1)-yellow.svg" />
</p>

---

# 📌 Problem Statement

Given a **non-empty array of integers** `nums`, every element appears **twice** except for one element that appears **only once**.

Find the element that appears only once.

---

# 📝 Examples

## Example 1

### Input

```text
nums = [2,2,1]
```

### Output

```text
1
```

### Explanation

```
2 appears two times

1 appears one time

Answer = 1
```

---

## Example 2

### Input

```text
nums = [4,1,2,1,2]
```

### Output

```text
4
```

### Explanation

```
Numbers:

4  1  2  1  2


Pairs:

1 1  → Cancel
2 2  → Cancel


Remaining:

4
```

---

# 💡 Approach

We solve this problem using the **XOR operator (`^`)**.

Instead of using:

❌ HashMap  
❌ Sorting  
❌ Extra counting array  

we use XOR because it automatically removes duplicates.

---

# 🧠 XOR Properties

## Property 1: Same numbers cancel each other

```
a ^ a = 0
```

Example:

```
5 ^ 5
```

Binary:

```
101
101
---
000
```

Result:

```
0
```

---

## Property 2: XOR with zero keeps the number

```
a ^ 0 = a
```

Example:

```
7 ^ 0
```

Binary:

```
111
000
---
111
```

Result:

```
7
```

---

# 🚀 Main Idea

Suppose:

```
nums = [4,1,2,1,2]
```

Apply XOR on all elements:

```
4 ^ 1 ^ 2 ^ 1 ^ 2
```

Rearrange:

```
4 ^ (1 ^ 1) ^ (2 ^ 2)
```

Duplicate values cancel:

```
1 ^ 1 = 0

2 ^ 2 = 0
```

Now:

```
4 ^ 0 ^ 0
```

Using:

```
a ^ 0 = a
```

Answer:

```
4
```

---

# 🎯 Complete Visualization

## Input Array

```
nums = [4,1,2,1,2]
```

Diagram:

```
Index:

 0   1   2   3   4

+---+---+---+---+---+
| 4 | 1 | 2 | 1 | 2 |
+---+---+---+---+---+
```

---

# 🔍 Dry Run Step By Step

## Initial State

```cpp
xorr = 0;
```

Diagram:

```
xorr

 0
```

---

# Step 1

Take:

```
nums[0] = 4
```

Operation:

```
xorr = 0 ^ 4
```

Binary:

```
000
100
---
100
```

Result:

```
xorr = 4
```

---

# Step 2

Take:

```
nums[1] = 1
```

Operation:

```
xorr = 4 ^ 1
```

Binary:

```
100
001
---
101
```

Result:

```
xorr = 5
```

---

# Step 3

Take:

```
nums[2] = 2
```

Operation:

```
xorr = 5 ^ 2
```

Binary:

```
101
010
---
111
```

Result:

```
xorr = 7
```

---

# Step 4

Take:

```
nums[3] = 1
```

Operation:

```
xorr = 7 ^ 1
```

Binary:

```
111
001
---
110
```

Result:

```
xorr = 6
```

---

# Step 5

Take:

```
nums[4] = 2
```

Operation:

```
xorr = 6 ^ 2
```

Binary:

```
110
010
---
100
```

Result:

```
xorr = 4
```

---

# 🎉 Final Answer

```
xorr = 4
```

The number appearing only once is:

```
4
```

---

# 🔄 Algorithm Flow Diagram

```
              START
                |
                ▼
        Create xorr = 0
                |
                ▼
       Traverse Array Elements
                |
                ▼
        Apply XOR Operation

        xorr = xorr ^ nums[i]

                |
                ▼
     Duplicate Elements Cancel
                |
                ▼
     Single Element Remains
                |
                ▼
             RETURN
```

---

# 💻 C++ Solution

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {

        int n = nums.size();

        int xorr = 0;

        // XOR all elements
        for(int i = 0; i < n; i++) {

            xorr = xorr ^ nums[i];
        }

        return xorr;
    }
};
```

---

# 📝 Code Explanation

## Step 1: Store Array Size

```cpp
int n = nums.size();
```

Example:

```
nums = [4,1,2,1,2]

n = 5
```

---

## Step 2: Create XOR Variable

```cpp
int xorr = 0;
```

Initially:

```
xorr = 0
```

This variable stores the XOR result.

---

## Step 3: Traverse Array

```cpp
for(int i = 0; i < n; i++)
```

The loop visits:

```
4 → 1 → 2 → 1 → 2
```

---

## Step 4: Apply XOR

```cpp
xorr = xorr ^ nums[i];
```

Every duplicate number cancels automatically.

Example:

```
1 ^ 1 = 0

2 ^ 2 = 0
```

Only the unique number remains.

---

## Step 5: Return Answer

```cpp
return xorr;
```

Returns the single occurring number.

---

# 📊 Complexity Analysis

| Type | Complexity |
|---|---|
| Time Complexity | O(n) |
| Space Complexity | O(1) |

---

# ⚡ Why XOR Approach is Best?

| Method | Time | Space | Problem |
|---|---|---|---|
| Sorting | O(n log n) | O(1) | Sorting required |
| HashMap | O(n) | O(n) | Extra memory |
| Counting | O(n) | O(n) | Extra storage |
| XOR | O(n) | O(1) | ✅ Best |

---

# 🧠 Memory Trick

Remember:

```
Same ^ Same = 0

Number ^ 0 = Number
```

So:

```
Duplicate values disappear

Only unique value survives
```

Short formula:

```
ALL NUMBERS
     XOR
ARRAY NUMBERS
     =
SINGLE NUMBER
```

---

# ✅ Key Takeaways

✔️ XOR removes duplicate pairs automatically.  
✔️ No extra data structure is required.  
✔️ Works in O(n) time.  
✔️ Uses O(1) extra space.  
✔️ Simple and highly optimized solution.

---

# 🌟 Pattern Recognition

Whenever you see:

```
Every element appears twice
except one
```

Think:

```
XOR
```

---

<div align="center">

# ⭐ If this README helped you, give the repository a star!

## 🚀 Happy Coding

</div>
