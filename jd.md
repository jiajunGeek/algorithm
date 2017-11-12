### С�����ڹ�˾Ҫ�����ս�����С��ǡ�û������߸�������Ҫ�ڹ�˾����ϲ���һ���齱��Ϸ����Ϸ��һ��6*6�������Ͻ��У��������36����ֵ���ȵ����ÿ��С���������������һ���������Ҫ�����Ͻǿ�ʼ��Ϸ��ÿ��ֻ�����»��������ƶ�һ�����������½�ֹͣ��һ·�ϵĸ����������С�������õ��������һ���㷨ʹС���õ���ֵ��ߵ����

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

### С������������һ����¥����С������վ��¥���Ĳ�ͬ�㣬����С��վ��¥��������N�ף�����������������£�ÿ����غ������ϴ�����߶ȵ�һ�룬���Դ�����֪��ȫ���䵽���治������4��С��һ�������˶����ף�(���ֶ�Ϊ����)

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