# Best time to buy and sell stocks
# Date 26-01-2026
# Problem link
- https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/
# Description
- We're given an `prices` array, which include price of a stock on `i'th` day
- we have to maximize the profit by making buy rate minimum and sell rate maximum, and of course sell rate comes after the buy rate
- Example
```bash
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
```
# Approach 1 - max and min
- We start with `maxProf=0` and `minBuy=prices[0]` from start
- then we iterate over the array
- we set maxProf to max of maxProf and `curr price - minBuy`
- and we set minBuy to min of minBuy and `curr price`
- at last we get max profit

|index|0|1|2|3|4|5|
|-|-|-|-|-|-|-|
|price|7|1|5|3|6|4|
|minBuy|7|1|1|1|1|1|
|maxProf|0|0|4|4|5|5|

<details>
<summary><b>Code</b></summary>

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int maxProf = 0;
        int minBuy = prices[0];
        int n = prices.size();
        for(int i=1 ; i<n ; i++){
            maxProf = max(maxProf, prices[i] - minBuy);
            minBuy = min(minBuy, prices[i]);
        }
        return maxProf;
    }
};
```
</details>

- Time complexity : O(n)
- Space complexity : O(1)
***