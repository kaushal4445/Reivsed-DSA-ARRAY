# 🚀 Maximum Subarray Sum - Kadane's Algorithm

![Algorithm](https://img.shields.io/badge/Algorithm-Kadane's%20Algorithm-blue)
![Language](https://img.shields.io/badge/Language-C%2B%2B-orange)
![Time Complexity](https://img.shields.io/badge/Time-O(n)-green)
![Space Complexity](https://img.shields.io/badge/Space-O(1)-green)

---

# 📌 Problem Statement

Given an integer array `nums`, find the **contiguous subarray** that has the largest sum.

Return the maximum possible sum.

---

# Example

## Input

```cpp
nums = [-2,1,-3,4,-1,2,1,-5,4]
```

## Output

```text
6
```

## Explanation

The subarray:

```
[4,-1,2,1]
```

has the maximum sum.

Calculation:

```
4 + (-1) + 2 + 1 = 6
```

Therefore:

```
Maximum Subarray Sum = 6
```

---

# 💡 Approach - Kadane's Algorithm

The idea is simple:

At every index, we decide:

1. Continue the previous subarray.
2. Start a new subarray from the current element.

If the current sum becomes negative, we discard it because a negative sum will reduce the future answer.

---

# 🔑 Variables Used

```cpp
int maxi;
```

Stores the maximum sum found so far.

---

```cpp
int sum;
```

Stores the current running sum.

---

# 🧠 Algorithm Steps

```
1. Initialize:

   sum = 0
   maxi = INT_MIN


2. Traverse the array.


3. Add current element to sum.


4. Update maximum:

   maxi = max(maxi, sum)


5. If sum becomes negative:

   Reset sum = 0


6. Return maxi.
```

---

# 🔥 Visualization

Example:

```
nums = [-2,1,-3,4,-1,2,1,-5,4]
```

Initial:

```
sum = 0
maxi = -∞
```

---

## Step 1

Current element:

```
-2
```

Add:

```
sum = 0 + (-2)

sum = -2
```

Diagram:

```
[-2]  1  -3  4  -1  2  1  -5  4
 ↑
Current
```

Update:

```
maxi = -2
```

Since:

```
sum < 0
```

Reset:

```
sum = 0
```

---

## Step 2

Element:

```
1
```

Add:

```
sum = 1
```

Diagram:

```
-2  [1]  -3  4  -1  2  1  -5  4
```

Update:

```
maxi = 1
```

---

## Step 3

Element:

```
-3
```

Add:

```
sum = 1 + (-3)

sum = -2
```

Negative:

```
Reset sum = 0
```

---

## Step 4

Element:

```
4
```

Add:

```
sum = 4
```

Diagram:

```
-2 1 -3 [4] -1 2 1 -5 4
```

Update:

```
maxi = 4
```

---

## Step 5

Element:

```
-1
```

Sum:

```
4 + (-1) = 3
```

```
maxi = 4
```

---

## Step 6

Element:

```
2
```

Sum:

```
3 + 2 = 5
```

Update:

```
maxi = 5
```

---

## Step 7

Element:

```
1
```

Sum:

```
5 + 1 = 6
```

Update:

```
maxi = 6
```

Current subarray:

```
[4,-1,2,1]
```

---

## Step 8

Element:

```
-5
```

Sum:

```
6 - 5 = 1
```

No update.

---

## Step 9

Element:

```
4
```

Sum:

```
1 + 4 = 5
```

Still:

```
maxi = 6
```

---

# Final Answer

Maximum sum:

```
6
```

From subarray:

```
[4,-1,2,1]
```

---

# 📊 Algorithm Visualization

```
                 Kadane's Algorithm


        Add Current Element
                 |
                 ↓
        Calculate Running Sum
                 |
                 ↓
        Is sum > maxi ?
              /      \
            Yes       No
             |         |
             ↓         |
       Update maxi     |
                       |
                 Is sum < 0 ?
                       |
                  Yes  |
                   |
                   ↓
              Reset sum = 0
```

---

# 💻 C++ Solution

```cpp
class Solution {
public:

    int maxSubArray(vector<int>& nums) {

        int maxi = INT_MIN;
        int sum = 0;


        for(int i = 0; i < nums.size(); i++) {

            sum = sum + nums[i];


            if(sum > maxi) {

                maxi = sum;

            }


            if(sum < 0) {

                sum = 0;

            }
        }


        return maxi;
    }
};
```

---

# ⏱️ Complexity Analysis

## Time Complexity

The array is traversed once.

```
O(n)
```

---

## Space Complexity

Only two variables are used.

```
O(1)
```

---

# ❓ Why Reset Sum When It Becomes Negative?

Example:

```
[-5, 4]
```

Current sum:

```
-5
```

Adding it with future numbers:

```
-5 + 4 = -1
```

is worse than starting from:

```
4
```

Therefore:

```
Negative sum is useless.
Discard it.
```

---

# ⭐ Key Takeaways

✅ Uses Kadane's Algorithm

✅ Finds maximum contiguous subarray sum

✅ One pass solution

✅ No extra memory required

✅ Optimal O(n) approach

---

# 🎯 Pattern To Remember

```
Keep adding elements.

If current sum is maximum:
    update answer.

If current sum becomes negative:
    restart from zero.
```

🚀 **Kadane's Algorithm converts a brute force O(n²) solution into an efficient O(n) solution.**
