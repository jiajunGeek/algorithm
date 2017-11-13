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

### ��԰����һ��ƻ����һ��nͷ(n����1С��9)�����֣���һͷΪС��������ƻ������n�ݺ󣬶����һ�������ӵ�����һ�����������Լ���һ��ƻ�������ŵڶ�ͷ���ظ���һ���̣����Ⱦ���n�ݣ��ӵ�һ��Ȼ������һ�ݣ��Դ�����ֱ�����һͷ�ܶ�������(���һͷ���ӵ����������0����Ҳ����n�ݾ���)����������ƻ�������ж��ٸ�

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

### ��̨��

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


### �����������ϣ�Ҫ��{A} + {B}�� ע��ͬһ�������в�����������ͬ��Ԫ�ء�

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