### ��һ����Ϊn������A��������0��a��b<n��A[b]-A[a]�����ֵ����������A�����Ĵ�Сn���뷵������ֵ��

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


### ��4x4�������ϰ����˺ڰ����ӣ��ڰ���ɫ��λ�ú���Ŀ����������Ͻ�����Ϊ(1,1),���½�����Ϊ(4,4),����������һЩ��ת������Ҫ��һЩ����֧������Ϊ���ĵ����������ĸ����ӵ���ɫ���з�ת����������ת���������ɫ��������������A��f,�ֱ�Ϊ��ʼ���̺ͷ�תλ�á����з�תλ�ù���3�����뷵�ط�ת������̡�


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


### ������һ���������۾�����Ҫ�ӹ�˾������ȥ�ݷ����ڵ��̼ң���֪����λ���Լ��̼ҵ�λ�ã��������ڳ��е�·��ͨ��ԭ����ֻ����������ѡ��һ��������������ѡ��һ���������������ж����ַ��������̼ҵ�ַ������һ����ͼmap�����ĳ���n��m������1������λ�ã�2�����̼�λ�ã�-1�����ܾ����ĵ�����0������Ծ����ĵ������뷵�ط���������֤һ�����ںϷ�·������֤����ĳ���С�ڵ���10��

```
public int countPath(int[][] map, int n, int m) {
    // �����ҳ�1��2���ڵ�λ��
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
    if(x1==x2&&y1==y2){// �����غ�
        return 1;
    }
    if(x1>x2){// x1,y1���ڱ������±�Ľ�С��
        x1 = x1^x2^(x2=x1);
        y1 = y1^y2^(y2=y1);
    }
    int dp[][] = new int[n][m];
    if(y1<y2){// ���㴦�����Խ�����
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
    }else{// ���ߴ��ڸ��Խ�����
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



### ��һ��ֱ��ͼ����һ�����������ʾ������ÿ�еĿ��Ϊ1��������ֱ��ͼ��������������������磬����ֱ��ͼ[2,7,9,4],���������������ε����Ϊ14(��[7,9]������7x2�ľ���)������һ��ֱ��ͼA�������ܿ��n���뷵���������������ֱ֤��ͼ���С�ڵ���500����֤�����int��Χ�ڡ�

```
 public int countArea(int[] A, int n) {
        if (A==null){
            return 0;
        }
        int dp[][]=new int[n][n];
        //��ֵ��ֵ
        for (int i = 0; i < n; i++) {
            dp[i][i]=A[i];
        }
        for (int k = 1; k <=n ; k++) {
            for (int i = 0; (i+k) <n ; i++) {
                //�������Сֵ
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


### ���ֵ�����s1��s2֮��ģ�������len1��len2���ַ����ĸ��������mod 1000007��

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
     * ���ֵ�����s1��s2֮��ģ�������len1��len2���ַ����ĸ��������mod 1000007��
     * @param str1 �ַ���s1
     * @param str2 �ַ���s2
     * @param len1 ����len1
     * @param len2 ����len1
     * @return ������len1��len2���ַ����ĸ��������mod 1000007
     */
    public static long getStrCount(String str1,String str2,int len1,int len2){
//      System.out.println(str1+" "+ str2+" "+len1+" "+len2);
        long sum = 0;
        char a[] = str1.toCharArray();
        char b[] = str2.toCharArray();
        int i = len1;
        for(i = len1; i <= len2; i++){//���ȴ�len1 ��len2������len2-len1�����
            char a1 = a[0];
            char b1 = b[0];
            int t = b1 - a1;//���ߵĲ�ֵ
            sum = sum + t * (long)Math.pow(26, i - 1);//�ȱȽϸ�λ�Ĳ�ֵ���ǵó���26��i-1����
            long suma = 0,sumb = 0;//����ͳ��a[1]~a[i]�ĸ�����b[1]~b[i]�ĸ�������a[1]-a[3] = abc ��ÿһλ�ĸ����ֱ�Ϊ 123��a[1]-'a'-1=1,a[2]-'a'-1=2,a[3]-'a'-1=3
            int j = 1;
            int min = a.length > i ? i : a.length;
            for(j = 1; j < min; j++ ){
                t = a[j] - 'a' + 1;//������ֵ����λ�ã�������Ҫ����'a'����Ҫ����һ��1����a���ֵ���Ϊ1��b���ֵ���Ϊ2
                suma = suma + t * (long)Math.pow(26, i - 1 - j);
            }
            min = b.length > i ? i : b.length;
            for(j = 1; j < min; j++ ){
                t = b[j] - 'a' + 1;
                sumb = sumb + t * (long)Math.pow(26, i - 1 - j);
            }
            sum = sum + sumb - suma;//sumb - suma ������a��b�����ַ�����b[1]~b[i]�������ַ��������-a[1]~a[i]�������ַ��������������֮����ַ�������        
        }
        sum = sum - 1;//�ڼ������һλ��ʱ����ַ���str2Ҳ������ȥ�ˣ�����Ҫ��ȥһ��1������Ŀ�������Ӽ���ce��ʱ���ce�����ȥ�ˣ�b[1]-'a'+1��ʱ�򣩣�����Ҫ����һ��1
        return sum % 1000007;
    }
```

### ��֪ĳ��˾������ΪW��ƽ������ΪY��(ÿ��3��ĩ���㣬ͬʱÿ��3�³���ְ����)������ÿ����ְ��Ϊx��x>0&&x<1,ÿ�걣������Ա���������������Ƹ����Ա��ƽ������21�ꡣ �ӽ���3��ĩ��ʼ����ʵ��һ���㷨�����Լ������N���˾Ա����ƽ�����䡣(���������ȡ��)�� 
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

### ��һ����ά����(n*n),д����ʵ�ִ����Ͻǵ����½������Խ��߷����ӡ������һ����λ����arr����Ŀ�еĲ���n���뷵�ؽ�����顣

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


### ��λ������

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
//���������



```