
### ��������

```
    public static int greedySelector(int s[],int f[],boolean [] a)
    {
        int n=s.length-1;
        a[1]=true;
        int j=1;
        //ѡ�е�һ��
        int count=1;
        
        for (int i=2;i<=n;i++)
        {
            //�����ǰ��Ŀ�ʼʱ�����ǰһ��ѡ�л��ѡ�иû
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