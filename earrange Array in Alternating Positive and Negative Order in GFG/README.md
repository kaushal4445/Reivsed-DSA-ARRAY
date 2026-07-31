# Rearrange Array in Alternating Positive and Negative Order

## Problem Statement

Given an array containing both **positive** and **negative** integers, rearrange the array so that:

- Positive numbers appear first.
- Negative numbers appear next.
- The **relative order** of positive and negative numbers is preserved.
- If one type of number remains after alternating, append the remaining elements at the end.

### Example

#### Input

```text
[1, 2, 3, -4, -1, 4]
```

#### Output

```text
[1, -4, 2, -1, 3, 4]
```

---

# Approach

Instead of rearranging the array directly, we:

1. Store all **positive** numbers in one vector.
2. Store all **negative** numbers in another vector.
3. Fill the original array alternately using both vectors.
4. Append the remaining elements if one vector becomes empty.

---

# Code

```cpp
class Solution {
public:
    void rearrange(vector<int> &arr) {

        int n = arr.size();
        vector<int> pos, neg;

        // Store positives and negatives separately
        for (int x : arr) {
            if (x >= 0)
                pos.push_back(x);
            else
                neg.push_back(x);
        }

        int posIndex = 0;
        int negIndex = 0;
        int i = 0;

        // Alternate positive and negative
        while (posIndex < pos.size() && negIndex < neg.size()) {
            arr[i++] = pos[posIndex++];
            arr[i++] = neg[negIndex++];
        }

        // Copy remaining positives
        while (posIndex < pos.size())
            arr[i++] = pos[posIndex++];

        // Copy remaining negatives
        while (negIndex < neg.size())
            arr[i++] = neg[negIndex++];
    }
};
```

---

# Step 1: Separate Positive and Negative Numbers

Input

```text
arr = [1, 2, 3, -4, -1, 4]
```

### Traverse the array

```
             +-------------------------+
             |      Original Array     |
             +-------------------------+

        1   2   3   -4   -1   4
        |   |   |    |    |   |
        |   |   |    |    |   |
        ▼   ▼   ▼    ▼    ▼   ▼

 Positive Vector      Negative Vector

 +---------------+    +-------------+
 | 1 | 2 | 3 | 4 |    | -4 | -1 |
 +---------------+    +-------------+
```

After traversal

```text
pos = [1,2,3,4]
neg = [-4,-1]
```

---

# Step 2: Initialize Indices

```
posIndex = 0
negIndex = 0
i = 0
```

Meaning

```
posIndex → Current Positive Element
negIndex → Current Negative Element
i        → Current Position in Original Array
```

---

# Step 3: Alternate Elements

## Iteration 1

```
arr[0] = pos[0] = 1
arr[1] = neg[0] = -4
```

Array becomes

```
+----+-----+---+---+---+---+
| 1  | -4  |   |   |   |   |
+----+-----+---+---+---+---+
```

Update

```
posIndex = 1
negIndex = 1
i = 2
```

---

## Iteration 2

```
arr[2] = pos[1] = 2
arr[3] = neg[1] = -1
```

Array becomes

```
+----+-----+----+-----+---+---+
| 1  | -4  | 2  | -1  |   |   |
+----+-----+----+-----+---+---+
```

Update

```
posIndex = 2
negIndex = 2
i = 4
```

Now

```
negIndex == neg.size()
```

So the alternating loop stops.

---

# Step 4: Copy Remaining Positives

Remaining positives

```
3
4
```

Copy them

```
arr[4] = 3
arr[5] = 4
```

Final Array

```
+----+-----+----+-----+----+----+
| 1  | -4  | 2  | -1  | 3  | 4  |
+----+-----+----+-----+----+----+
```

---

# Another Example

## Input

```text
[-1, -2, 5, 6, 7]
```

Separate

```
Positive = [5,6,7]

Negative = [-1,-2]
```

Alternating

```
5  -1  6  -2
```

Remaining

```
7
```

Output

```text
[5,-1,6,-2,7]
```

---

# Flow Diagram

```
                 Start
                    │
                    ▼
          Traverse Original Array
                    │
         ┌──────────┴──────────┐
         │                     │
         ▼                     ▼
 Positive Number?          Negative Number?
         │                     │
         ▼                     ▼
 Store in pos[]          Store in neg[]
         │                     │
         └──────────┬──────────┘
                    ▼
          Both Arrays Created
                    │
                    ▼
     Pick One Positive & One Negative
                    │
                    ▼
      One Array Finished?
          │          │
         No          Yes
          │          ▼
          │   Copy Remaining Elements
          │          │
          └──────────┘
                    ▼
                 Finished
```

---

# Dry Run

Input

```
1 2 3 -4 -1 4
```

After Separation

```
Positive → 1 2 3 4

Negative → -4 -1
```

Reconstruction

```
Step 1 → 1

Step 2 → 1 -4

Step 3 → 1 -4 2

Step 4 → 1 -4 2 -1

Remaining → 3 4
```

Output

```
1 -4 2 -1 3 4
```

---

# Complexity Analysis

| Operation | Complexity |
|-----------|------------|
| Separate positives & negatives | **O(N)** |
| Rearrange array | **O(N)** |
| **Overall Time** | **O(N)** |
| **Extra Space** | **O(N)** |

---

# Key Points

- ✅ Preserves the relative order of positive numbers.
- ✅ Preserves the relative order of negative numbers.
- ✅ Works even when positives and negatives are unequal.
- ✅ Easy to understand and implement.
- ✅ Avoids index out-of-bounds errors.
