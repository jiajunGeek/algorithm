### 题目：在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

### 思路：抓住重要的一点，右上方的那一个点，向下是变大，向左是变小

```
public class Solution {
    public boolean Find(int target, int [][] array) {
        int i=0;
        int j=array[0].length-1;
        
        while(i>=0&&j>=0&&i<array.length&&j<array[0].length)
        {
            if(array[i][j]==target)
            {
                return  true;
            }
            else
            {
                if(array[i][j]<target)
                {
                    i++;
                    
                }
                else
                {
                    j--;
                }
            }
        }
        return false;
    }
}
```
