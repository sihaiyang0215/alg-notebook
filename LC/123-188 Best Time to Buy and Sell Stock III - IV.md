### 123. Best Time to Buy and Sell Stock III
```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length < 2)
            return 0;
        int hold0 = -prices[0]; //第一次买入时的最大收益
        int hold1 = -prices[0]; //第一次买入时的最大收益
        int sell0 = 0; //第一次卖出时的最大收益
        int sell1 = 0; //第二次卖出时的最大收益
        for(int i = 1; i < prices.length; i++){
            //倒叙计算是因为当前价格第二次卖出要使用前一次价格中第二次买入的价格；
            //当前价格第二次买入要使用前一次价格中一次卖出的价格进行计算
            sell1 = Math.max(sell1, hold1 + prices[i]); //当前第二次卖出时的最大收益
            hold1 = Math.max(hold1, sell0 - prices[i]); //当前第二次买入时的最大收益
            sell0 = Math.max(sell0, hold0 + prices[i]); //当前第一次卖出时的最大收益
            hold0 = Math.max(hold0, 0 - prices[i]); //当前第二次买入时的最大收益，第一次买入手中价钱是0。
        }
        return sell1;
    }
}
```
---
### 188. Best Time to Buy and Sell Stock IV
188是将123的问题由两次买卖推广到K次。  
如果k >= prices.length / 2 就变成了```122. Best Time to Buy and Sell Stock II```.  
否则两种方法:   
Solution 1: 完全是123的推广    
```java
class Solution {
    public int maxProfit(int k, int[] prices) {
        if(prices == null || prices.length < 2)
            return 0;
        if(k >= prices.length / 2)
            return helper(prices);
        
        int[] sell = new int[k + 1];
        int[] hold = new int[k + 1];
        Arrays.fill(hold, -prices[0]);
        for(int j = 1; j < prices.length; j++){
            for(int i = k; i > 0; i--){
                sell[i] = Math.max(sell[i], hold[i] + prices[j]);
                hold[i] = Math.max(hold[i], sell[i - 1] - prices[j]);
            }
        }
        
        return sell[k];
    }
    
    public int helper(int[] prices){
        int sum = 0; 
        for(int i = 1; i < prices.length; i++){
            if(prices[i] > prices[i - 1])
                sum += prices[i] - prices[i - 1];
        }
        return sum;
    }
}
```

solution 2: 动态规划
```java
class Solution {
    public int maxProfit(int k, int[] prices) {
        if(prices == null || prices.length < 2)
            return 0;
        if(k >= prices.length / 2)
            return helper(prices);
        
        int[][] sell = new int[k + 1][prices.length];
        //注意：sell[0][n] == 0.因为0次交易的最大收益永远是是0
        //sell[n][0] == 0. 没有股票价格自然最大收益是0
        
        for(int i = 1; i <= k; i++){
            int hold = 0 - prices[0]; //第一次买入，此时本金为0
            for(int j = 1; j < prices.length; j++){
                sell[i][j] = Math.max(sell[i][j - 1], hold + prices[j]); //前j-1个价格时卖出的最大收益和当前价格卖出时最大收益的较大值
                hold = Math.max(hold, sell[i - 1][j - 1] - prices[j]); //当前买入的最大收益，sell[i - 1][j - 1]表示[前一次交易][前一次价格]
            }
        }
        return sell[k][prices.length - 1];
    }
    
    public int helper(int[] prices){
        int sum = 0; 
        for(int i = 1; i < prices.length; i++){
            if(prices[i] > prices[i - 1])
                sum += prices[i] - prices[i - 1];
        }
        return sum;
    }
}
```
