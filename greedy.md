
### 互动安排

```
    public static int greedySelector(int s[],int f[],boolean [] a)
    {
        int n=s.length-1;
        a[1]=true;
        int j=1;
        //选中第一个
        int count=1;
        
        for (int i=2;i<=n;i++)
        {
            //如果当前活动的开始时间大于前一个选中活动，选中该活动
            if(s[i]>=f[j])
            {
                a[i]=true;
                j=1;
                count++;
            }
            else
                a[i]=false;
        }
        return count;
    }
```