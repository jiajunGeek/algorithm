### 小东所在公司要发年终奖，而小东恰好获得了最高福利，他要在公司年会上参与一个抽奖游戏，游戏在一个6*6的棋盘上进行，上面放着36个价值不等的礼物，每个小的棋盘上面放置着一个礼物，他需要从左上角开始游戏，每次只能向下或者向右移动一步，到达右下角停止，一路上的格子里的礼物小东都能拿到，请设计一个算法使小东拿到价值最高的礼物。

```
import java.util.*;

public class Bonus {
    public int getMost(int[][] board) {
        // write code here
        int l=board[0].length;
        int dp[][]=new int[l][l];
        dp[0][0]=board[0][0];
        
        for(int i=1;i<l;i++)
        {
            dp[0][i]=dp[0][i-1]+board[0][i];
            dp[i][0]=dp[i-1][0]+board[i][0];
        }
        for(int i=1;i<l;i++)
        {
            for(int j=1;j<l;j++)
            {
                dp[i][j]=board[i][j]+Math.max(dp[i][j-1],dp[i-1][j]);
            }
        }
        return dp[5][5];
    }
}
```

### 小东和三个朋友一起在楼上抛小球，他们站在楼房的不同层，假设小东站的楼层距离地面N米，球从他手里自由落下，每次落地后反跳回上次下落高度的一半，并以此类推知道全部落到地面不跳，求4个小球一共经过了多少米？(数字都为整数)

```
import java.util.*;

public class Balls {
    double distance(double n){
        if(n==0)
            return 0;
        return n+n/2+distance(n/2);
    }
    public int calcDistance(int A, int B, int C, int D) {
        return (int)(distance(A)+distance(B)+distance(C)+distance(D));
    }
}

```

### 果园里有一堆苹果，一共n头(n大于1小于9)熊来分，第一头为小东，它把苹果均分n份后，多出了一个，它扔掉了这一个，拿走了自己的一份苹果，接着第二头熊重复这一过程，即先均分n份，扔掉一个然后拿走一份，以此类推直到最后一头熊都是这样(最后一头熊扔掉后可以拿走0个，也算是n份均分)。问最初这堆苹果最少有多少个

```
import java.util.*;
public int getInitial(int n) {
        //return n*n-n+1;
        for (int i = 1; i < Integer.MAX_VALUE; i++) {
            int count = i;
            boolean flag = false;
            for (int j = 1; j <= n; j++) {
                count--;
                if (count % n == 0){
                    count = count / n *(n-1);
                } else {
                    flag = true;
                    break;
                }
            }
            if(!flag){
                return i;
            }
        }
        return 0;
    }
```

### 上台阶

```
import java.util.*;

public class GoUpstairs {

public int countWays(int n) {
 
    int[] dp = new int[n+1];
    dp[0] = 0;
    dp[1] = 1;
 
    for (int i = 2; i <= n; i++) {
        dp[i] = (dp[i-1] + dp[i-2]) % 1000000007;
    }
    return dp[n];
}
}
```


### 给你两个集合，要求{A} + {B}。 注：同一个集合中不会有两个相同的元素。

```
import java.util.*;
public class Main
{
    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);
        int l1=sc.nextInt();
        int l2=sc.nextInt();
        int array1[]=new int[l1];
        int array2[]=new int[l2];
        TreeSet <Integer>set=new TreeSet();
        for(int i=0;i<l1;i++)
        {
           set.add(sc.nextInt());
        }
        for(int i=0;i<l2;i++)
        {
            set.add(sc.nextInt());
        }
        StringBuffer sb=new StringBuffer();
        for(Iterator iter = set.iterator(); iter.hasNext(); ) { 
    		sb.append(iter.next());
            sb.append(" ");
            
		}
        sb.delete(sb.length()-1, sb.length());
        System.out.println(sb.toString());
    }
}
```