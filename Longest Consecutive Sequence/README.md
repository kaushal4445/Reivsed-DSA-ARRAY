# Longest Consecutive Sequence (Better Approach)

## Problem Statement

Given an unsorted array of integers, find the length of the **longest consecutive sequence**.

A consecutive sequence means numbers appear one after another.

Example:

Input

```text
[100,4,200,1,3,2]
```

Output

```text
4
```

Because the longest consecutive sequence is

```text
1 → 2 → 3 → 4
```

---

# Code

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {

        int n = nums.size();

        if(n == 0)
            return 0;

        sort(nums.begin(), nums.end());

        int lastSmaller = INT_MIN;
        int cnt = 0;
        int longest = 1;

        for(int i=0;i<n;i++){

            if(nums[i]-1 == lastSmaller){

                cnt++;
                lastSmaller = nums[i];

            }

            else if(nums[i] != lastSmaller){

                cnt = 1;
                lastSmaller = nums[i];

            }

            longest = max(longest,cnt);
        }

        return longest;
    }
};
```

---

# Idea

The algorithm works in **3 simple steps**

```
Original Array

        │
        ▼

Sort the Array

        │
        ▼

Traverse One by One

        │
        ▼

Current Number Consecutive ?

      Yes            No
       │              │
       ▼              ▼

Increase Count   Start New Sequence

        │
        ▼

Update Longest
```

---

# Example

Input

```text
nums = [100,4,200,1,3,2]
```

---

# Step 1 : Sort the Array

Original

```
100   4   200   1   3   2
```

↓

After Sorting

```
1   2   3   4   100   200
```

Now consecutive numbers become neighbors.

---

# Variables

```
lastSmaller = -∞

cnt = 0

longest = 1
```

Meaning

| Variable | Purpose |
|----------|---------|
| lastSmaller | Previous number |
| cnt | Current consecutive sequence length |
| longest | Maximum sequence found |

---

# Iteration 1

Current Number

```
1
```

Check

```
1-1 == -∞ ?

0 == -∞

False
```

So start a new sequence.

```
cnt = 1

lastSmaller = 1
```

Diagram

```
1

Sequence

1
```

Longest

```
1
```

---

# Iteration 2

Current Number

```
2
```

Check

```
2-1 == 1

True
```

So it is consecutive.

Increase count.

```
cnt = 2

lastSmaller = 2
```

Diagram

```
1 → 2
```

Longest

```
2
```

---

# Iteration 3

Current Number

```
3
```

Check

```
3-1 == 2

True
```

Diagram

```
1 → 2 → 3
```

```
cnt = 3
```

Longest

```
3
```

---

# Iteration 4

Current Number

```
4
```

Check

```
4-1 == 3

True
```

Diagram

```
1 → 2 → 3 → 4
```

```
cnt = 4
```

Longest

```
4
```

---

# Iteration 5

Current Number

```
100
```

Check

```
100-1 == 4 ?

99 == 4

False
```

Not consecutive.

Start a new sequence.

```
100
```

```
cnt = 1

lastSmaller = 100
```

Longest remains

```
4
```

---

# Iteration 6

Current Number

```
200
```

Check

```
200-1 == 100

199 ==100

False
```

Again,

```
New Sequence

200
```

Longest

```
4
```

---

# Final Answer

```
Longest = 4
```

Sequence

```
1 → 2 → 3 → 4
```

---

# Dry Run Table

| i | nums[i] | Consecutive? | cnt | longest |
|---|----------|-------------|-----|----------|
|0|1|No|1|1|
|1|2|Yes|2|2|
|2|3|Yes|3|3|
|3|4|Yes|4|4|
|4|100|No|1|4|
|5|200|No|1|4|

---

# How Duplicate Numbers are Handled

Example

```
1 2 2 3 4
```

After Sorting

```
1 2 2 3 4
```

When second **2** comes

```
nums[i] == lastSmaller
```

Condition

```cpp
else if(nums[i] != lastSmaller)
```

becomes false.

So duplicate is ignored.

Diagram

```
1 → 2

      2 (Duplicate)

Ignored

Continue

↓

3

↓

4
```

Final Sequence

```
1 → 2 → 3 → 4
```

Length

```
4
```

---

# Complete Visualization

```
               Start

                 │

                 ▼

         Sort the Array

                 │

                 ▼

      Traverse Each Number

                 │

                 ▼

Is Current Number = Previous + 1 ?

        ┌──────────────┐
        │              │
       Yes             No
        │              │
        ▼              ▼

Increase Count    New Sequence

        │              │
        └──────┬───────┘
               ▼

Update Maximum Length

               │

               ▼

Return Answer
```

---

# Why Sorting?

Without sorting

```
100 4 200 1 3 2
```

It is impossible to know consecutive numbers easily.

After sorting

```
1 2 3 4 100 200
```

Now consecutive numbers become adjacent.

---

# Complexity Analysis

Sorting

```
O(N log N)
```

Traversal

```
O(N)
```

Overall

```
O(N log N)
```

Space

```
O(1)
```

(ignoring sorting's internal space)

---

# Key Points

✅ Sort the array first.

✅ Compare every element with the previous one.

✅ If current = previous + 1 → increase count.

✅ If duplicate → ignore it.

✅ Otherwise → start a new sequence.

✅ Keep updating the maximum sequence length.

Time Complexity

```
O(N log N)
```

Space Complexity

```
O(1)
```
