# 🔗 Union of Two Arrays (GFG) - Using Set

<p align="center">
  <img src="https://img.shields.io/badge/Language-C%2B%2B-blue.svg" />
  <img src="https://img.shields.io/badge/Algorithm-Set%20Based-red.svg" />
  <img src="https://img.shields.io/badge/Time-O((n%2Bm)log(n%2Bm))-brightgreen.svg" />
  <img src="https://img.shields.io/badge/Space-O(n%2Bm)-orange.svg" />
</p>

---

# 📌 Problem Statement

Given two arrays `a[]` and `b[]`, find the **union** of both arrays.

The union contains:

- All unique elements from both arrays.
- No duplicate values.

---

# 📝 Example

## Input

```text
a = [1,2,3,4,5]

b = [2,3,6,7]
```

## Output

```text
[1,2,3,4,5,6,7]
```

---

# 💡 What is Union?

Union means combining two arrays and keeping only **unique elements**.

Example:

```
Array A

1 2 3 4 5


Array B

2 3 6 7
```

Combine:

```
1 2 3 4 5 2 3 6 7
```

Remove duplicates:

```
1 2 3 4 5 6 7
```

---

# 🚀 Approach: Using Set

A `set` automatically:

✅ Stores unique values  
✅ Removes duplicates  
✅ Keeps elements sorted (ascending order)

---

# 🔍 Algorithm

### Step 1

Create an empty set.

```cpp
set<int> st;
```

---

### Step 2

Insert all elements of first array into the set.

```cpp
for(int i = 0; i < n; i++)
{
    st.insert(a[i]);
}
```

---

### Step 3

Insert all elements of second array into the set.

```cpp
for(int i = 0; i < m; i++)
{
    st.insert(b[i]);
}
```

Duplicate values are automatically ignored.

---

### Step 4

Convert the set into a vector.

```cpp
vector<int> unionArr(st.begin(), st.end());
```

Return the answer.

---

# 📝 Dry Run With Diagram

## Input

```
a = [1,2,3,4,5]

b = [2,3,6,7]
```

---

# 🔹 Step 1: Create Empty Set

```
set

+---+
|   |
+---+
```

---

# 🔹 Step 2: Insert Array A Elements

Array A:

```
1  2  3  4  5
```

Insert one by one:

```
Insert 1

Set:

+---+
| 1 |
+---+


Insert 2

+---+---+
| 1 | 2 |
+---+---+


Insert 3

+---+---+---+
| 1 | 2 | 3 |
+---+---+---+


Insert 4

+---+---+---+---+
| 1 | 2 | 3 | 4 |
+---+---+---+---+


Insert 5

+---+---+---+---+---+
| 1 | 2 | 3 | 4 | 5 |
+---+---+---+---+---+
```

---

# 🔹 Step 3: Insert Array B Elements

Array B:

```
2 3 6 7
```

Insert 2:

```
2 already exists ❌

No change
```

Set:

```
1 2 3 4 5
```

---

Insert 3:

```
3 already exists ❌
```

No change.

---

Insert 6:

```
6 is new ✅
```

Set:

```
1 2 3 4 5 6
```

---

Insert 7:

```
7 is new ✅
```

Set:

```
1 2 3 4 5 6 7
```

---

# 🎯 Final Set

```
+---+---+---+---+---+---+---+
| 1 | 2 | 3 | 4 | 5 | 6 | 7 |
+---+---+---+---+---+---+---+
```

---

# 🔄 Convert Set to Vector

Code:

```cpp
vector<int> unionArr(st.begin(), st.end());
```

Conversion:

```
Set

1 2 3 4 5 6 7

        ↓

Vector

[1,2,3,4,5,6,7]
```

---

# 🎯 Complete Visualization

```
Array A

1 2 3 4 5
    |
    |
    ▼

        Insert

        ↓

Set

1 2 3 4 5


Array B

2 3 6 7
    |
    |
    ▼

        Insert

        ↓

Set

1 2 3 4 5 6 7


        ↓

Convert

        ↓


Union Array

[1,2,3,4,5,6,7]
```

---

# 💻 C++ Solution

```cpp
class Solution {
public:
    vector<int> findUnion(vector<int> &a, vector<int> &b) {

        set<int> st;

        int n = a.size();
        int m = b.size();

        // Insert elements from first array
        for(int i = 0; i < n; i++) {
            st.insert(a[i]);
        }

        // Insert elements from second array
        for(int i = 0; i < m; i++) {
            st.insert(b[i]);
        }

        // Convert set to vector
        vector<int> unionArr(st.begin(), st.end());

        return unionArr;
    }
};
```

---

# 🧠 How Code Works

## Create Set

```cpp
set<int> st;
```

Initially:

```
st = {}
```

---

## Insert First Array

Example:

```
a = [1,2,2,3]
```

Insert:

```
1 → {1}

2 → {1,2}

2 → Already Exists

3 → {1,2,3}
```

Duplicates are removed automatically.

---

## Insert Second Array

Example:

```
b = [2,4,5]
```

Insert:

```
2 → Already Exists

4 → Add

5 → Add
```

Final:

```
{1,2,3,4,5}
```

---

# 📊 Complexity Analysis

Let:

```
n = size of array a

m = size of array b
```

---

## Time Complexity

Each insertion in a set takes:

```
O(log(n+m))
```

Total insertions:

```
n + m
```

Therefore:

```
O((n+m) log(n+m))
```

---

## Space Complexity

Set stores all unique elements:

```
O(n+m)
```

---

# 🧠 Memory Trick

Remember:

```
Two Arrays
     |
     ▼
Put Everything in Set
     |
     ▼
Duplicates Removed Automatically
     |
     ▼
Convert Set to Vector
     |
     ▼
Union Answer
```

Short form:

```
INSERT → REMOVE DUPLICATE → RETURN
```

---

# ✅ Key Takeaways

- ✔️ Union contains all unique elements from both arrays.
- ✔️ `set` automatically removes duplicates.
- ✔️ `set` stores values in sorted order.
- ✔️ Easy implementation.
- ✔️ Works even when arrays contain duplicates.
- ✔️ Time Complexity: **O((n+m)log(n+m))**
- ✔️ Space Complexity: **O(n+m)**

---

<div align="center">

# ⭐ If this README helped you, give the repository a ⭐!

## Happy Coding 🚀

</div>
