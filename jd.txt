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