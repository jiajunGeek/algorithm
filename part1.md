### 题目：在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

### 思路：抓住重要的一点，右上方的那一个点，向下是变大，向左是变小

```
public class Solution {
    public boolean Find(int target, int [][] array) {
        int i=0;
        int j=array[0].length-1;
        
        while(i>=0&&j>=0&&i<array.length&&j<array[0].length)
        {
            if(array[i][j]==target)
            {
                return  true;
            }
            else
            {
                if(array[i][j]<target)
                {
                    i++;
                    
                }
                else
                {
                    j--;
                }
            }
        }
        return false;
    }
}




```


### 题目：一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

### 思路：动态规划的入门题
public class Solution {
    public int JumpFloor(int target) {
        if(target==0)
            return 0;
        if(target==1)
            return 1;
        int dp[]=new int [target+1];
        dp[1]=1;
        dp[0]=1;
        for (int i = 2; i <=target ; i++) {
            dp[i]=dp[i-1]+dp[i-2];
        }
        return dp[target];
    }
}
```
```
