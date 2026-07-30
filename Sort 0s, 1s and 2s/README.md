# 🔥 Sort an Array of 0s, 1s, and 2s (Dutch National Flag Algorithm)

## 📌 Problem Statement

Given an array consisting only of **0s, 1s, and 2s**, sort the array in ascending order **without using any extra space**.

### Example

```cpp
Input:
arr = {2, 0, 2, 1, 1, 0}

Output:
{0, 0, 1, 1, 2, 2}
```

---

# 💡 Intuition

Since the array contains only three distinct values:

- `0` should be on the **left**
- `1` should be in the **middle**
- `2` should be on the **right**

Instead of sorting the array, we can place each element directly into its correct region.

To achieve this, we use **three pointers**:

- **low** → Position where the next `0` should be placed.
- **mid** → Current element being processed.
- **high** → Position where the next `2` should be placed.

---

# 🎯 Pointer Representation

Initially

```text
low
 ↓
mid
 ↓
                high
                 ↓
+---+---+---+---+---+---+
| 2 | 0 | 2 | 1 | 1 | 0 |
+---+---+---+---+---+---+
```

Initially

```text
low = 0
mid = 0
high = n-1
```

---

# 🚀 Algorithm

Continue while

```text
mid <= high
```

There are **three cases**.

---

# Case 1 : arr[mid] == 0

Swap with `low`.

```text
Before

L,M
 ↓
 ↓
2 0 2 1 1 0
          ↑
          H

Current = 0

Swap(mid, low)
```

Example

```text
Before

0 1 2
↑ ↑
L M

After Swap

0 1 2
```

Move both pointers.

```cpp
low++
mid++
```

Because:

- 0 is now in the correct position.
- The swapped element has already been processed.

---

# Case 2 : arr[mid] == 1

No swap is required.

```text
0 0 1 2 2
    ↑
   mid
```

Since `1` belongs in the middle,

Simply move

```cpp
mid++
```

---

# Case 3 : arr[mid] == 2

Swap with `high`.

Example

```text
Before

0 1 2 0
    ↑   ↑
   M    H
```

Swap

```text
0 1 0 2
    ↑   ↑
   M    H
```

Now decrease

```cpp
high--
```

---

# ❓ Why don't we increment `mid` here?

Notice after swapping,

```text
Before

0 1 2 0
    ↑
   mid
```

Swap

```text
0 1 0 2
    ↑
   mid
```

A **new value (0)** has arrived at `mid`.

This value has **not been processed yet**.

If we do

```cpp
mid++;
```

The new `0` would be skipped.

Therefore,

```cpp
high--;
```

Only decrease `high`.

Keep `mid` at the same position so we can process the swapped element.

---

# 📖 Complete Dry Run

Input

```cpp
arr = {2,0,2,1,1,0}
```

---

## Initial State

```text
L,M                 H
 ↓                  ↓

2 0 2 1 1 0
```

---

### Step 1

Current = 2

Swap(mid, high)

```text
L,M             H
 ↓              ↓

0 0 2 1 1 2
```

high--

---

### Step 2

Current = 0

Swap(low, mid)

```text
L M           H
  ↓           ↓

0 0 2 1 1 2
```

low++

mid++

---

### Step 3

Current = 0

```text
0 0 2 1 1 2
  ↑ ↑
  L M
```

Swap

(No visible change)

Move

```text
low++
mid++
```

---

### Step 4

Current = 2

```text
0 0 2 1 1 2
    ↑     ↑
    M     H
```

Swap

```text
0 0 1 1 2 2
```

high--

---

### Step 5

Current = 1

Move

```text
mid++
```

---

### Step 6

Current = 1

Move

```text
mid++
```

Now

```text
mid > high
```

Stop.

---

# ✅ Final Array

```text
0 0 1 1 2 2
```

---

# 🧠 Visualization

```
                Unknown Region
                      │
                      ▼

+---------+-----------------------+---------+
|   0's   |   Unprocessed Area    |   2's   |
+---------+-----------------------+---------+
          ↑                       ↑
         low                    high
            ↑
           mid
```

As the algorithm runs,

- Left side grows with **0s**
- Middle grows with **1s**
- Right side grows with **2s**
- Unknown region keeps shrinking

Eventually,

```text
+---------+---------+---------+
|   0's   |   1's   |   2's   |
+---------+---------+---------+
```

---

# ✅ C++ Solution

```cpp
class Solution {
public:
    void sort012(vector<int>& arr) {

        int low = 0;
        int mid = 0;
        int high = arr.size() - 1;

        while (mid <= high) {

            if (arr[mid] == 0) {

                swap(arr[low], arr[mid]);
                low++;
                mid++;

            }
            else if (arr[mid] == 1) {

                mid++;

            }
            else {

                swap(arr[mid], arr[high]);
                high--;

            }
        }
    }
};
```

---

# ⏱️ Complexity Analysis

### Time Complexity

Every element is visited at most once.

```
O(n)
```

---

### Space Complexity

No extra array is used.

```
O(1)
```

---

# ✅ Why This Algorithm Works

The algorithm always maintains four regions:

```text
0 ...... low-1      → All 0s

low .... mid-1      → All 1s

mid .... high       → Unknown

high+1 ... n-1      → All 2s
```

With each iteration, the **unknown region becomes smaller**, until every element is placed in its correct section.

---

# ⭐ Key Takeaways

- Uses **three pointers** (`low`, `mid`, `high`)
- No sorting algorithm is required
- No extra memory is used
- Runs in **O(n)** time
- Also known as the **Dutch National Flag Algorithm** (by Edsger Dijkstra)
