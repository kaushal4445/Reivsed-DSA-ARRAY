# Merge Intervals (LeetCode 56)

## Problem Statement

Given an array of intervals where `intervals[i] = [start, end]`, merge all overlapping intervals and return an array of the non-overlapping intervals.

### Example

```cpp
Input:
intervals = [[1,3],[2,6],[8,10],[15,18]]

Output:
[[1,6],[8,10],[15,18]]
```

---

# Solution

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {

        sort(intervals.begin(), intervals.end());

        vector<vector<int>> ans;

        for(auto interval : intervals){

            if(ans.empty() || ans.back()[1] < interval[0]){
                ans.push_back(interval);
            }
            else{
                ans.back()[1] = max(ans.back()[1], interval[1]);
            }
        }

        return ans;
    }
};
```

---

# Intuition

The main idea is:

1. Sort all intervals by their **starting point**.
2. Traverse each interval one by one.
3. If the current interval overlaps with the last merged interval,
   merge them.
4. Otherwise, simply add the current interval to the answer.

---

# Why Sorting?

Suppose the intervals are:

```text
[8,10] [1,3] [2,6]
```

Without sorting, we cannot determine which intervals should merge first.

After sorting:

```text
[1,3] [2,6] [8,10]
```

Now every possible overlapping interval appears next to each other.

Time Complexity of sorting:

```
O(n log n)
```

---

# Dry Run

## Input

```cpp
intervals = [[1,3],[2,6],[8,10],[15,18]]
```

---

## Step 1

Sort the intervals.

```text
Before Sorting

[1,3] [2,6] [8,10] [15,18]

↓

After Sorting

[1,3] [2,6] [8,10] [15,18]
```

Already sorted.

---

## Step 2

Initially

```text
ans = []
```

---

# Iteration 1

Current interval

```text
[1,3]
```

Since `ans` is empty,

```cpp
ans.push_back(interval);
```

Result

```text
ans

[1,3]
```

---

# Iteration 2

Current interval

```text
[2,6]
```

Current Answer

```text
[1,3]
```

Visual Diagram

```text
1------3
   2---------6
```

They overlap because

```
3 >= 2
```

So merge them.

```cpp
ans.back()[1] = max(3,6);
```

Result

```text
1-------------6
```

Now

```text
ans

[1,6]
```

---

# Iteration 3

Current interval

```text
[8,10]
```

Current merged interval

```text
[1,6]
```

Diagram

```text
1-------------6

             8------10
```

Check

```cpp
6 < 8
```

There is **no overlap**.

So push it.

```text
ans

[1,6]
[8,10]
```

---

# Iteration 4

Current interval

```text
[15,18]
```

Diagram

```text
1-------------6

8------10

               15------18
```

Check

```cpp
10 < 15
```

No overlap.

Push it.

Final Answer

```text
ans

[1,6]
[8,10]
[15,18]
```

---

# Understanding the if Condition

```cpp
if(ans.empty() || ans.back()[1] < interval[0])
```

This condition means

### Case 1

Answer is empty.

```text
ans = []
```

Simply insert the first interval.

---

### Case 2

No overlap.

Example

```text
Last Interval

1--------5

Current Interval

          7------9
```

Since

```
5 < 7
```

The intervals are separate.

So,

```cpp
ans.push_back(interval);
```

---

# Else Condition

```cpp
else{
    ans.back()[1] = max(ans.back()[1], interval[1]);
}
```

This means

The intervals overlap.

Example

```text
Last Interval

1---------5

Current

    3------------8
```

Both intervals intersect.

Merged interval becomes

```text
1----------------8
```

because

```cpp
max(5,8) = 8
```

---

# Another Example

Input

```cpp
[[1,4],[2,5],[3,8],[10,12]]
```

Sorted

```text
[1,4] [2,5] [3,8] [10,12]
```

---

## Step 1

```text
ans

[1,4]
```

---

## Step 2

```text
1---------4
   2----------5
```

Merge

```text
1-------------5
```

---

## Step 3

```text
1-------------5
      3--------------8
```

Merge again

```text
1----------------------8
```

---

## Step 4

```text
1----------------------8

                    10------12
```

No overlap.

Final Answer

```text
[1,8]
[10,12]
```

---

# Dry Run Table

| Current Interval | Last Interval in `ans` | Overlap? | Action | Result |
|-----------------|------------------------|----------|--------|--------|
| `[1,3]` | Empty | — | Push | `[1,3]` |
| `[2,6]` | `[1,3]` | ✅ Yes | Merge | `[1,6]` |
| `[8,10]` | `[1,6]` | ❌ No | Push | `[1,6],[8,10]` |
| `[15,18]` | `[8,10]` | ❌ No | Push | `[1,6],[8,10],[15,18]` |

---

# Time Complexity

### Sorting

```
O(n log n)
```

### Traversing

```
O(n)
```

### Overall

```
O(n log n)
```

---

# Space Complexity

The answer vector stores the merged intervals.

Worst case (no intervals overlap):

```
O(n)
```

---

# Key Takeaways

- ✔ Sort intervals by starting point.
- ✔ Compare the current interval with the last merged interval.
- ✔ If they overlap, extend the ending point.
- ✔ Otherwise, create a new interval.
- ✔ This greedy approach guarantees the optimal solution in **O(n log n)** time.
