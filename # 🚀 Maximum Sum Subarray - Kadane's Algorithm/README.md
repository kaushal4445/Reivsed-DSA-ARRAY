# 🚀 Maximum Sum Subarray - Kadane's Algorithm

![Algorithm](https://img.shields.io/badge/Algorithm-Kadane's%20Algorithm-blue)
![Language](https://img.shields.io/badge/Language-C%2B%2B-orange)
![Time](https://img.shields.io/badge/Time%20Complexity-O(n)-green)
![Space](https://img.shields.io/badge/Space%20Complexity-O(1)-green)

---

# 📌 Problem Statement

Given an integer array, find the **contiguous subarray** that has the largest sum.

Return the actual subarray elements.

---

## Example

### Input

```cpp
arr = {-2,1,-3,4,-1,2,1,-5,4}
```

### Output

```cpp
[4,-1,2,1]
```

### Explanation

The sum of this subarray is:

```
4 + (-1) + 2 + 1 = 6
```

No other contiguous subarray gives a larger sum.

---

# 💡 Idea Behind Kadane's Algorithm

The main idea:

> A negative running sum can never help us create a maximum sum in the future, so we discard it.

We maintain:

```
sum  → Current subarray sum

maxi → Maximum sum found so far

start → Starting index of current subarray

ansStart → Starting index of best subarray

ansEnd → Ending index of best subarray
```

---

# 🧠 Visualization

Example:

```
arr = {-2,1,-3,4,-1,2,1,-5,4}
```

Array:

```
Index:    0    1    2    3    4    5    6    7    8

Array:   -2    1   -3    4   -1    2    1   -5    4
```

---

# 🔥 Dry Run

## Step 1

Element:

```
-2
```

Current sum:

```
sum = -2
```

Diagram:

```
[-2]  1  -3  4  -1  2  1  -5  4
 ↑

Current Subarray
```

Since sum is negative:

```
Reset sum = 0
```

Reason:

A negative value will decrease future answers.

---

# Step 2

Element:

```
1
```

Start new subarray:

```
sum = 1
```

Diagram:

```
-2  [1]  -3  4  -1  2  1  -5  4
     ↑

Current Subarray
```

Maximum:

```
maxi = 1
```

---

# Step 3

Element:

```
-3
```

Add:

```
sum = 1 + (-3)

sum = -2
```

Diagram:

```
-2  [1 -3]  4  -1  2  1  -5  4
```

Negative sum:

```
Reset sum = 0
```

---

# Step 4

Element:

```
4
```

New start:

```
sum = 4
```

Diagram:

```
-2  1  -3  [4]  -1  2  1  -5  4
             ↑
```

Update:

```
maxi = 4
```

---

# Step 5

Element:

```
-1
```

Add:

```
sum = 4 + (-1)

sum = 3
```

Diagram:

```
-2  1  -3  [4 -1]  2  1  -5  4
```

Maximum remains:

```
maxi = 4
```

---

# Step 6

Element:

```
2
```

Add:

```
sum = 3 + 2

sum = 5
```

Diagram:

```
-2  1  -3  [4 -1 2]  1  -5  4
```

Update:

```
maxi = 5
```

---

# Step 7

Element:

```
1
```

Add:

```
sum = 5 + 1

sum = 6
```

Diagram:

```
-2  1  -3  [4 -1 2 1]  -5  4
```

New maximum:

```
maxi = 6
```

Store:

```
ansStart = 3
ansEnd = 6
```

---

# Step 8

Element:

```
-5
```

Sum:

```
6 - 5 = 1
```

Still positive, continue.

```
-2 1 -3 [4 -1 2 1 -5] 4
```

---

# Step 9

Element:

```
4
```

Sum:

```
1 + 4 = 5
```

No update because:

```
5 < 6
```

---

# Final Answer

Stored indexes:

```
ansStart = 3
ansEnd = 6
```

Subarray:

```
Index:

0   1   2    3    4    5    6   7   8

-2  1  -3   [4] [-1] [2] [1] -5  4
```

Result:

```cpp
[4,-1,2,1]
```

---

# 🔍 Why Does It Work?

Suppose:

```
[-5, 4]
```

Sum:

```
-5 + 4 = -1
```

Keeping `-5` is harmful.

Better:

```
[4]
```

Therefore:

```
If current sum < 0

Discard it
```

A negative prefix can never contribute to a future maximum.

---

# 💻 C++ Solution

```cpp
class Solution {
public:
    vector<int> findSubarray(vector<int>& arr) {

        long long sum = 0;
        long long maxi = INT_MIN;

        int start = 0;
        int ansStart = 0;
        int ansEnd = 0;


        for(int i = 0; i < arr.size(); i++) {

            if(sum == 0)
                start = i;


            sum += arr[i];


            if(sum > maxi) {

                maxi = sum;

                ansStart = start;
                ansEnd = i;

            }


            if(sum < 0) {

                sum = 0;

            }
        }


        vector<int> ans;


        for(int i = ansStart; i <= ansEnd; i++) {

            ans.push_back(arr[i]);

        }


        return ans;
    }
};
```

---

# 📊 Complexity Analysis

## Time Complexity

We traverse the array only once.

```
O(n)
```

---

## Space Complexity

Only variables are used.

```
O(1)
```

---

# 🏆 Key Takeaways

✅ Uses Kadane's Algorithm

✅ Finds maximum sum contiguous subarray

✅ Tracks starting and ending indexes

✅ Removes negative contribution automatically

✅ Runs in linear time

---

# Algorithm Summary

```
Start
  |
  ↓
Add current element
  |
  ↓
Is sum maximum?
  |
  ├── Yes → Store answer indexes
  |
  ↓
Is sum negative?
  |
  ├── Yes → Reset sum
  |
  ↓
Continue until array ends
```

## 🚀 Result

```
Maximum Sum Subarray

[-2,1,-3,4,-1,2,1,-5,4]

        ↓

[4,-1,2,1]

Sum = 6
```
