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


### 题目：一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

### 思路：动态规划的入门题

```
public class Solution {
    public int JumpFloor(int target) {
        if(target==0)
            return 0;
        if(target==1)
            return 1;
        int dp[]=new int [target+1];
        dp[1]=1;
        dp[0]=1;
        for (int i = 2; i <=target ; i++) {
            dp[i]=dp[i-1]+dp[i-2];
        }
        return dp[target];
    }
}
```

### 题目：定义栈的数据结构，请在该类型中实现一个能够得到栈最小元素的min函数。

### 思路：建一个辅助栈，如果当前push的是最小值，那么将他push到辅助栈。pop的时候，看是否是最小值，如果是的话，那么将辅助栈pop

```

public class Solution {
    Stack<Integer> data = new Stack<Integer>();
    Stack<Integer> min = new Stack<Integer>();
    Integer temp = null;
    public void push(int node) {
        if(temp != null){
            if(node <= temp ){
                temp = node;
                min.push(node);
            }
            data.push(node);
        }else{
            temp = node;
            data.push(node);
            min.push(node);
        }
    }
     
    public void pop() {
        int num = data.pop();
        int num2 = min.pop();
        if(num != num2){
           min.push(num2);
        }
    }
     
    public int top() {
        int num = data.pop();
        data.push(num);
        return num;
    }
     
    public int min() {
        int num = min.pop();
        min.push(num);
        return num;
    }
}
```


### 题目：输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4，5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

### 思路：按照压栈顺序，比如说第一个，如果这个不是弹出序列的第一个，那么就压入，如果是的话，就将他弹出，看下栈顶元素，是不是要弹出。依次进行下去，如果到了最后栈是空的，说明是可能的

```

import java.util.ArrayList;
import java.util.Stack;
public class Solution {
    public boolean IsPopOrder(int [] pushA,int [] popA) {
        if(pushA.length == 0 || popA.length == 0)
            return false;
        Stack<Integer> s = new Stack<Integer>();
        //用于标识弹出序列的位置
        int popIndex = 0;
        for(int i = 0; i< pushA.length;i++){
            s.push(pushA[i]);
            //如果栈不为空，且栈顶元素等于弹出序列
            while(!s.empty() &&s.peek() == popA[popIndex]){
                //出栈
                s.pop();
                //弹出序列向后一位
                popIndex++;
            }
        }
        return s.empty();
    }
}
```

### 题目：从上往下打印出二叉树的每个节点，同层节点从左至右打印

### 思路：经典的广度遍历，用一个队列辅助

```
public class Solution {
    public ArrayList<Integer> PrintFromTopToBottom(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        if(root==null){
            return list;
        }
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            TreeNode treeNode = queue.poll();
            if (treeNode.left != null) {
                queue.offer(treeNode.left);
            }
            if (treeNode.right != null) {
                queue.offer(treeNode.right);
            }
            list.add(treeNode.val);
        }
        return list;
    }
}

```


### 题目：输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出Yes,否则输出No。假设输入的数组的任意两个数字都互不相同。

### 思路：先清楚二叉搜素数的概念，如果左子树不为空，则左子树上所有的节点都小于根节点，如果右子树不为空，则右子树所有节点都大于根节点。树的问题用递归往往容易解决。首先找到根节点，然后找到比根节点小的位置，那么这个位置到根节点的就是右子树，左边的就是左子树，然后递归执行下去就行。

```
public class Solution {
    public boolean VerifySquenceOfBST(int [] sequence) {
        if(sequence.length==0)
            return false;
        if(sequence.length==1)
            return true;
        return ju(sequence, 0, sequence.length-1);
         
    }
     
    public boolean ju(int[] a,int star,int root){
        if(star>=root)
            return true;
        int i = root;
        //从后面开始找
        while(i>star&&a[i-1]>a[root])
            i--;//找到比根小的坐标
        //从前面开始找 star到i-1应该比根小
        for(int j = star;j<i-1;j++)
            if(a[j]>a[root])
                return false;;
        return ju(a,star,i-1)&&ju(a, i, root-1);
    }
}
```


### 题目：输入一颗二叉树和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。


### 思路：本题采用深搜。从根节点到出发，有两条路可走，走左边和走右边，分别进行遍历。
```

public class Solution {
    private ArrayList<ArrayList<Integer>> listAll = new ArrayList<ArrayList<Integer>>();
    private ArrayList<Integer> list = new ArrayList<Integer>();
    public ArrayList<ArrayList<Integer>> FindPath(TreeNode root,int target) {
        if(root == null) return listAll;
        list.add(root.val);
        target -= root.val;
        //判断是否符合
        if(target == 0 && root.left == null && root.right == null)
            listAll.add(new ArrayList<Integer>(list));
        //不符合的话，向左走
        FindPath(root.left, target);
        //向右走
        FindPath(root.right, target);
        //退回一步
        list.remove(list.size()-1);
        return listAll;
    }
}
```

### 题目：输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串abc,则打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。

### 思路：用递归解就可以，注意去重的问题，可以用hashset来去重。


```
import java.util.*;
public class Solution {
    public ArrayList<String> Permutation(String A) {
        // write code here
        
        
        ArrayList<String> list = new ArrayList<>();
        if(A.length()==0)
            return list;
		permutation(list, A.toCharArray(), 0);
        HashSet set=new HashSet(list);
        list=new ArrayList(set);
        Collections.sort(list);
        
        
        return list;
    }
     
    public void permutation(ArrayList<String> list, char[] array, int k) {
        if(k == array.length) {
            list.add(new String(array));
            return ;
        }
        //核心代码
        for(int i = k; i < array.length; i++) {
            swap(array, i, k);
            permutation(list, array, k + 1);
            swap(array, i, k);
        }
    }
     
    public void swap(char[] array, int i, int j) {
        if(i != j) {
            char temp = array[i];
            array[i] = array[j];
            array[j] = temp;
        }
    }
    
}
```



### 题目：数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。

### 思路：用一个辅助的hashmap，键为数组元素，数组为次数。这样的话从头开始遍历，put进map里面，最后进行看map里面那个键对应的值超过数组长度一半

```


public class Solution {
    public int MoreThanHalfNum_Solution(int [] array) {
        HashMap<Integer,Integer> map = new HashMap<Integer,Integer>();
         
        for(int i=0;i<array.length;i++){
             
            if(!map.containsKey(array[i])){
               map.put(array[i],1);
            }else{
                int count = map.get(array[i]);
                map.put(array[i],++count);
            }
        }
        Iterator iter = map.entrySet().iterator();
        while(iter.hasNext()){
            Map.Entry entry = (Map.Entry)iter.next();
            Integer key =(Integer)entry.getKey();
            Integer val = (Integer)entry.getValue();
            if(val>array.length/2){
                return key;
            }
        }
        return 0;
}
```


### 题目：输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

### 思路：冒泡实现的是取出最小的n个数，所以将第二重循环改成k就行


```
public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
        ArrayList<Integer> al = new ArrayList<Integer>();
        if (k > input.length) {
            return al;
        }
        for (int i = 0; i < k; i++) {
            for (int j = 0; j < input.length - i - 1; j++) {
                if (input[j] < input[j + 1]) {
                    int temp = input[j];
                    input[j] = input[j + 1];
                    input[j + 1] = temp;
                }
            }
            al.add(input[input.length - i - 1]);
        }
        return al;
    }
```

### 题目：HZ偶尔会拿些专业问题来忽悠那些非计算机专业的同学。今天测试组开完会后,他又发话了:在古老的一维模式识别中,常常需要计算连续子向量的最大和,当向量全为正数的时候,问题很好解决。但是,如果向量中包含负数,是否应该包含某个负数,并期望旁边的正数会弥补它呢？例如:{6,-3,-2,7,-15,1,2,2},连续子向量的最大和为8(从第0个开始,到第3个为止)。你会不会被他忽悠住？(子向量的长度至少是1)

### 思路：从头开始遍历，tempsum表示目前连续的和，如果此时这个和是小于0的时候（没有意义），这个tempsum应该用当前的元素代替。如果不是的话，加上当前的元素，如果和比之前记录的最大值还要大的话，sum设置为当前的和


```

int FindGreatestSumOfSubArray(int array[]) {
        if(array.length==0)return 0;
        int sum = array[0], tempsum = array[0]; 
        for(int i = 1; i < array.length; i++) 
        {
            tempsum = (tempsum < 0) ? array[i] : tempsum + array[i];
            sum = (tempsum > sum) ? tempsum : sum;
        }
        return sum;
    }
```

### 题目：求出1~13的整数中1出现的次数,并算出100~1300的整数中1出现的次数？为此他特别数了一下1~13中包含1的数字有1、10、11、12、13因此共出现6次,但是对于后面问题他就没辙了。ACMer希望你们帮帮他,并把问题更加普遍化,可以很快的求出任意非负整数区间中1出现的次数。

### 思路：从1到n，将这些数添加到StringBuffer（设置好大小，可以减少空间减少时间），然后遍历这个字符串有多少个1就行了

```

 public int NumberOf1Between1AndN_Solution(int n) {
        int count=0;
        StringBuffer s=new StringBuffer();
        for(int i=1;i<n+1;i++){
             s.append(i);
        }
        String str=s.toString();
        for(int i=0;i<str.length();i++){
            if(str.charAt(i)=='1')
                count++;
        }
        return count;
    }
```



