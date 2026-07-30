# 🗳️ Majority Element - Moore's Voting Algorithm

![Algorithm](https://img.shields.io/badge/Algorithm-Moore's%20Voting-blue)
![Language](https://img.shields.io/badge/Language-C%2B%2B-orange)
![Complexity](https://img.shields.io/badge/Time-O(n)-green)
![Space](https://img.shields.io/badge/Space-O(1)-green)

---

# 📌 Problem Statement

Given an array `nums` of size `n`, find the element that appears **more than n/2 times**.

The majority element always occurs more than half of the array size.

### Example

```
Input:

nums = [2,2,1,1,1,2,2]


Output:

2
```

### Explanation

```
2 appears = 4 times

Array size = 7

n/2 = 7/2 = 3

4 > 3 ✅

Therefore answer = 2
```

---

# 💡 Intuition

Think of every number as a person voting for a candidate.

- Same number → vote increases
- Different number → one vote cancels another vote

The majority element has more votes than all other elements combined, so it will survive after cancellation.

---

# 🧠 Moore's Voting Algorithm

We maintain two variables:

```
candidate → Current possible majority element

count     → Number of votes
```

---

# 🎯 Algorithm

```
1. Start count = 0

2. Traverse the array

3. If count == 0
       Choose current element as candidate
       Increase count

4. If current element == candidate
       Increase count

5. Otherwise
       Decrease count

6. Verify candidate by counting its frequency
```

---

# 🔥 Visualization

Example:

```
nums = [2,2,1,1,1,2,2]
```

Initial:

```
candidate = ?
count = 0
```

---

## Step 1

Element = 2

count is zero, so select candidate.

```
Candidate = 2
Count = 1
```

Diagram:

```
[2] 2 1 1 1 2 2
 ↑

Candidate = 2
Count = 1
```

---

## Step 2

Element = 2

Same as candidate.

Increase count.

```
Candidate = 2
Count = 2
```

Diagram:

```
2 [2] 1 1 1 2 2
   ↑

2 supports 2
```

---

## Step 3

Element = 1

Different element.

Cancel one vote.

```
Count:

2 → 1
```

Diagram:

```
2 2 [1] 1 1 2 2
     ↑

2 and 1 cancel
```

---

## Step 4

Element = 1

Again different.

```
Count:

1 → 0
```

Diagram:

```
2 2 1 [1] 1 2 2
       ↑

Count becomes 0
```

The current candidate loses all votes.

---

## Step 5

Element = 1

Count is zero.

Choose new candidate.

```
Candidate = 1
Count = 1
```

Diagram:

```
2 2 1 1 [1] 2 2
         ↑

New Candidate
```

---

## Step 6

Element = 2

Different.

Cancel.

```
Count:

1 → 0
```

---

## Step 7

Element = 2

Count is zero.

Choose new candidate.

```
Candidate = 2
Count = 1
```

---

# Final Candidate

```
Candidate = 2
```

Now verify:

```
Array:

2 2 1 1 1 2 2

Frequency of 2 = 4

n/2 = 3

4 > 3 ✅
```

Answer:

```
2
```

---

# 🧩 Why Does It Work?

The majority element appears more than half of the time.

Example:

```
[2,2,2,1,1]

Majority = 2
```

Cancel different pairs:

```
2 2 2 1 1

Remove:

2 + 1

2 + 1


Remaining:

2
```

The majority element cannot be completely removed.

It always remains as the final candidate.

---

# 📊 Algorithm Visualization

```
Before Cancellation:

2 2 1 1 1 2 2


Cancel opposite votes:

(2,1)
(2,1)


Remaining:

2 1 2


Cancel again:

(2,1)


Remaining:

2
```

Survivor:

```
Majority Element = 2
```

---

# 💻 C++ Solution

```cpp
class Solution {
public:

    int majorityElement(vector<int>& nums) {

        int n = nums.size();

        int count = 0;
        int candidate;


        // Moore's Voting Algorithm
        for(int i = 0; i < n; i++) {

            if(count == 0) {

                candidate = nums[i];
                count = 1;

            }
            else if(candidate == nums[i]) {

                count++;

            }
            else {

                count--;

            }
        }


        // Verification step
        int frequency = 0;

        for(int i = 0; i < n; i++) {

            if(nums[i] == candidate)
                frequency++;

        }


        if(frequency > n/2)
            return candidate;


        return -1;
    }
};
```

---

# 📝 Dry Run Table

Example:

```
nums = [2,2,1,1,1,2,2]
```

| Index | Value | Candidate | Count | Action |
|---|---|---|---|---|
|0|2|2|1|New candidate|
|1|2|2|2|Same → increase|
|2|1|2|1|Cancel|
|3|1|2|0|Cancel|
|4|1|1|1|New candidate|
|5|2|1|0|Cancel|
|6|2|2|1|New candidate|

Final:

```
Candidate = 2
```

---

# ⏱️ Complexity Analysis

## Time Complexity

Two traversals:

```
Finding candidate  → O(n)

Verification       → O(n)
```

Total:

```
O(n)
```

---

## Space Complexity

Only two variables:

```
candidate
count
```

Therefore:

```
O(1)
```

---

# ⭐ Key Points

✅ Uses Moore's Voting Algorithm

✅ No extra array or hashmap required

✅ Works in linear time

✅ Constant memory

✅ Very common interview problem

---

# 🚀 Learning Summary

The main idea:

```
Different elements cancel each other.

The element with more than n/2 frequency
cannot be cancelled completely.

The survivor is the majority element.
```

```
Majority Element
        |
        ↓
Moore's Voting Algorithm
        |
        ↓
O(n) Time + O(1) Space
```
