# 📈 Best Time to Buy and Sell Stock - One Pass Algorithm

![Algorithm](https://img.shields.io/badge/Algorithm-Greedy-blue)
![Language](https://img.shields.io/badge/Language-C%2B%2B-orange)
![Time Complexity](https://img.shields.io/badge/Time-O(n)-green)
![Space Complexity](https://img.shields.io/badge/Space-O(1)-green)

---

# 📌 Problem Statement

You are given an array `prices` where:

- `prices[i]` represents the stock price on day `i`.
- You can buy the stock on one day.
- You can sell the stock on a future day.

Find the **maximum profit** you can achieve.

---

# Example

## Input

```cpp
prices = [7,1,5,3,6,4]
```

## Output

```
5
```

## Explanation

Buy on day:

```
price = 1
```

Sell on day:

```
price = 6
```

Profit:

```
6 - 1 = 5
```

Therefore:

```
Maximum Profit = 5
```

---

# 💡 Approach - Greedy Algorithm

The idea:

> Always keep track of the lowest buying price seen so far and calculate the profit if we sell today.

We maintain two variables:

---

## 1. bestBuy

Stores the minimum stock price found so far.

Example:

```
bestBuy = 1
```

means:

```
Best day to buy until now
```

---

## 2. maxProfit

Stores the maximum profit possible.

Formula:

```
profit = selling price - buying price
```

Example:

```
6 - 1 = 5
```

---

# 🧠 Algorithm

```
1. Assume first day price is the best buying price.

2. Traverse the array from day 1.

3. If today's price is greater than buying price:

       Calculate profit.

4. Update maximum profit.

5. Update minimum buying price.

6. Return maximum profit.
```

---

# 🔥 Visualization Example

Input:

```
prices = [7,1,5,3,6,4]
```

Array:

```
Day:      0   1   2   3   4   5

Price:    7   1   5   3   6   4
```

---

# Step 1

Initial:

```
bestBuy = prices[0]

bestBuy = 7

maxProfit = 0
```

Diagram:

```
Buy Price

   ↓

[7]  1   5   3   6   4
```

---

# Step 2

Day 1:

```
price = 1
```

Compare:

```
1 < 7
```

Update buying price:

```
bestBuy = 1
```

Diagram:

```
7  [1]  5   3   6   4
    ↑
 Best Buy
```

---

# Step 3

Day 2:

```
price = 5
```

Can sell?

```
5 > 1 ✅
```

Calculate profit:

```
5 - 1 = 4
```

Update:

```
maxProfit = 4
```

Diagram:

```
Buy          Sell

 ↓             ↓

1             5

Profit = 4
```

---

# Step 4

Day 3:

```
price = 3
```

Profit:

```
3 - 1 = 2
```

Already have:

```
maxProfit = 4
```

No update.

---

# Step 5

Day 4:

```
price = 6
```

Profit:

```
6 - 1 = 5
```

Update:

```
maxProfit = 5
```

Diagram:

```
Buy              Sell

 ↓                ↓

 1                6


Profit:

6 - 1 = 5
```

---

# Step 6

Day 5:

```
price = 4
```

Profit:

```
4 - 1 = 3
```

No update.

---

# Final Answer

```
Maximum Profit = 5
```

Transaction:

```
Buy  → 1

Sell → 6
```

---

# 📊 Algorithm Flow Diagram

```
             Start

               |

               ↓

      Store minimum buy price

               |

               ↓

        Traverse prices array

               |

               ↓

     Is current price > bestBuy?

          /             \

        Yes              No

         |                |

         ↓                |

 Calculate Profit         |

         |                |

         ↓                |

 Update maxProfit         |

          \              /

             Continue

               |

               ↓

        Update bestBuy

               |

               ↓

             Return

          maxProfit
```

---

# 💻 C++ Solution

```cpp
class Solution {
public:

    int maxProfit(vector<int>& prices) {

        int maxProfit = 0;

        int bestBuy = prices[0];


        for(int i = 1; i < prices.size(); i++) {


            if(prices[i] > bestBuy) {

                maxProfit = max(
                    maxProfit,
                    prices[i] - bestBuy
                );

            }


            bestBuy = min(
                bestBuy,
                prices[i]
            );
        }


        return maxProfit;
    }
};
```

---

# 📖 Another Example

Input:

```
prices = [7,6,4,3,1]
```

Diagram:

```
7
 \
  6
   \
    4
     \
      3
       \
        1
```

Prices are continuously decreasing.

There is no profitable transaction.

Output:

```
0
```

---

# ⏱️ Complexity Analysis

## Time Complexity

Only one traversal:

```
O(n)
```

---

## Space Complexity

Only two variables:

```
O(1)
```

---

# ⭐ Key Takeaways

✅ Greedy approach

✅ Track minimum buying price

✅ Calculate profit while traversing

✅ No need to check every pair

✅ One-pass optimal solution

---

# 🧠 Pattern To Remember

```
Keep the cheapest buying price.

For every new price:

    Profit = Current Price - Cheapest Price

    Update maximum profit.
```

Example:

```
Prices:

7  1  5  3  6  4

    Buy      Sell
     ↓        ↓

     1  --->  6

Profit = 5
```

🚀 **A brute force O(n²) stock problem becomes an efficient O(n) greedy solution.**
