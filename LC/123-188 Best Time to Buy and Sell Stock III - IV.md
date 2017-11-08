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
