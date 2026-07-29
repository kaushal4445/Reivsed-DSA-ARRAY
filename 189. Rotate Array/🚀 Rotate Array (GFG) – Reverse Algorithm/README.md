# 🔄 Rotate Array (GFG) – Reverse Algorithm

<p align="center">
  <img src="https://img.shields.io/badge/Language-C%2B%2B-blue.svg" />
  <img src="https://img.shields.io/badge/Time-O(n)-brightgreen.svg" />
  <img src="https://img.shields.io/badge/Space-O(1)-orange.svg" />
  <img src="https://img.shields.io/badge/Algorithm-Reverse%20Algorithm-red.svg" />
</p>

---

# 📌 Problem Statement

Given an integer array `arr[]` of size `n`, rotate the array **to the left** by `d` positions.

### Example

#### Input

```text
arr = [1,2,3,4,5,6,7]
d = 2
```

#### Output

```text
[3,4,5,6,7,1,2]
```

---

# 💡 Intuition

Instead of shifting every element one by one, we use the **Reverse Algorithm**.

We divide the array into **two parts**.

```text
A = First d elements
B = Remaining elements
```

Original Array

```text
+-----+-------------------------+
|1  2 |3  4  5  6  7           |
+-----+-------------------------+
   A             B
```

Our Goal

```text
+-------------------------+-----+
|3  4  5  6  7           |1  2 |
+-------------------------+-----+
            B               A
```

---

# ❓ Why `d = d % n`?

Before rotating, we write

```cpp
d = d % n;
```

where

- `d` = Number of rotations
- `n` = Size of the array

This avoids unnecessary rotations.

---

## Example 1

```text
n = 7
d = 10
```

```cpp
d = 10 % 7;
```

Result

```text
d = 3
```

Instead of rotating **10 times**, we only rotate **3 times**.

### Why?

```text
0 rotations  → Original Array
1 rotation   → Rotate Once
2 rotations  → Rotate Twice
3 rotations  → Rotate Three Times
4 rotations  → Rotate Four Times
5 rotations  → Rotate Five Times
6 rotations  → Rotate Six Times
7 rotations  → Original Again
8 rotations  → Same as 1 Rotation
9 rotations  → Same as 2 Rotations
10 rotations → Same as 3 Rotations
```

---

## Example 2

```text
arr = [1,2,3,4,5]

n = 5
d = 5
```

```cpp
d = 5 % 5;
```

```text
d = 0
```

The array remains unchanged.

```text
Before

1 2 3 4 5

↓

After

1 2 3 4 5
```

> 💡 **Memory Tip:** Imagine the array as a **clock**. After one complete circle (`n` rotations), you're back where you started.

---

# 🚀 Reverse Algorithm

The algorithm has only **3 simple steps**.

### Step 1

Reverse the first `d` elements.

### Step 2

Reverse the remaining `n-d` elements.

### Step 3

Reverse the entire array.

---

# 📝 Dry Run

## Input

```text
arr = [1,2,3,4,5,6,7]
d = 2
```

---

# 🔹 Step 0 : Divide the Array

```text
+-----+-------------------------+
|1  2 |3  4  5  6  7           |
+-----+-------------------------+
   A             B
```

Target

```text
+-------------------------+-----+
|3  4  5  6  7           |1  2 |
+-------------------------+-----+
            B               A
```

---

# 🔹 Step 1 : Reverse First `d` Elements

```cpp
reverse(arr.begin(), arr.begin() + d);
```

Before

```text
+-----+-------------------------+
|1  2 |3  4  5  6  7           |
+-----+-------------------------+
```

↓

After

```text
+-----+-------------------------+
|2  1 |3  4  5  6  7           |
+-----+-------------------------+
```

Current Array

```text
2 1 3 4 5 6 7
```

---

# 🔹 Step 2 : Reverse Remaining Elements

```cpp
reverse(arr.begin() + d, arr.end());
```

Reverse

```text
3 4 5 6 7
```

↓

Result

```text
7 6 5 4 3
```

Current Array

```text
+-----+-------------------------+
|2  1 |7  6  5  4  3           |
+-----+-------------------------+
```

or

```text
2 1 7 6 5 4 3
```

---

# 🔹 Step 3 : Reverse Entire Array

```cpp
reverse(arr.begin(), arr.end());
```

Before

```text
2 1 7 6 5 4 3
```

↓

After

```text
3 4 5 6 7 1 2
```

🎉 Final Answer

```text
+-------------------------+-----+
|3  4  5  6  7           |1  2 |
+-------------------------+-----+
```

---

# 🎯 Complete Visualization

```text
Original

1 2 | 3 4 5 6 7
A   |     B

        │
        ▼
Reverse A

2 1 | 3 4 5 6 7

        │
        ▼
Reverse B

2 1 | 7 6 5 4 3

        │
        ▼
Reverse Whole Array

3 4 5 6 7 | 1 2
     B     |  A
```

---

# 🧠 Why Does This Work?

Suppose

```text
A = First d elements
B = Remaining elements
```

Original

```text
A B
```

Step 1

```text
reverse(A) B
```

Step 2

```text
reverse(A) reverse(B)
```

Step 3

```text
reverse(reverse(A) reverse(B))
```

Which becomes

```text
B A
```

Because

```text
reverse(reverse(A)) = A

reverse(reverse(B)) = B
```

Hence the array becomes

```text
B A
```

which is exactly the required left rotation.

---

# 💻 C++ Solution

```cpp
class Solution {
public:
    void rotateArr(vector<int>& arr, int d) {

        int n = arr.size();

        if (n == 0)
            return;

        d = d % n;

        if (d == 0)
            return;

        reverse(arr.begin(), arr.begin() + d);

        reverse(arr.begin() + d, arr.end());

        reverse(arr.begin(), arr.end());
    }
};
```

---

# 📊 Complexity Analysis

| Operation | Complexity |
|-----------|------------|
| Reverse First `d` | **O(d)** |
| Reverse Remaining | **O(n-d)** |
| Reverse Entire Array | **O(n)** |

### ⏱️ Time Complexity

```text
O(n)
```

### 💾 Space Complexity

```text
O(1)
```

No extra array is used.

The rotation is performed **in-place**.

---

# 🔄 LeetCode vs GFG

| LeetCode 189 | GFG Rotate Array |
|--------------|------------------|
| Right Rotation | Left Rotation |
| Reverse Whole Array | Reverse First `d` |
| Reverse First `k` | Reverse Remaining |
| Reverse Remaining | Reverse Whole Array |

---

# 📝 Memory Tricks

## 🔹 Trick 1 : `d %= n`

Imagine the array is a **clock**.

```text
0 Rotation  → Original

1 Rotation

2 Rotations

...

n Rotations → Original Again
```

So,

```cpp
d = d % n;
```

keeps only the effective rotations.

---

## 🔹 Trick 2 : GFG Left Rotation

```text
Reverse First d
        │
        ▼
Reverse Remaining
        │
        ▼
Reverse Whole Array
```

Remember it as

> **Parts First → Whole Last**

---

## 🔹 Trick 3 : LeetCode Right Rotation

```text
Reverse Whole Array
        │
        ▼
Reverse First k
        │
        ▼
Reverse Remaining
```

Remember it as

> **Whole First → Parts Later**

---

# ✅ Key Takeaways

- ✔️ Normalize rotations using `d %= n`.
- ✔️ Divide the array into **A** and **B**.
- ✔️ Reverse **A**.
- ✔️ Reverse **B**.
- ✔️ Reverse the entire array.
- ✔️ Time Complexity: **O(n)**
- ✔️ Space Complexity: **O(1)**

---

<div align="center">

# ⭐ If this README helped you, don't forget to ⭐ the repository!

### Happy Coding 🚀

</div>
