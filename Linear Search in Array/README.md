# 🔍 Linear Search in Array (GFG)

<p align="center">
  <img src="https://img.shields.io/badge/Language-C%2B%2B-blue.svg" />
  <img src="https://img.shields.io/badge/Algorithm-Linear%20Search-red.svg" />
  <img src="https://img.shields.io/badge/Time-O(n)-brightgreen.svg" />
  <img src="https://img.shields.io/badge/Space-O(1)-orange.svg" />
</p>

---

# 📌 Problem Statement

Given an array `arr[]` and an integer `x`, find the **index of the first occurrence** of `x` in the array.

If the element is not present, return:

```text
-1
```

---

# 📝 Example

## Example 1

### Input

```text
arr = [10,20,30,40,50]
x = 30
```

### Output

```text
2
```

### Explanation

The element `30` is present at index `2`.

```
Index:
 0   1   2   3   4
+---+---+---+---+---+
|10 |20 |30 |40 |50 |
+---+---+---+---+---+

        ↑
      Found x
```

---

# 💡 Approach: Linear Search

Linear Search checks each element one by one from the beginning of the array.

### Steps:

1. Start from index `0`.
2. Compare the current element with `x`.
3. If it matches, return the index.
4. If the complete array is checked and no match is found, return `-1`.

---

# 🔍 Dry Run

## Input

```text
arr = [5,8,2,9,4]
x = 9
```

---

## Step 1: Start Searching

Array:

```
Index:
 0   1   2   3   4

+---+---+---+---+---+
| 5 | 8 | 2 | 9 | 4 |
+---+---+---+---+---+
  ↑
 i = 0
```

Check:

```text
arr[0] == x ?

5 == 9 ❌
```

Move to next index.

---

## Step 2

```
Index:
 0   1   2   3   4

+---+---+---+---+---+
| 5 | 8 | 2 | 9 | 4 |
+---+---+---+---+---+
      ↑
    i = 1
```

Check:

```text
arr[1] == x ?

8 == 9 ❌
```

Move ahead.

---

## Step 3

```
Index:
 0   1   2   3   4

+---+---+---+---+---+
| 5 | 8 | 2 | 9 | 4 |
+---+---+---+---+---+
          ↑
        i = 2
```

Check:

```text
arr[2] == x ?

2 == 9 ❌
```

Continue.

---

## Step 4

```
Index:
 0   1   2   3   4

+---+---+---+---+---+
| 5 | 8 | 2 | 9 | 4 |
+---+---+---+---+---+
              ↑
            i = 3
```

Check:

```text
arr[3] == x ?

9 == 9 ✅
```

Element found!

Return:

```text
3
```

---

# 🎯 Complete Visualization

```
Search x = 9


[5] [8] [2] [9] [4]
 ↓   ↓   ↓   ↓

No  No  No  YES

              ↑
           Return index
```

---

# ❌ Element Not Found Example

Input:

```
arr = [1,3,5,7]
x = 9
```

Searching:

```
[1] [3] [5] [7]
 ↓   ↓   ↓   ↓

No  No  No  No
```

All elements checked.

Return:

```
-1
```

---

# 💻 C++ Solution

```cpp
class Solution {
public:
    int search(vector<int>& arr, int x) {

        int n = arr.size();

        // Traverse the complete array
        for(int i = 0; i < n; i++)
        {
            // If element is found, return index
            if(arr[i] == x)
                return i;
        }

        // Element not found
        return -1;
    }
};
```

---

# 🧠 How Code Works

### Step 1: Get Array Size

```cpp
int n = arr.size();
```

Example:

```
arr = [10,20,30,40]

n = 4
```

---

### Step 2: Traverse Array

```cpp
for(int i = 0; i < n; i++)
```

The loop moves like:

```
i = 0 → arr[0]
i = 1 → arr[1]
i = 2 → arr[2]
i = 3 → arr[3]
```

---

### Step 3: Compare Each Element

```cpp
if(arr[i] == x)
```

Example:

```
arr = [10,20,30,40]
x = 30
```

Checking:

```
10 == 30 ❌

20 == 30 ❌

30 == 30 ✅
```

Return:

```
2
```

---

# 📊 Complexity Analysis

## Time Complexity

### Best Case

Element found at first position:

```
[5,10,20,30]

x = 5
```

Only one comparison.

```
O(1)
```

---

### Worst Case

Element is at the end or not present:

```
[5,10,20,30]

x = 30
```

All elements checked.

```
O(n)
```

---

### Overall Time Complexity

```
O(n)
```

---

## Space Complexity

No extra memory is used.

```
O(1)
```

---

# 🔄 Linear Search Flow Diagram

```
          Start
            |
            ▼
     Take first element
            |
            ▼
       Compare with x
            |
      +-----+-----+
      |           |
    Match       Not Match
      |           |
      ▼           ▼
 Return Index   Next Element
                  |
                  ▼
             More Elements?
                  |
             +----+----+
             |         |
            Yes        No
             |         |
             ▼         ▼
          Continue   Return -1
```

---

# 🧠 Memory Trick

Remember:

```
Check → Compare → Move → Repeat
```

or

```
Start
  ↓
Search One by One
  ↓
Found? Return Index
  ↓
Not Found? Return -1
```

---

# ✅ Key Takeaways

- ✔️ Linear Search checks elements one by one.
- ✔️ Works on sorted and unsorted arrays.
- ✔️ Returns the first matching index.
- ✔️ Returns `-1` when the element is absent.
- ✔️ Simple and easy to implement.
- ✔️ Time Complexity: **O(n)**
- ✔️ Space Complexity: **O(1)**

---

<div align="center">

# ⭐ If this explanation helped you, give the repository a ⭐!

## Happy Coding 🚀

</div>
