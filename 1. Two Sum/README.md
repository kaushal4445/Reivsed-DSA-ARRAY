# 🔹 Two Sum - Brute Force (C++)

## 📌 Problem Statement

Given an array of integers `nums` and an integer `target`, return the **indices** of the two numbers such that they add up to the target.

You may assume that:

- Exactly one solution exists.
- You may not use the same element twice.
- Return the indices in any order.

---

## Example

### Input

```cpp
nums = {2, 7, 11, 15}
target = 9
```

### Output

```cpp
{0, 1}
```

### Explanation

```text
nums[0] + nums[1]
   2    +    7 = 9
```

Therefore, return:

```cpp
{0,1}
```

---

# 💡 Approach (Brute Force)

The idea is very simple.

- Pick the first element.
- Compare it with every element after it.
- If their sum equals the target, return their indices.

Since every possible pair is checked, the solution is guaranteed to find the answer.

---

# 🧠 Visualization

Given

```text
nums = [2, 7, 11, 15]
target = 9
```

## Step 1

Choose the first element.

```text
Index :   0   1   2   3
Array :  [2]  7  11  15
           ↑
           i
```

Now compare with every element after it.

---

### Compare with j = 1

```text
2 + 7 = 9 ✅
```

```text
Index :   0   1
Array :  [2] [7]

2 + 7 = 9
```

Target found.

Return

```cpp
{0,1}
```

The algorithm stops here.

---

# Another Example

```cpp
nums = {3,2,4}
target = 6
```

## Iteration 1

```text
3 + 2 = 5 ❌
3 + 4 = 7 ❌
```

No answer.

---

## Iteration 2

Move to the next element.

```text
Index :   0   1   2
Array :   3  [2] [4]
              ↑
              i
```

Compare

```text
2 + 4 = 6 ✅
```

Return

```cpp
{1,2}
```

---

# Dry Run

Example

```cpp
nums = {2,7,11,15}
target = 9
```

### i = 0

| j | nums[i] | nums[j] | Sum | Result |
|---|----------|----------|-----|--------|
|1|2|7|9|✅ Found|

Return

```cpp
{0,1}
```

---

# Algorithm

```
for each i
    for each j = i+1
        if nums[i] + nums[j] == target
            return {i,j}
```

---

# C++ Solution

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {

        for(int i = 0; i < nums.size(); i++) {

            for(int j = i + 1; j < nums.size(); j++) {

                if(nums[i] + nums[j] == target) {
                    return {i, j};
                }

            }

        }

        return {};
    }
};
```

---

# Complexity Analysis

## Time Complexity

There are two nested loops.

```
Outer loop  -> n
Inner loop  -> n
```

Total

```
O(n²)
```

---

## Space Complexity

No extra data structure is used.

```
O(1)
```

---

# Why does this work?

The algorithm checks **every possible pair**.

For an array of size `n`, the possible pairs are

```text
(0,1)
(0,2)
(0,3)
...

(1,2)
(1,3)

...

(n-2,n-1)
```

Since every pair is examined exactly once, if a valid pair exists, it will definitely be found.

---

# Pros

✅ Very easy to understand

✅ Easy to implement

✅ Good for beginners

---

# Cons

❌ Slow for large arrays

Time Complexity is **O(n²)**.

A better solution uses a **Hash Map** and solves the problem in **O(n)** time.
