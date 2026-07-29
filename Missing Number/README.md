# 🔍 Missing Number in Array (GFG) | XOR Approach

<p align="center">
  <img src="https://img.shields.io/badge/Language-C%2B%2B-blue.svg" />
  <img src="https://img.shields.io/badge/Algorithm-XOR-red.svg" />
  <img src="https://img.shields.io/badge/Time%20Complexity-O(n)-brightgreen.svg" />
  <img src="https://img.shields.io/badge/Space%20Complexity-O(1)-orange.svg" />
</p>

---

# 🚀 Problem Statement

You are given an array containing **N-1 numbers** from the range:

```
1 to N
```

One number is missing.

Your task is to find the missing number.

---

## Example

### Input

```
arr = [1,2,4,5]
```

### Complete Range

```
1 2 3 4 5
```

### Missing Number

```
3
```

### Output

```
3
```

---

# 💡 Approach: XOR Method

Instead of using:

- ❌ Sorting
- ❌ Extra HashMap
- ❌ Sum Formula (possible overflow)

We use the **XOR trick**.

---

# 🧠 XOR Properties

XOR (`^`) follows two important rules:

## Rule 1: Same numbers cancel

```
a ^ a = 0
```

Example:

```
5 ^ 5

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

## Rule 2: Number with zero remains same

```
a ^ 0 = a
```

Example:

```
5 ^ 0

101
000
---
101
```

Result:

```
5
```

---

# 🔥 Main Idea

We XOR:

```
All numbers from 1 to N
```

with

```
All numbers present in array
```

The common numbers cancel each other.

Only the missing number remains.

---

# 🎯 Visualization

Example:

```
Array:

[1,2,4,5]


Numbers should be:

[1,2,3,4,5]
```

---

## Step 1: XOR Expected Numbers

```
1 ^ 2 ^ 3 ^ 4 ^ 5
```

## Step 2: XOR Given Array

```
1 ^ 2 ^ 4 ^ 5
```

---

## Combine Both

```
(1 ^ 2 ^ 3 ^ 4 ^ 5)
              ^
(1 ^ 2 ^    4 ^ 5)
```

Cancel same values:

```
1 cancels 1

2 cancels 2

4 cancels 4

5 cancels 5
```

Remaining:

```
3
```

🎉 Missing Number = 3

---

# 📝 Dry Run Step By Step

## Input

```
arr = [1,2,4,5]

N = 5
```

---

## Initial Values

```
xor1 = 0
xor2 = 0
```

Diagram:

```
xor1
 |
 v
0


xor2
 |
 v
0
```

---

# 🔹 Iteration 1

Value:

```
arr[0] = 1
```

Update:

```
xor2 = xor2 ^ arr[i]

xor2 = 0 ^ 1
```

Result:

```
xor2 = 1
```

Expected number:

```
xor1 = 0 ^ 1

xor1 = 1
```

---

# 🔹 Iteration 2

Value:

```
arr[1] = 2
```

Update:

```
xor2 = 1 ^ 2

001
010
---
011
```

```
xor2 = 3
```

Expected:

```
xor1 = 1 ^ 2

001
010
---
011
```

```
xor1 = 3
```

---

# 🔹 Iteration 3

Value:

```
arr[2] = 4
```

```
xor2 = 3 ^ 4


011
100
---
111
```

```
xor2 = 7
```

Expected:

```
xor1 = 3 ^ 3

011
011
---
000
```

```
xor1 = 0
```

---

# 🔹 Iteration 4

Value:

```
arr[3] = 5
```

Array XOR:

```
xor2 = 7 ^ 5


111
101
---
010
```

```
xor2 = 2
```

Expected XOR:

```
xor1 = 0 ^ 4

xor1 = 4
```

---

# Add Last Number N

```cpp
xor1 = xor1 ^ N;
```

Here:

```
N = 5
```

So:

```
xor1 = 4 ^ 5


100
101
---
001
```

```
xor1 = 1
```

---

# Final XOR

```cpp
return xor1 ^ xor2;
```

Values:

```
xor1 = 1

xor2 = 2
```

Operation:

```
1 ^ 2


001
010
---
011
```

Answer:

```
3
```

---

# 🔄 Complete Flow Diagram

```
              Start
                |
                v
        Find Array Size
                |
                v
          Calculate N
                |
                v
     ----------------------
     |                    |
     v                    v

 XOR Array Values     XOR 1 to N Values

     |                    |
     ----------------------
                |
                v
          XOR Both Results
                |
                v
       Missing Number Found
```

---

# 💻 C++ Solution

```cpp
class Solution {
public:
    int missingNum(vector<int>& arr) {

        int n = arr.size();

        int N = n + 1;

        int xor1 = 0;
        int xor2 = 0;


        for(int i = 0; i < n; i++)
        {
            // XOR array elements
            xor2 = xor2 ^ arr[i];

            // XOR numbers 1 to N-1
            xor1 = xor1 ^ (i + 1);
        }


        // Include N
        xor1 = xor1 ^ N;


        // Missing number
        return xor1 ^ xor2;
    }
};
```

---

# 📊 Complexity Analysis

| Type | Complexity |
|------|------------|
| Time Complexity | O(n) |
| Space Complexity | O(1) |

---

# ⚡ Why XOR is Better?

| Approach | Time | Space | Problem |
|---|---|---|---|
| Sorting | O(n log n) | O(1) | Slower |
| HashMap | O(n) | O(n) | Extra memory |
| Sum Formula | O(n) | O(1) | Integer overflow risk |
| XOR | O(n) | O(1) | ✅ Best |

---

# 🧠 Memory Trick

Remember:

```
FULL RANGE
     XOR
ARRAY VALUES
     =
MISSING NUMBER
```

or simply:

```
EXPECTED ^ PRESENT = ANSWER
```

---

# ✅ Key Points

✔️ XOR removes duplicate values automatically.  
✔️ No extra data structure required.  
✔️ Works in linear time.  
✔️ Uses constant memory.  
✔️ Safe from integer overflow.  

---

<div align="center">

# ⭐ If this explanation helped you, give the repository a star!

## Happy Coding 🚀

</div>
