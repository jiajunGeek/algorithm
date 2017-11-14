
### 世界上有10种人，一种懂二进制，一种不懂。那么你知道两个int32整数m和n的二进制表达，有多少个位(bit)不同么？

```
 public int countBitDiff(int m, int n) {
        String str=Integer.toBinaryString(m^n);
        str=str.replaceAll("0","");
        return str.length();
    }
}
```


### 风口之下，猪都能飞。当今中国股市牛市，真可谓“错过等七年”。 给你一个回顾历史的机会，已知一支股票连续n天的价格走势，以长度为n的整数数组表示，数组中第i个元素（prices[i]）代表该股票第i天的股价。 假设你一开始没有股票，但有至多两次买入1股而后卖出1股的机会，并且买入前一定要先保证手上没有股票。若两次交易机会都放弃，收益为0。 设计算法，计算你能获得的最大收益。 输入数值范围：2<=n<=100,0<=prices[i]<=100


```
public class Solution {
    /**
     * 计算你能获得的最大收益
     * 
     * @param prices Prices[i]即第i天的股价
     * @return 整型
     */


public int calculateMax(int[] prices) {
	if(prices==null||prices.length<2)
		return 0;
	int len=prices.length;
	int[] left=new int[len];
	left[0]=0;
	int min=prices[0];
	int max=0;
	for(int i=1;i<len;i++){
		if(prices[i]<min)
	min=prices[i];
	if(prices[i]-min>max)
		max=prices[i]-min;
	left[i]=max;
}
	int[] right=new int[len];
	right[0]=0;
	int high=prices[len-1];
	max=0;
	for(int i=len-2;i>=0;i--){
		if(prices[i]>high)
			high=prices[i];
		if(high-prices[i]>max)
			max=high-prices[i];
		right[i]=max;
}
	int result=0;
	for(int i=0;i<len;i++){
		if(left[i]+right[i]>result)
			result=left[i]+right[i];
	}
	return result;
	}
}
```