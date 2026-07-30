# 🔄 Rearrange Array Elements by Sign

![Algorithm](https://img.shields.io/badge/Algorithm-Array%20Manipulation-blue)
![Language](https://img.shields.io/badge/Language-C%2B%2B-orange)
![Time Complexity](https://img.shields.io/badge/Time-O(n)-green)
![Space Complexity](https://img.shields.io/badge/Space-O(n)-green)

---

# 📌 Problem Statement

Given an array containing **positive and negative numbers**, rearrange the elements such that:

- Positive numbers are placed at **even indexes**.
- Negative numbers are placed at **odd indexes**.
- The relative order of positive and negative numbers remains the same.

---

# Example

## Input

```cpp
nums = [3,1,-2,-5,2,-4]
```

## Output

```text
[3,-2,1,-5,2,-4]
```

---

# 💡 Intuition

We need two separate positions:

```
Even Index  → Positive Numbers

Odd Index   → Negative Numbers
```

Example:

```
Index:

 0   1   2   3   4   5

[ + , - , + , - , + , - ]
```

So we maintain two pointers:

```
PositiveIndex → points to next even position

NegativeIndex → points to next odd position
```

---

# 🧠 Variables Used

## Positive Index

```cpp
int PositiveIndex = 0;
```

Starts from index `0`.

Because:

```
0,2,4,6...
```

are even positions.

---

## Negative Index

```cpp
int NegativeIndex = 1;
```

Starts from index `1`.

Because:

```
1,3,5,7...
```

are odd positions.

---

# 🔥 Dry Run Example

Input:

```
nums = [3,1,-2,-5,2,-4]
```

Initial result array:

```
ans = [0,0,0,0,0,0]


PositiveIndex = 0

NegativeIndex = 1
```

---

# Step 1

Element:

```
3
```

It is positive.

Place at PositiveIndex.

```
ans[0] = 3
```

Diagram:

```
Index:

 0   1   2   3   4   5

[3]  0   0   0   0   0
 ↑
PositiveIndex
```

Move:

```
PositiveIndex += 2
```

Now:

```
PositiveIndex = 2
```

---

# Step 2

Element:

```
1
```

Positive.

Place:

```
ans[2] = 1
```

Diagram:

```
 0   1   2   3   4   5

[3]  0  [1]  0   0   0
             ↑
       PositiveIndex
```

Move:

```
PositiveIndex = 4
```

---

# Step 3

Element:

```
-2
```

Negative.

Place at NegativeIndex.

```
ans[1] = -2
```

Diagram:

```
 0   1   2   3   4   5

[3] [-2] [1] 0  0   0
      ↑
 NegativeIndex
```

Move:

```
NegativeIndex = 3
```

---

# Step 4

Element:

```
-5
```

Negative.

Place:

```
ans[3] = -5
```

Diagram:

```
[3] [-2] [1] [-5] 0 0
```

Move:

```
NegativeIndex = 5
```

---

# Step 5

Element:

```
2
```

Positive.

Place:

```
ans[4] = 2
```

Diagram:

```
[3] [-2] [1] [-5] [2] 0
```

Move:

```
PositiveIndex = 6
```

---

# Step 6

Element:

```
-4
```

Negative.

Place:

```
ans[5] = -4
```

Final:

```
[3,-2,1,-5,2,-4]
```

---

# 📊 Visualization

Input:

```
+   +   -   -   +   -

3   1  -2  -5   2  -4
```

Separate:

```
Positive:

3   1   2


Negative:

-2  -5  -4
```

Place alternately:

```
Index:

0    1    2    3    4    5

+    -    +    -    +    -

3   -2    1   -5    2   -4
```

---

# 💻 C++ Solution

```cpp
class Solution {
public:

    vector<int> rearrangeArray(vector<int>& nums) {

        int n = nums.size();


        vector<int> ans(n,0);


        int PositiveIndex = 0;
        int NegativeIndex = 1;


        for(int i = 0; i < n; i++) {


            if(nums[i] < 0) {

                ans[NegativeIndex] = nums[i];

                NegativeIndex += 2;

            }

            else {

                ans[PositiveIndex] = nums[i];

                PositiveIndex += 2;

            }
        }


        return ans;
    }
};
```

---

# ⏱️ Complexity Analysis

## Time Complexity

We traverse the array once.

```
O(n)
```

---

## Space Complexity

Extra result array:

```
O(n)
```

---

# ⭐ Key Points

✅ Uses two pointers

✅ Maintains relative order

✅ Positive numbers go to even indexes

✅ Negative numbers go to odd indexes

✅ Simple one-pass solution

---

# 🧠 Pattern To Remember

```
Positive number found:

    Place at even index
    Move +2


Negative number found:

    Place at odd index
    Move +2
```

Visual:

```
Positive → 0 → 2 → 4 → 6

Negative → 1 → 3 → 5 → 7
```

---

# 🚀 Final Result

Input:

```
[3,1,-2,-5,2,-4]
```

Process:

```
Positive positions:

0,2,4

Negative positions:

1,3,5
```

Output:

```
[3,-2,1,-5,2,-4]
```
