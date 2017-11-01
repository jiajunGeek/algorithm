### 题目：Given a string s and a dictionary of words dict, determine if s can be segmented into a space-separated sequence of one or more dictionary words.
```
For example, given
s = "leetcode",
dict = ["leet", "code"].

```

### 思路：动态规划两个步骤，一个是看是否符合最优子结构，一个是写出递归方程式。定义一个数组，这个数组标记从0到n-1个字符是否被字典中的单词分割。状态转移方程：state[i] = {state[j]&&string[i,j]在字典中，0=<j<i}

```
public boolean wordBreak(String s, Set<String> dict) {  
        if(dict.isEmpty()) {  
            return false;  
        }  
        if(s.length()==0) {  
            return true;  
        }  
          
        int[] state = new int[s.length() + 1];  
        state[0] = 1;  
        for(int i=1;i<=s.length();i++) {  
            for(int j=0;j<i;j++) {  
                if(state[j]==1&&(dict.contains(s.substring(j,i))==true)) {  
                    state[i] = 1;  
                    break;  
                }  
            }  
        }  
        if(state[s.length()]==1) {  
            return true;  
        } else {  
            return false;  
        }  
    }  
```


### 题目：n个小朋友站成一排，根据他们的得分分发糖果，得分高的小朋友要比旁边得分低的小朋友得到的糖果多，每个小朋友至少得到一枚糖果，问最少要准备多少糖果？

### 思路：
先从左到右扫描一遍，使得右边比左边得分高的小朋友糖果数比左边多1(尽可能的少)；
再从右到左扫描一遍，使得左边比右边得分高的小朋友糖果数比右边多（这里要注意，从右向左比较时，只有当左边小朋友比右边的分高且得到的糖果少于等于右边时，b[i]=b[i+1]+1;否则不更新b[i]。）

```
public int candy(int[] ratings) {  
        if(ratings == null||ratings.length == 0)  
            return 0;  
        //b[i]存放第i个小孩得到的糖果数；  
        int []b=new int[ratings.length];  
        //从左向右分糖果：  
        for(int i=0;i<ratings.length;i++)  
            {  
            if(i==0||ratings[i]<=ratings[i-1])  
                {  
                b[i]=1;  
            }else  
                {  
                b[i]=b[i-1]+1;  
            }  
        }  
    //从右向左比较：只有当左边小朋友比右边的分高且得到的糖果少于等于右边时，b[i]=b[i+1]+1;否则不更新b[i];  
        for(int i=b.length-2;i>=0;i--)  
            {  
            if(ratings[i]>ratings[i+1])  
                {  
                if(b[i]<=b[i+1])  
                b[i]=b[i+1]+1;  
            }  
        }  
        //对b[]求和即为总糖果数；  
        int sum=0;  
        for(int i:b)  
            {  
            sum+=i;  
        }  
        return sum;  
    }  
```


### 题目：求字符串的最小分割数，使得分割后的子串都是回文串

### 思路：用一个二维的boolean数组表示i到j是否回文，用一个数组cutnum表示最小分割数


```
public class Solution {  
    public int minCut(String s) {  
        if (s == null || s.length() < 2) return 0;  
          
        int n = s.length();  
        boolean[][] isPalin = new boolean[n][n];  
        int[] cutNum = new int[n]; // cutNum[i]: cuts numbers from 0 to i  
          
        for (int i = 0; i < n; i++) {  
            cutNum[i] = i;  
              
            for (int j = i; j >= 0; j--) {  
                //如果j和i的位置这两个字符是一样的，说明可能是回文的
                if (s.charAt(j) == s.charAt(i) && (i - j < 2 || isPalin[j + 1][i - 1]) ) {  
                    isPalin[j][i] = true;  
                      
                    if (j == 0) {  
                        cutNum[i] = 0; // s[0...i] is palindrome, no need cut  
                    } else {  
                        cutNum[i] = Math.min(cutNum[i], cutNum[j - 1] + 1);  
                    }  
                }  
            }  
        }  
          
        return cutNum[n - 1];  
    }  
}  
```
### 题目：Given a string S and a string T, count the number of distinct subsequences of T in S.
A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ACE" is a subsequence of "ABCDE" while "AEC" is not).
Here is an example:
S = "rabbbit", T = "rabbit"
Return 3.

### 思路：题目的意思是在s中找有几种和T一样的字串


```
public class Solution {
    public int numDistinct(String s, String t) {
        int n = s.length(), m = t.length();
        int[][] dp = new int[m+1][n+1];
        for(int j = 0; j < n; j++){
            dp[0][j] = 1;
        }
        for(int i = 1; i < m+1; i++){
            for(int j = 1; j < n+1; j++){
                if(s.charAt(j-1)==t.charAt(i-1)){
                    dp[i][j] = dp[i-1][j-1]+dp[i][j-1];
                } else {
                    dp[i][j] = dp[i][j-1];
                }
            }
        }
        return dp[m][n];
    }
}
```

### 题目：Given a string s and a dictionary of words dict, determine if s can be segmented into a space-separated sequence of one or more dictionary words.For example, given s = "leetcode", dict = ["leet", "code"].Return true because "leetcode" can be segmented as "leet code".

### 思路：创建一个boolean数组dp，dp[i]为true表示i后面的字符串可以分割成指定的字符串，如果dp[0]为true表示这个这个字符串可以分割

```
public class Solution {
    public boolean wordBreak(String s, Set<String> wordDict) {
        boolean[] dp = new boolean[s.length()+1];
        Arrays.fill(dp,false);
        dp[s.length()]=true;
        // 外层循环递增长度
        for(int i = s.length()-1; i >=0 ; i--){
            // 内层循环寻找分割点
            for(int j = i; j < s.length(); j++){
                String sub = s.substring(i,j+1);
                if(wordDict.contains(sub) && dp[j+1]){
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[0];
    }
}
```


### 题目：A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).How many possible unique paths are there?

### 思路：找出状态转移方程：dp[i][j]=dp[i-1][j]+dp[i][j-1],降成一维结果如下

```
public int uniquePaths(int m, int n) {  
    if(m<=0 || n<=0)  
        return 0;  
    int[] res = new int[n];  
    res[0] = 1;  
    for(int i=0;i<m;i++)  
    {  
        for(int j=1;j<n;j++)  
        {  
           res[j] += res[j-1];  
        }  
    }  
    return res[n-1];  
}  
```