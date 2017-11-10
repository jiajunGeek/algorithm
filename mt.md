### 有一个长为n的数组A，求满足0≤a≤b<n的A[b]-A[a]的最大值。给定数组A及它的大小n，请返回最大差值。

```
import java.util.*;  
  
public class LongestDistance {  
    public int getDis(int[] A, int n) {  
        // write code here  
        int result = 0;  
        int min = A[0];  
        if (n > 1) {  
            for (int i = 1; i < n; i++) {  
                if (A[i] - min > result) {  
                    result = A[i] - min;  
                }  
                if (A[i] < min) {  
                    min = A[i];  
                }  
            }  
        }  
        return result;  
    }  
}  
```


### 在4x4的棋盘上摆满了黑白棋子，黑白两色的位置和数目随机其中左上角坐标为(1,1),右下角坐标为(4,4),现在依次有一些翻转操作，要对一些给定支点坐标为中心的上下左右四个棋子的颜色进行翻转，请计算出翻转后的棋盘颜色。给定两个数组A和f,分别为初始棋盘和翻转位置。其中翻转位置共有3个。请返回翻转后的棋盘。


```
import java.util.*;

public class Flip {
    
    public int[][] flipChess(int[][] A, int[][] f) {
        // write code here
        for(int i=0;i<f.length;i++)
        {
            int m=f[i][0]-1;
            int n=f[i][1]-1;
            change(A,m-1,n);
            change(A,m+1,n);
            change(A,m,n-1);
            change(A,m,n+1);
        }
        return A;
    }
    public static void change(int A[][],int m,int n)
    {
        if(m<0||n<0||m==A.length||n==A[0].length)
        {
            return;
        }
        A[m][n]=A[m][n]==0?1:0;
        
    }
    
}
```


### 现在有一个城市销售经理，需要从公司出发，去拜访市内的商家，已知他的位置以及商家的位置，但是由于城市道路交通的原因，他只能在左右中选择一个方向，在上下中选择一个方向，现在问他有多少种方案到达商家地址。给定一个地图map及它的长宽n和m，其中1代表经理位置，2代表商家位置，-1代表不能经过的地区，0代表可以经过的地区，请返回方案数，保证一定存在合法路径。保证矩阵的长宽都小于等于10。

```
public int countPath(int[][] map, int n, int m) {
    // 首先找出1和2所在的位置
    int i,j;
    int x1=0,x2 = 0,y1 = 0,y2 = 0;
    for (i = 0; i < n; i++) {
        for (j = 0; j < m; j++) {
            if(map[i][j]==1){
                x1 = i;y1=j;
            }else if(map[i][j]==2){
                x2=i;y2=j;
            }
        }
    }      
    if(x1==x2&&y1==y2){// 两点重合
        return 1;
    }
    if(x1>x2){// x1,y1用于保存行下标的较小者
        x1 = x1^x2^(x2=x1);
        y1 = y1^y2^(y2=y1);
    }
    int dp[][] = new int[n][m];
    if(y1<y2){// 两点处在主对角线上
        dp[x1][y1] = 1;
        for (i = x1+1; i<=x2; i++) {
            dp[i][y1] = map[i][y1]==-1?0:dp[i-1][y1];
        }
        for (j = y1+1; j <=y2; j++) {
            dp[x1][j] = map[x1][j]==-1?0:dp[x1][j-1];
        }
        for (i = x1+1; i <= x2; i++) {
            for (j = y1+1; j <=y2; j++) {
                dp[i][j] = map[i][j]==-1?0:dp[i-1][j]+dp[i][j-1];
            }
        }
    }else{// 两者处在副对角线上
        dp[x1][y1] = 1;
        for (i = x1+1; i<=x2; i++) {
            dp[i][y1] = map[i][y1]==-1?0:dp[i-1][y1];
        }
        for (j = y1-1; j >=y2; j--) {
            dp[x1][j] = map[x1][j]==-1?0:dp[x1][j+1];
        }
        for (i = x1+1; i <= x2; i++) {
            for (j = y1-1; j >=y2; j--) {
                dp[i][j] = map[i][j]==-1?0:dp[i-1][j]+dp[i][j+1];
            }
        }
    }
    return dp[x2][y2];
}
```



### 有一个直方图，用一个整数数组表示，其中每列的宽度为1，求所给直方图包含的最大矩形面积。比如，对于直方图[2,7,9,4],它所包含的最大矩形的面积为14(即[7,9]包涵的7x2的矩形)。给定一个直方图A及它的总宽度n，请返回最大矩形面积。保证直方图宽度小于等于500。保证结果在int范围内。

```
 public int countArea(int[] A, int n) {
        if (A==null){
            return 0;
        }
        int dp[][]=new int[n][n];
        //赋值初值
        for (int i = 0; i < n; i++) {
            dp[i][i]=A[i];
        }
        for (int k = 1; k <=n ; k++) {
            for (int i = 0; (i+k) <n ; i++) {
                //先算出最小值
                int min=A[i];
                for (int j = i+1; j <= i+k; ++j) {
                    min = Math.min(min, A[j]);
                }
                dp[i][i+k]=Math.max(dp[i][i+k-1], dp[i+1][i + k]);
                dp[i][i+k]=Math.max(min*(k+1),dp[i][i+k]);
            }
        }
        return dp[0][n-1];
    }
```


### 求字典序在s1和s2之间的，长度在len1到len2的字符串的个数，结果mod 1000007。

```
public static void main(String[] args) {
        // TODO Auto-generated method stub
        Scanner scan = new Scanner(System.in);
//      String t[] = "a   b c".split(" ");
//      System.out.println((int)(0.6)+t.length);
        while(scan.hasNextLine()){
            String inputString[] = scan.nextLine().split(" ");
            System.out.println(getStrCount(inputString[0],inputString[1],Integer.parseInt(inputString[2]),Integer.parseInt(inputString[3])));
            //          System.out.println(scan.nextLine()+"@");
        }


    }
    /***
     * 求字典序在s1和s2之间的，长度在len1到len2的字符串的个数，结果mod 1000007。
     * @param str1 字符串s1
     * @param str2 字符串s2
     * @param len1 长度len1
     * @param len2 长度len1
     * @return 长度在len1到len2的字符串的个数，结果mod 1000007
     */
    public static long getStrCount(String str1,String str2,int len1,int len2){
//      System.out.println(str1+" "+ str2+" "+len1+" "+len2);
        long sum = 0;
        char a[] = str1.toCharArray();
        char b[] = str2.toCharArray();
        int i = len1;
        for(i = len1; i <= len2; i++){//长度从len1 到len2，共有len2-len1种情况
            char a1 = a[0];
            char b1 = b[0];
            int t = b1 - a1;//两者的差值
            sum = sum + t * (long)Math.pow(26, i - 1);//先比较高位的差值，记得乘以26的i-1次幂
            long suma = 0,sumb = 0;//用于统计a[1]~a[i]的个数和b[1]~b[i]的个数，例a[1]-a[3] = abc 则每一位的个数分别为 123即a[1]-'a'-1=1,a[2]-'a'-1=2,a[3]-'a'-1=3
            int j = 1;
            int min = a.length > i ? i : a.length;
            for(j = 1; j < min; j++ ){
                t = a[j] - 'a' + 1;//算出其字典序的位置，所以是要剪掉'a'但还要加上一个1，例a的字典序为1，b的字典序为2
                suma = suma + t * (long)Math.pow(26, i - 1 - j);
            }
            min = b.length > i ? i : b.length;
            for(j = 1; j < min; j++ ){
                t = b[j] - 'a' + 1;
                sumb = sumb + t * (long)Math.pow(26, i - 1 - j);
            }
            sum = sum + sumb - suma;//sumb - suma 即剪掉a、b两个字符串从b[1]~b[i]的所有字符串的情况-a[1]~a[i]的所有字符串的情况即两者之间的字符串个数        
        }
        sum = sum - 1;//在计算最后一位的时候把字符串str2也包含进去了，所以要减去一个1，即题目给的例子计算ce的时候把ce计算进去了（b[1]-'a'+1的时候），所以要减掉一个1
        return sum % 1000007;
    }
```

### 已知某公司总人数为W，平均年龄为Y岁(每年3月末计算，同时每年3月初入职新人)，假设每年离职率为x，x>0&&x<1,每年保持所有员工总数不变进行招聘，新员工平均年龄21岁。 从今年3月末开始，请实现一个算法，可以计算出第N年后公司员工的平均年龄。(最后结果向上取整)。 
```
      public static int Average(int w,double y,double x,int n)
      {
          for(int i=0;i<n;i++)
          {
              y=(y+1)*(1-x)+21*x;
          }
          return (int )Math.ceil(Y)
      }

```

### 有一个二维数组(n*n),写程序实现从右上角到左下角沿主对角线方向打印。给定一个二位数组arr及题目中的参数n，请返回结果数组。

```
public int[] arrayPrint(int[][] arr, int n) {
        int res[]=new int [n*n];
        int index=0;
        int startX=0;
        int startY=n-1;
        while(startX<n)
        {
            int x=startX;
            int y=startY;
            while(x<n&&y<n)
            {
                res[index++]=arr[x++][y++]; 0 2 1 3
                if(startY>0)
                    startY--;
                else
                    startX++;
            }
        }
        return res;

    }
```


### 奇位数丢弃

```
public static void main(String[] args)
{
    Scanner sc=new Scanner(System.in);
    while(sc.hasNext())
    {
        int n=sc.nextInt();
        List<Integer> list=new ArrayList<Integer>();
        for(int i=0;i<=n;i++)
        {
            list.add(i);
        }
        while(list.size()!=1)
        {
            for(int i=0;i<list.size();i=i+1)
                list.remove(i);
        }
        System.out.println(list.get(0))
    }
}
//用链表更加



```