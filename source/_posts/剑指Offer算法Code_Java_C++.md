---
title: 剑指Offer算法Code_Java_C++(0820更新)
date: 2018-08-16 09:39:40
tags: [Java, C++, 算法]
toc: true
---

剑指Offer算法Code_Java_C++

<!--more-->
### 1
在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
>思路：从左下角元素往上查找，右边元素是比这个元素大，上边是的元素比这个元素小。
Java代码
```
public class Solution {
    public boolean Find(int target, int [][] array) {
        //填写
        int row = array.length;
        int col = array[0].length;
        int i=row-1,j=0;
        while(i>=0&&j<=col-1){
            if(target<array[i][j]){
                i--;
            }else if(target>array[i][j]){
                j++;
            }else
                return true;
        }
        return false;
    }
}
```
C++代码
```
class Solution {
public:
    bool Find(int target, vector<vector<int> > array) {
        // array是二维数组，这里没做判空操作
        int rows = array.size();
        int cols = array[0].size();
        int i=rows-1,j=0;//左下角元素坐标
        while(i>=0 && j<cols){//使其不超出数组范围
            if(target<array[i][j])
                i--;//查找的元素较少，往上找
            else if(target>array[i][j])
                j++;//查找元素较大，往右找
            else
                return true;//找到
        }
        return false;
    }
};
```

### 2
请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。
Java代码：
```
public class Solution {
    public String replaceSpace(StringBuffer str) {
    	String str1 = str.toString();
        String str2 = str1.replace(" ","%20");
        return str2;
    }
}
```
Java代码：
```
public class Solution {
    public String replaceSpace(StringBuffer str) {
        int spacenum = 0;//spacenum为计算空格数
        for(int i=0;i<str.length();i++){
            if(str.charAt(i)==' ')
                spacenum++;
        }
        int indexold = str.length()-1; //indexold为为替换前的str下标
        int newlength = str.length() + spacenum*2;//计算空格转换成%20之后的str长度
        int indexnew = newlength-1;//indexold为为把空格替换为%20后的str下标
        str.setLength(newlength);//使str的长度扩大到转换成%20之后的长度,防止下标越界
        for(;indexold>=0 && indexold<newlength;--indexold){ 
                if(str.charAt(indexold) == ' '){  //
                str.setCharAt(indexnew--, '0');
                str.setCharAt(indexnew--, '2');
                str.setCharAt(indexnew--, '%');
                }else{
                    str.setCharAt(indexnew--, str.charAt(indexold));
                }
        }
        return str.toString();
    }
}
```

c++代码
```
class Solution {
public:
	void replaceSpace(char *str,int length) {
    int count = 0;
        for (int i=0;i<length;i++){
            if (str[i]==' '){
                count++;
            }
            for (int i=length-1;i>=0;i--){
                if (str[i]==' '){
                    count--;
                  str[i+2*count]='%';
                str[i+2*count+1]='2';
                str[i+2*count+2]='0';
                }else{
                      str[i+2*count]=str[i];
                }
            }
        }
	}
};
```
### 3
输入一个链表，按链表值从尾到头的顺序返回一个ArrayList。

Java代码：
```
java 递归超简洁版本
public class Solution {
    ArrayList<Integer> arrayList=new ArrayList<Integer>();
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        if(listNode!=null){
            this.printListFromTailToHead(listNode.next);
            arrayList.add(listNode.val);
        }
        return arrayList;
    }
}
```
C++代码
```
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        vector<int> value;
        if (head != NULL){
            value.insert(value.begin(),head->val);
            while (head->next !=NULL){
                value.insert(value.begin(),head->next->val);
                head = head ->next;
            }
        }
        return value;
    }
};
```
### 4
输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。
>递归思想，每次将左右两颗子树当成新的子树进行处理，中序的左右子树索引很好找，前序的开始结束索引通过计算中序中左右子树的大小来计算，然后递归求解，直到startPre>endPre||startIn>endIn说明子树整理完到。方法每次返回左子树活右子树的根节点
```
      1
     /  \
   2     3
  /\    /
 4  5  6
  \    /
   7  8
```
Java代码：
```
public class Solution {
    public TreeNode reConstructBinaryTree(int [] pre,int [] in) {
        TreeNode root=reConstructBinaryTree(pre,0,pre.length-1,in,0,in.length-1);
        return root;
    }
    //前序遍历{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}
    private TreeNode reConstructBinaryTree(int [] pre,int startPre,int endPre,int [] in,int startIn,int endIn) {
         
        if(startPre>endPre||startIn>endIn)
            return null;
        TreeNode root=new TreeNode(pre[startPre]);
         
        for(int i=startIn;i<=endIn;i++)
            if(in[i]==pre[startPre]){
                root.left=reConstructBinaryTree(pre,startPre+1,startPre+i-startIn,in,startIn,i-1);
                root.right=reConstructBinaryTree(pre,i-startIn+startPre+1,endPre,in,i+1,endIn);
                      break;
            }
                 
        return root;
    }
}
```

### 5
大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0）。
n<=39

Java代码
```
public class Solution {
    public int Fibonacci(int n) {
        if(n<1){
            return n;
        }
        int[] ints = new int[n+1];
        ints[0] = 0;
        ints[1] = 1;
        
        for(int i = 2; i <= n; i++ ){
            ints[i] = ints[i-1] + ints[i-2];
        }
        return ints[n];
    }
}
```
C++代码：
```
class Solution {
public:
    int Fibonacci(int n) {
    int pre = 0;
        int last=1;
            int result =0;
        if(n<=1){
            return n;
        }
        for(int i=2; i<=n; i++){
            result=pre+last;
            pre=last;
            last=result;
        }
        return result;
    }
};
```

### 6

一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。
>思路：，f(1) = 1, f(2) = 2, f(3) = 3, f(4) = 5，  可以总结出f(n) = f(n-1) + f(n-2)的规律
Java代码：
```
public class Solution {
    public int JumpFloor(int target) {
        int[] ints= new int[target+1];
        if(target <=0 ){
            return 0;
        }else if(target==1 || target==2){
            return target;
        }
        ints[0] = 1;ints[1] = 2;
        for(int i =2; i<=target; i++){
            ints[i] = ints[i-1] + ints[i-2];
           }
        return ints[target-1];
    }
}
```
C++代码
```
class Solution {
public:
    int jumpFloor(int number) {
        int first = 1;int second = 2; int result = 0;
        if (number<=0){
            return 0;
        }else if (number==1||number==2){
            return number;
        }
        for (int i=3; i<=number; i++){
            result = first + second;
            first = second;
            second = result;
        }
        return result;
    }
};
```
### 7

输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。
>思路：1自身左移动，然后跟原数字做**与**比较，如果对应相同输出为1，否则为0。
Java代码：
```
public class Solution {
    public int NumberOf1(int n) {
    int count = 0;
        int flag = 1;
        while(flag != 0){
            if((n & flag) !=0 ){
                count++;
            }
            flag = flag << 1;
        }
        return count;
    }
}
```

C++代码：
```
class Solution {
public:
     int  NumberOf1(int n) {
         int count = 0;
         int flag = 1;
         while(flag != 0){
             if((n & flag)!=0){
                 count++;    
             }
             flag = flag << 1;
         }
        return count   ;  
     }
    
};
```
### 8

输入一个链表，反转链表后，输出新链表的表头:
>整体反转链表，但是要把断开的节点保存起来，才能继续反转链表
Java代码： 
```
public class Solution {
    public ListNode ReverseList(ListNode head) {
       
        if(head==null)
            return null;
        //head为当前节点，如果当前节点为空的话，那就什么也不做，直接返回null；
        ListNode pre = null;
        ListNode next = null;
        //当前节点是head，pre为当前节点的前一节点，next为当前节点的下一节点
        //需要pre和next的目的是让当前节点从pre->head->next1->next2变成pre<-head next1->next2
        //即pre让节点可以反转所指方向，但反转之后如果不用next节点保存next1节点的话，此单链表就此断开了
        //所以需要用到pre和next两个节点
        //1->2->3->4->5
        //1<-2<-3 4->5
        while(head!=null){
            //做循环，如果当前节点不为空的话，始终执行此循环，此循环的目的就是让当前节点从指向next到指向pre
            //如此就可以做到反转链表的效果
            //先用next保存head的下一个节点的信息，保证单链表不会因为失去head节点的原next节点而就此断裂
            next = head.next;
            //保存完next，就可以让head从指向next变成指向pre了，代码如下
            head.next = pre;
            //head指向pre后，就继续依次反转下一个节点
            //让pre，head，next依次向后移动一个节点，继续下一次的指针反转
            pre = head;
            head = next;
        }
        //如果head为null的时候，pre就为最后一个节点了，但是链表已经反转完毕，pre就是反转后链表的第一个节点
        //直接输出pre就是我们想要得到的反转后的链表
        return pre;
    }
}
```

C++代码：
```
class Solution {
public:
    ListNode* ReverseList(ListNode* pHead) {

        if(pHead == NULL){
            return NULL;
        }
        
        ListNode* pNode = pHead;//当前指针
        ListNode* pPre = NULL;//链表的前一个指针
        ListNode* pNewHead = NULL;
        
        while(pNode != NULL){
           ListNode* pNext = pNode->next;
            if(pNext == NULL){ //尾节点
                pNewHead = pNode;
            }
            pNode->next = pPre;
            pPre = pNode;
            pNode = pNext;
        }
        return pNewHead;
    }
};
```
### 9
输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。
>两两数值对比,merge可以合并两个事物，链表也行，考点在取两个链表比较小的头节点

Java代码：
```
public class Solution {
    public ListNode Merge(ListNode list1,ListNode list2) {
        if(list1 == null){
            return list2;
        }
        if(list2 == null){
            return list1;
        }
        if(list1.val <= list2.val){
            list1.next = Merge(list1.next,list2);
                return list1;
              }else{
            list2.next = Merge(list1,list2.next);
            return list2;
        }
    }
}
```

C++代码：
```
class Solution {
public:
    ListNode* Merge(ListNode* pHead1, ListNode* pHead2)
    {
     if(pHead1 == NULL){
            return pHead2;
        }
        if(pHead2 == NULL){
            return pHead1;
        }
        
        ListNode* NewHead = NULL;
        if(pHead1->val <= pHead2->val){
            NewHead = pHead1;
            NewHead->next = Merge(pHead1->next,pHead2);
        }else{
            NewHead = pHead2;
            NewHead->next = Merge(pHead1,pHead2->next);
        }
        return NewHead;
    }
};
```
### 10
 从上往下打印出二叉树的每个节点，同层节点从左至右打印。

Java代码：
```
/**
思路是用arraylist模拟一个队列来存储相应的TreeNode
*/
public class Solution {
    public ArrayList<Integer> PrintFromTopToBottom(TreeNode root) {
        ArrayList<Integer> arr = new ArrayList<>();
        ArrayList<TreeNode> TN = new ArrayList<>();
        if(root==null){
            return arr;
        }
        TN.add(root);
        while(TN.size()!=0){
            TreeNode temp = TN.remove(0);
            if(temp.left!= null){
                TN.add(temp.left);
            }
            if(temp.right!= null){
                TN.add(temp.right);
            }
            arr.add(temp.val);
        }
        return arr;
    }
}
```
C++代码：
```
```

### 11
1个整型数组里除了两个数字之外，其他的数字都出现了偶数次。请写程序找出这两个只出现一次的数字。
>思路：两个相同数字异或=0，一个数和0异或还是它本身。<br>
我们首先还是先异或，剩下的数字肯定是A、B异或的结果，这个结果的二进制中的1，表现的是A和B的不同的位。我们就取第一个1所在的位数，假设是第3位，接着把原数组分成两组，分组标准是第3位是否为1。如此，相同的数肯定在一个组，因为相同数字所有位都相同，而不同的数，肯定不在一组。然后把这两个组按照最开始的思路，依次异或，剩余的两个结果就是这两个只出现一次的数字。

Java代码：
```
public class Solution {
    public void FindNumsAppearOnce(int[] array, int[] num1, int[] num2)    {
        int length = array.length;
        if(length == 2){
            num1[0] = array[0];
            num2[0] = array[1];
            return;
        }
        int bitResult = 0;
        for(int i = 0; i < length; ++i){
            bitResult ^= array[i];
        }
        int index = findFirst1(bitResult);
        for(int i = 0; i < length; ++i){
            if(isBit1(array[i], index)){
                num1[0] ^= array[i];
            }else{
                num2[0] ^= array[i];
            }
        }
    }
     
    private int findFirst1(int bitResult){
        int index = 0;
        while(((bitResult & 1) == 0) && index < 32){
            bitResult >>= 1;
            index++;
        }
        return index;
    }
     
    private boolean isBit1(int target, int index){
        return ((target >> index) & 1) == 1;
    }
}
```

C++代码：
```
链接：https://www.nowcoder.com/questionTerminal/e02fdb54d7524710a7d664d082bb7811
来源：牛客网

class Solution {
public:
    void FindNumsAppearOnce(vector<int> data,int* num1,int *num2) {
  if(data.size()<2)
   return ;
  int size=data.size();
  int temp=data[0];
  for(int i=1;i<size;i++)
   temp=temp^data[i];
  if(temp==0)
   return ;
  int index=0;
  while((temp&1)==0){
   temp=temp>>1;
   ++index;
  }
  *num1=*num2=0;
  for(int i=0;i<size;i++)
  {
   if(IsBit(data[i],index))
    *num1^=data[i];
   else
    *num2^=data[i];
  }
    }
 bool IsBit(int num,int index)
 {
  num=num>>index;
  return (num&1);
 }
};
```
 ^=:逐位异或 

### 12
最小的k个数
输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

Java代码：(快排/最小堆)
```
链接：https://www.nowcoder.com/questionTerminal/6a296eb82cf844ca8539b57c23e6e9bf
来源：牛客网

/*
*基于堆排序算法，构建最大堆。时间复杂度为O(nlogk)
*如果用快速排序，时间复杂度为O(nlogn)；
*如果用冒泡排序，时间复杂度为O(n*k)
*/
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
        ArrayList<Integer> list=new ArrayList<Integer>();
        //检查输入的特殊情况
        if(input==null || input.length<=0 || input.length<k){
            return list;
        }
        //构建最大堆
        for(int len=k/2-1; len>=0; len--){
            adjustMaxHeapSort(input,len,k-1);
        }
        //从第k个元素开始分别与最大堆的最大值做比较，如果比最大值小，则替换并调整堆。
        //最终堆里的就是最小的K个数。
        int tmp;
        for(int i=k; i<input.length; i++){
            if(input[i]<input[0]){
                tmp=input[0];
                input[0]=input[i];
                input[i]=tmp;
                adjustMaxHeapSort(input,0,k-1);
            }
        }
        for(int j=0; j<k; j++){
            list.add(input[j]);
        }
        return list;
    }
     
    public void adjustMaxHeapSort(int[] input, int pos, int length){
        int temp;
        int child;
        for(temp=input[pos]; 2*pos+1<=length; pos=child){
            child=2*pos+1;
            if(child<length && input[child]<input[child+1]){
                child++;
            }
            if(input[child]>temp){
                input[pos]=input[child];
            }else{
                break;
            }
        }
        input[pos]=temp;
    }
}
```
### 二叉树的景象
```
题目描述
操作给定的二叉树，将其变换为源二叉树的镜像。
输入描述:
二叉树的镜像定义：源二叉树 
    	    8
    	   /  \
    	  6   10
    	 / \  / \
    	5  7 9 11
    	镜像二叉树
    	    8
    	   /  \
    	  10   6
    	 / \  / \
    	11 9 7  5
```
C++代码：
```
```

### 13


Java代码：
```
public class Solution {
    public void Mirror(TreeNode root) {
        if(root == null){
            return;
        }
        
        
        TreeNode temp;
        if(root!=null){
            temp = root.left;
            root.left = root.right;
            root.right = temp;
        }
        if(root.left!=null){
            Mirror(root.left);
            }
        if(root.right!=null){
            Mirror(root.right);
        }
    }
}
```

C++代码：
```
```




Java代码：
```
```
C++代码：
```
```



Java代码：
```
```

C++代码：
```
```




Java代码：
```
```

C++代码：
```
```




Java代码：
```
```
C++代码：
```
```