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