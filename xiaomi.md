
### ��������10���ˣ�һ�ֶ������ƣ�һ�ֲ�������ô��֪������int32����m��n�Ķ����Ʊ��ж��ٸ�λ(bit)��ͬô��

```
 public int countBitDiff(int m, int n) {
        String str=Integer.toBinaryString(m^n);
        str=str.replaceAll("0","");
        return str.length();
    }
}
```


### ���֮�£����ܷɡ������й�����ţ�У����ν����������ꡱ�� ����һ���ع���ʷ�Ļ��ᣬ��֪һ֧��Ʊ����n��ļ۸����ƣ��Գ���Ϊn�����������ʾ�������е�i��Ԫ�أ�prices[i]������ù�Ʊ��i��Ĺɼۡ� ������һ��ʼû�й�Ʊ������������������1�ɶ�������1�ɵĻ��ᣬ��������ǰһ��Ҫ�ȱ�֤����û�й�Ʊ�������ν��׻��ᶼ����������Ϊ0�� ����㷨���������ܻ�õ�������档 ������ֵ��Χ��2<=n<=100,0<=prices[i]<=100


```
public class Solution {
    /**
     * �������ܻ�õ��������
     * 
     * @param prices Prices[i]����i��Ĺɼ�
     * @return ����
     */


public int calculateMax(int[] prices) {
	if(prices==null||prices.length<2)
		return 0;
	int len=prices.length;
	int[] left=new int[len];
	left[0]=0;
	int min=prices[0];
	int max=0;
	for(int i=1;i<len;i++){
		if(prices[i]<min)
	min=prices[i];
	if(prices[i]-min>max)
		max=prices[i]-min;
	left[i]=max;
}
	int[] right=new int[len];
	right[0]=0;
	int high=prices[len-1];
	max=0;
	for(int i=len-2;i>=0;i--){
		if(prices[i]>high)
			high=prices[i];
		if(high-prices[i]>max)
			max=high-prices[i];
		right[i]=max;
}
	int result=0;
	for(int i=0;i<len;i++){
		if(left[i]+right[i]>result)
			result=left[i]+right[i];
	}
	return result;
	}
}
```