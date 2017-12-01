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

### 题目：在一个字符串(1<=字符串长度<=10000，全部由字母组成)中找到第一个只出现一次的字符,并返回它的位置

### 思路：用一个数组记录每个字符的字数

```
public int FirstNotRepeatingChar(String str)
    {
        char[] c = str.toCharArray();
        int[] a = new int['z'+1];
        for (char d : c)
            a[(int) d]++;
        for (int i = 0; i < c.length; i++)
            if (a[(int) c[i]] == 1)
                return i;
        return -1;
    }
}
```


### 题目：输入两个链表，找出它们的第一个公共结点。
### 思路：充分利用hashmap的特性

```

import java.util.HashMap;
public class Solution {
    public ListNode FindFirstCommonNode(ListNode pHead1, ListNode pHead2) {
        ListNode current1 = pHead1;
        ListNode current2 = pHead2;
 
 
        HashMap<ListNode, Integer> hashMap = new HashMap<ListNode, Integer>();
        while (current1 != null) {
            hashMap.put(current1, null);
            current1 = current1.next;
        }
        while (current2 != null) {
            if (hashMap.containsKey(current2))
                return current2;
            current2 = current2.next;
        }
 
        return null;
 
    }
}
```
### 题目：统计一个数字在排序数组中出现的次数。

### 思路：用二分查找该数字在数组中的位置，然后向前早最左的下标，向后找最右的下标，两个下标相减+1即为所求结果

```
public class Solution {
    public int GetNumberOfK(int [] array , int k) {
       int index=binarySearch(array,0,array.length-1,k);
        if (index==-1)
            return 0;
        int start=searchLeft(array,index);
        int end =searchRight(array,index);
        return end-start+1;
       
    }
    public int searchLeft(int array[],int index)
    {
    	    int target=array[index];
        	while(true){
                if(index==0)
                    break;
                if(array[--index]!=target){
                    index++;
                    break;
                    
                }
            }
        return index;
                
    }
    public int searchRight(int array[],int index)
    {
    	    int target=array[index];
        	while(true){
                if(index==array.length-1)
                    break;
                if(array[++index]!=target){
                    index--;
                    break;
                    
                }
            }
        return index;
    }
    public int binarySearch(int array[],int start,int end,int target)
    {
    	    if(start>end)
                return -1;
        	int index=(start+end)/2;
        	if(array[index]>target){
                return binarySearch(array,start,index-1,target);
            }
        	else{
                if(array[index]==target)
                    return index;
                return binarySearch(array,index+1,end,target);
            }
                
    
    }
}
```


### 题目：输入一棵二叉树，求该树的深度。从根结点到叶结点依次经过的结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度。

### 思路：递归深度遍历

```
public class Solution {
    public int TreeDepth(TreeNode pRoot)
    {
        return pRoot == null? 0 : Math.max(TreeDepth(pRoot.left),TreeDepth(pRoot.right)) + 1;
    }
}
```


### 题目：输入一棵二叉树，判断该二叉树是否是平衡二叉树。

### 思路：二叉树有很好的特点，就是大多可以用递归解决，而递归的好处就是思路清晰

```

public class Solution {
    //后续遍历时，遍历到一个节点，其左右子树已经遍历  依次自底向上判断，每个节点只需要遍历一次
     
    private boolean isBalanced=true;
    public boolean IsBalanced_Solution(TreeNode root) {
         
        getDepth(root);
        return isBalanced;
    }
    public int getDepth(TreeNode root){
        if(root==null)
            return 0;
        int left=getDepth(root.left);
        int right=getDepth(root.right);
         
        if(Math.abs(left-right)>1){
            isBalanced=false;
        }
        return right>left ?right+1:left+1;
         
    }
}
```

### 题目:小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? Good Luck! 


### 思路：巧妙利用等差树列的性质，对每一个可能连续序列长度的进行遍历，判断这个长度下的连续序列是否存在

```


import java.util.ArrayList;
public class Solution {
        public ArrayList<ArrayList<Integer> > FindContinuousSequence(int sum) {
            ArrayList<ArrayList<Integer>>list=new ArrayList<ArrayList<Integer>>();
            if(sum<3)return list;
            int s=(int) Math.sqrt(2*sum);
            for(int i=s;i>=2;i--)
                {
                    if(2*sum%i==0)
                        {
                            int d=2*sum/i;
                            if(d%2==0&&i%2!=0||d%2!=0&&i%2==0)
                                {
                                    int a1=(d-i+1)/2;
                                    int an=(d+i-1)/2;
                                    ArrayList<Integer>temp=new ArrayList<Integer>();
                                    for(int j=a1;j<=an;j++)
                                        temp.add(j);
                                    list.add(temp);
                                }
                        }
                }
            return list;
        }
}
```

### 题目：输入一个递增排序的数组和一个数字S，在数组中查找两个数，是的他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。

### 思路：设置一个头指针，一个尾指针，向中间靠拢

```
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> FindNumbersWithSum(int [] array,int sum) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        if (array == null || array.length < 2) {
            return list;
        }
        int i=0,j=array.length-1;
        while(i<j){
            if(array[i]+array[j]==sum){
            list.add(array[i]);
            list.add(array[j]);
                return list;
           }else if(array[i]+array[j]>sum){
                j--;
            }else{
                i++;
            }
             
        }
        return list;
    }
}
```

### 题目：汇编语言中有一种移位指令叫做循环左移（ROL），现在有个简单的任务，就是用字符串模拟这个指令的运算结果。对于一个给定的字符序列S，请你把其循环左移K位后的序列输出。例如，字符序列S=”abcXYZdef”,要求输出循环左移3位后的结果，即“XYZdefabc”。是不是很简单？OK，搞定它！

### 思路：用api很轻松就可以得出答案。另一种方法，左边反转，右边反转，然后整个进行反转，最后得出结果

```
public String LeftRotateString(String str,int n) {
        return n<=str.length()?str.substring(n)+str.substring(0, n):"";
    }
```

### 题目：牛客最近来了一个新员工Fish，每天早晨总是会拿着一本英文杂志，写些句子在本子上。同事Cat对Fish写的内容颇感兴趣，有一天他向Fish借来翻看，但却读不懂它的意思。例如，“student. a am I”。后来才意识到，这家伙原来把句子单词的顺序翻转了，正确的句子应该是“I am a student.”。Cat对一一的翻转这些单词顺序可不在行，你能帮助他么？

### 思路：spilt成多个字符串，然后从后往前拼接起来就行。或者将每个单词反转，然后整个整个反转

```
public class Solution {
    public String ReverseSentence(String str) {
        if(str.trim().equals("")){
            return str;
        }
        String[] a = str.split(" ");
        StringBuffer o = new StringBuffer();
        int i;
        for (i = a.length; i >0;i--){
            o.append(a[i-1]);
            if(i > 1){
                o.append(" ");
            }
        }
        return o.toString();
    }
} 
```

### 题目：在一个长度为n的数组里的所有数字都在0到n-1的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。 例如，如果输入长度为7的数组{2,3,1,0,2,5,3}，那么对应的输出是第一个重复的数字2。

### 思路：用一个boolean数组来标志是否已经访问过，如果已经访问过，返回true

```

    public boolean duplicate(int numbers[], int length, int[] duplication) {
        boolean[] k = new boolean[length];
        for (int i = 0; i < k.length; i++) {
            if (k[numbers[i]] == true) {
                duplication[0] = numbers[i];
                return true;
            }
            k[numbers[i]] = true;
        }
        return false;
    }
```

### 题目：给定一个数组A[0,1,...,n-1],请构建一个数组B[0,1,...,n-1],其中B中的元素B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]。不能使用除法。

### 思路：可以画出一个矩形，然后先计算下三角的连乘积，然后计算上三角的连乘积，和之前同一行的下三角部分相乘

```
public class Solution {
    public int[] multiply(int[] A) {
        int length = A.length;
        int[] B = new int[length];
        if(length != 0 ){
            B[0] = 1;
            //计算下三角连乘
            for(int i = 1; i < length; i++){
                B[i] = B[i-1] * A[i-1];
            }
            int temp = 1;
            //计算上三角
            for(int j = length-2; j >= 0; j--){
                temp *= A[j+1];
                B[j] *= temp;
            }
        }
        return B;
    }
}
```

### 题目：每年六一儿童节,牛客都会准备一些小礼物去看望孤儿院的小朋友,今年亦是如此。HF作为牛客的资深元老,自然也准备了一些小游戏。其中,有个游戏是这样的:首先,让小朋友们围成一个大圈。然后,他随机指定一个数m,让编号为0的小朋友开始报数。每次喊到m-1的那个小朋友要出列唱首歌,然后可以在礼品箱中任意的挑选礼物,并且不再回到圈中,从他的下一个小朋友开始,继续0...m-1报数....这样下去....直到剩下最后一个小朋友,可以不用表演,并且拿到牛客名贵的“名侦探柯南”典藏版(名额有限哦!!^_^)。请你试着想下,哪个小朋友会得到这份礼品呢？(注：小朋友的编号是从0到n-1)

### 思路：本质上是约瑟夫环

```
public class Solution {  
    public int LastRemaining_Solution(int n, int m) {  
        if(n <= 0)  
            return -1;  
        int res = 0;  
        for(int i = 2; i <= n; i++){  
            res = (res + m) % i;  
        }  
        return res;  
    }  
}  
```


### 题目： 请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符"go"时，第一个只出现一次的字符是"g"。当从该字符流中读出前六个字符“google"时，第一个只出现一次的字符是"l"。

### 思路：创建一个hashmap，遍历字符串的所有字符，然后通过hashmap统计字符出现的次数，最后选择第一个出现一次的字符

```
public class Solution
{    
    int[] hashtable=new int[256];
    StringBuffer s=new StringBuffer();
    //Insert one char from stringstream
    public void Insert(char ch)
    {
        s.append(ch);
        if(hashtable[ch]==0)
            hashtable[ch]=1;
        else hashtable[ch]+=1;
    }
  //return the first appearence once char in current stringstream
    public char FirstAppearingOnce()
    {
      char[] str=s.toString().toCharArray();
      for(char c:str)
      {
          if(hashtable[c]==1)
              return c;
      }
      return '#';
    }
}
```

### 题目：一个链表中包含环，请找出该链表的环的入口结点。

### 思路：求出环中节点的数目，然后设置两个指针，一个指针先走n步，然后另一个才开始，当两个指针指向的节点相同时，说明这个是入口节点

```
public class Solution {
    //找到一快一满指针相遇处的节点，相遇的节点一定是在环中
    public static ListNode meetingNode(ListNode head) {
        if(head==null)
            return null;
         
        ListNode slow = head.next;
        if(slow==null)
            return null;
         
        ListNode fast = slow.next;
        while (slow != null && fast != null) {
            if(slow==fast){
                return fast;
            }
            slow=slow.next;
            fast=fast.next;
             
            if(fast!=slow){
                fast=fast.next;
            }
        }
        return null;
    }
    public ListNode EntryNodeOfLoop(ListNode pHead) {
        ListNode meetingNode=meetingNode(pHead);
        if(meetingNode==null)
            return null;
//      得到环中的节点个数
        int nodesInLoop=1;
        ListNode p1=meetingNode;
        while(p1.next!=meetingNode){
            p1=p1.next;
            ++nodesInLoop;
        }
//      移动p1
        p1=pHead;
        for(int i=0;i<nodesInLoop;i++){
            p1=p1.next;
        }
//      移动p1，p2
        ListNode p2=pHead;
        while(p1!=p2){
            p1=p1.next;
            p2=p2.next;
        }
        return p1;
    }
}
```

### 题目：给定一颗二叉搜索树，请找出其中的第k大的结点。例如， 5 / \ 3 7 /\ /\ 2 4 6 8 中，按结点数值大小顺序第三个结点的值为4。

### 思路：首先知道什么是二叉搜索树，就是左边的小于根节点，右边的大于根节点，而二叉搜索树的中序遍历刚好是从小到大的顺序

```
public class Solution {
   int index = 0; //计数器
    TreeNode KthNode(TreeNode root, int k)
    {
        if(root != null){ //中序遍历寻找第k个
            TreeNode node = KthNode(root.left,k);
            if(node != null)
                return node;
            index ++;
            if(index == k)
                return root;
            node = KthNode(root.right,k);
            if(node != null)
                return node;
        }
        return null;
    }
}
```



### 一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字。


```
//num1,num2分别为长度为1的数组。传出参数
//将num1[0],num2[0]设置为返回结果

import java.util.*;
public class Solution {
    public void FindNumsAppearOnce(int [] array,int num1[] , int num2[]) {
        HashMap <Integer,Integer>hashmap=new HashMap();
        for(int n=0;n<array.length;n++)
        {
            if(hashmap.containsKey(array[n]))
            {
                hashmap.put(array[n],2);
            }
            else
            	hashmap.put(array[n],1);
        }
        Iterator it=hashmap.keySet().iterator();
        int i=0;
        while(it.hasNext())
        {
            int key=(Integer)it.next();
            if(hashmap.get(key)==1)
            {
                if(i==0)
                {
                    num1[0]=key;
                    i++;
                }
                else
                {
                     num2[0]=key;
                    break;
                }
                    
            }
        }
    }
}
```


### 把只包含因子2、3和5的数称作丑数（Ugly Number）。例如6、8都是丑数，但14不是，因为它包含因子7。 习惯上我们把1当做是第一个丑数。求按从小到大的顺序的第N个丑数。


```

public class Solution {
    final int d[] = { 2, 3, 5 };
    public int GetUglyNumber_Solution(int index) {
        if(index == 0) return 0;
        int a[] = new int[index];
        a[0] = 1;
        int p[] = new int[] { 0, 0, 0 };
        int num[] = new int[] { 2, 3, 5 };
        int cur = 1;
 
        while (cur < index) {
            int m = finMin(num[0], num[1], num[2]);
            if (a[cur - 1] < num[m])
                a[cur++] = num[m];
            p[m] += 1;
            num[m] = a[p[m]] * d[m];
        }
        return a[index - 1];
    }
 
    private int finMin(int num2, int num3, int num5) {
        int min = Math.min(num2, Math.min(num3, num5));
        return min == num2 ? 0 : min == num3 ? 1 : 2;
    }
}
```


### 请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一个格子开始，每一步可以在矩阵中向左，向右，向上，向下移动一个格子。如果一条路径经过了矩阵中的某一个格子，则该路径不能再进入该格子。 例如 a b c e s f c s a d e e 矩阵中包含一条字符串"bcced"的路径，但是矩阵中不包含"abcb"路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入该格子。

```

public class Solution {
    public boolean hasPath(char[] matrix, int rows, int cols, char[] str) {
        int flag[] = new int[matrix.length];
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (helper(matrix, rows, cols, i, j, str, 0, flag))
                    return true;
            }
        }
        return false;
    }
 
    private boolean helper(char[] matrix, int rows, int cols, int i, int j, char[] str, int k, int[] flag) {
        int index = i * cols + j;
        if (i < 0 || i >= rows || j < 0 || j >= cols || matrix[index] != str[k] || flag[index] == 1)
            return false;
        if(k == str.length - 1) return true;
        flag[index] = 1;
        if (helper(matrix, rows, cols, i - 1, j, str, k + 1, flag)
                || helper(matrix, rows, cols, i + 1, j, str, k + 1, flag)
                || helper(matrix, rows, cols, i, j - 1, str, k + 1, flag)
                || helper(matrix, rows, cols, i, j + 1, str, k + 1, flag)) {
            return true;
        }
        flag[index] = 0;
        return false;
    }
}

```


### 地上有一个m行和n列的方格。一个机器人从坐标0,0的格子开始移动，每一次只能向左，右，上，下四个方向移动一格，但是不能进入行坐标和列坐标的数位之和大于k的格子。 例如，当k为18时，机器人能够进入方格（35,37），因为3+5+3+7 = 18。但是，它不能进入方格（35,38），因为3+5+3+8 = 19。请问该机器人能够达到多少个格子？

```


public class Solution {
 
    public int movingCount(int threshold, int rows, int cols) {
        int flag[][] = new int[rows][cols]; //记录是否已经走过
        return helper(0, 0, rows, cols, flag, threshold);
    }
 
    private int helper(int i, int j, int rows, int cols, int[][] flag, int threshold) {
        if (i < 0 || i >= rows || j < 0 || j >= cols || numSum(i) + numSum(j)  > threshold || flag[i][j] == 1) return 0;    
        flag[i][j] = 1;
        return helper(i - 1, j, rows, cols, flag, threshold)
            + helper(i + 1, j, rows, cols, flag, threshold)
            + helper(i, j - 1, rows, cols, flag, threshold)
            + helper(i, j + 1, rows, cols, flag, threshold)
            + 1;
    }
 
    private int numSum(int i) {
        int sum = 0;
        do{
            sum += i%10;
        }while((i = i/10) > 0);
        return sum;
    }
}
```

### LL今天心情特别好,因为他去买了一副扑克牌,发现里面居然有2个大王,2个小王(一副牌原本是54张^_^)...他随机从中抽出了5张牌,想测测自己的手气,看看能不能抽到顺子,如果抽到的话,他决定去买体育彩票,嘿嘿！！“红心A,黑桃3,小王,大王,方片5”,“Oh My God!”不是顺子.....LL不高兴了,他想了想,决定大\小 王可以看成任何数字,并且A看作1,J为11,Q为12,K为13。上面的5张牌就可以变成“1,2,3,4,5”(大小王分别看作2和4),“So Lucky!”。LL决定去买体育彩票啦。 现在,要求你使用这幅牌模拟上面的过程,然后告诉我们LL的运气如何。为了方便起见,你可以认为大小王是0。
```
import java.util.*;
public class Solution {
    public boolean isContinuous(int [] numbers) {
		if(numbers.length<5)
            return false;
        //统计1的个数
        int count=0;
        for(int n=0;n<numbers.length;n++)
        {
            if(numbers[n]==0)
                count++;
        }
        //进行排序
        Arrays.sort(numbers);
        //记录最小的非0数
        int min=numbers[count];
        for(int n=count;n<numbers.length-1;n++)
        {
            //相邻两个非0数的间隔
            int gap=numbers[n+1]-numbers[n];
            //如果间隔大于0的个数，说明癞子不够，直接返回
            if(gap>1)
            {
            	if(gap-1>count)
                	return false;
            	else
                	count=count-gap+1;
            }
            
        }
        
        if(count>0&&min-count>0)
            return true;
        else if(count==0||count==4)
            return true;
        else
            return false;
    }
}
```

### 给定一个二叉树和其中的一个结点，请找出中序遍历顺序的下一个结点并且返回。注意，树中的结点不仅包含左右子结点，同时包含指向父结点的指针

```
public class Solution {
    TreeLinkNode GetNext(TreeLinkNode node)
    {
        if(node==null) return null;
        if(node.right!=null){    //如果有右子树，则找右子树的最左节点
            node = node.right;
            while(node.left!=null) node = node.left;
            return node;
        }
        while(node.next!=null){ //没右子树，则找第一个当前节点是父节点左孩子的节点
            if(node.next.left==node) return node.next;
            node = node.next;
        }
        return null;   //退到了根节点仍没找到，则返回null
    }
}
```

### 对称的二叉树
```
public class Solution {
    boolean isSymmetrical(TreeNode pRoot) {
        if(pRoot == null){
            return true;
        }
        return nodeIsSymmetrical(pRoot.left , pRoot.right);
    }

    private boolean nodeIsSymmetrical(TreeNode left, TreeNode right) {
        if(left == null){
            return right == null;
        }
        if(right == null){
            return false;
        }
        if(left.val != right.val){
            return false;
        }
        return nodeIsSymmetrical(left.left , right.right) && nodeIsSymmetrical(left.right , right.left);
    }
}
```

### 把二叉树打印成多行

```
public class Solution {
    ArrayList<ArrayList<Integer> > Print(TreeNode pRoot) {
    	ArrayList <ArrayList<Integer>> lists=new ArrayList();
        if(pRoot==null)
            return lists;
        LinkedList <TreeNode>queue=new LinkedList();
        queue.offer(pRoot);
        int count=1;
        while(queue.size()!=0)
        {
            //遍历每一层
            count=queue.size();
            ArrayList <Integer> list=new ArrayList();
            while(count!=0)
            {
                TreeNode node=queue.poll();
                count--;
                list.add(node.val);
                if(node.left!=null)
                    queue.offer(node.left);
                if(node.right!=null)
                    queue.offer(node.right);
            
            }
            lists.add(list);
        }
        return lists;
    }
    
}
```

### 求1+2+....n
```


class Solution {


public int Sum_Solution(int n) {
        int sum = n;
        boolean ans = (n>0)&&((sum+=Sum_Solution(n-1))>0);
        return sum;
    }
}
```

### 树的子结构

```

public class Solution {
    public boolean HasSubtree(TreeNode root1,TreeNode root2) {
        boolean result = false;
            if(root1 != null && root2 != null){
                if(root1.val == root2.val){
                    result = DoesTree1HaveTree2(root1,root2);
                }
                if(!result){result = HasSubtree(root1.left, root2);}
                if(!result){result = HasSubtree(root1.right, root2);}
            }
            return result;
    }
    public boolean DoesTree1HaveTree2(TreeNode root1,TreeNode root2){
            if(root1 == null && root2 != null) return false;
            if(root2 == null) return true;
            if(root1.val != root2.val) return false;
            return DoesTree1HaveTree2(root1.left, root2.left) && DoesTree1HaveTree2(root1.right, root2.right);
        }
}
```

### 删除链表中重复的节点
```


public class Solution {
    public ListNode deleteDuplication(ListNode pHead) {
        if (pHead == null || pHead.next == null) { // 只有0个或1个结点，则返回
            return pHead;
        }
        if (pHead.val == pHead.next.val) { // 当前结点是重复结点
            ListNode pNode = pHead.next;
            while (pNode != null && pNode.val == pHead.val) {
                // 跳过值与当前结点相同的全部结点,找到第一个与当前结点不同的结点
                pNode = pNode.next;
            }
            return deleteDuplication(pNode); // 从第一个与当前结点不同的结点开始递归
        } else { // 当前结点不是重复结点
            pHead.next = deleteDuplication(pHead.next); // 保留当前结点，从下一个结点开始递归
            return pHead;
        }
    }
}

```

### 序列化二叉树

```


public class Solution {
    public int index = -1;
    String Serialize(TreeNode root) {
        StringBuffer sb = new StringBuffer();
        if(root == null){
            sb.append("#,");
            return sb.toString();
        }
        sb.append(root.val + ",");
        sb.append(Serialize(root.left));
        sb.append(Serialize(root.right));
        return sb.toString();
  }
    TreeNode Deserialize(String str) {
        index++;
       int len = str.length();
        if(index >= len){
            return null;
        }
        String[] strr = str.split(",");
        TreeNode node = null;
        if(!strr[index].equals("#")){
            node = new TreeNode(Integer.valueOf(strr[index]));
            node.left = Deserialize(str);
            node.right = Deserialize(str);
        }
         
        return node;
  }
}
```