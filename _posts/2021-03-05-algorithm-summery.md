---
layout: post
title: algorithm summery
categories: 学习
description: note
keywords: divide and conquer
---

<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>





# 1 分治

## 1.1 思想定义

* 原问题可分解为几个规模较小，但类似于原问题的子问题。

* 递归地求解这些子问题。

* 合并子问题的解得到原问题的解。

## 1.2 举例

### 1.2.1  归并排序

* 分解待排序的n个元素为各有n/2个元素的两个子序列。
* 使用归并排序递归地排序两个子序列。
* 合并两个已排序的子序列产生最终的排序。

```c++
#include<vector>
#include<iostream>
using std::vector;
using std::cout;
using std::endl;
void  merge(vector<int>&input,int p,int q,int r)
        {
            vector<int> temp;
            temp.clear();
            int i=p,j=q+1;
            while(i<=q&&j<=r)
            {
                if(input[i]>input[j])
                    temp.push_back(input[j++]);
                else
                    temp.push_back(input[i++]);
            }
            while (i<=q)
            {
                temp.push_back(input[i++]);
            }
            while(j<=q)
            {
                temp.push_back(input[j++]);
            }
            i=p,j=0;
            while(j<temp.size())
                input[i++]=temp[j++];
            temp.clear();
            temp.shrink_to_fit();//释放内存
            return;
        }

        void mergesort(vector<int>&input,int low,int high)
        {
            if(low<high)
            {
                int mid=(low+high)/2;
                mergesort(input,low,mid);
                mergesort(input,mid+1,high);
                merge(input,low,mid,high);
            }

        }

```

# 2 动态规划

## 2.1 基本思想

* 刻画最优解的结构；
* 递归定义最优解的值；
* 计算最优解的值；
  * 两种方式，自底向上或者自顶向下。
* 利用计算出的信息刻画最优解。
* 思考：局部最大不一定是全局最大？

## 2.2 典型问题

### 2.2.1 背包问题

#### 2.2.1.1 0-1背包

##### 条件

V:背包容量（可装物品的总重量）;

N: 物品个数；

C[N]: 物品重量；

V[N]: 一个物品放入背包后所获得的价值；

##### 问题

求如何放哪些物品使得获得的总价值最大。

##### 转移方程

$F[i][j]$:容量为j的背包放入前i个物品可以获得的最大价值为:不放第i个物品时所获得的最大价值加上放第i个物品时所获得的最大价值二者之间的最大值。

$F[i][j]=max(F[i-1][j],F[i-1][j-C[i]]+V[i])$ 

### 2.2.2 零钱兑换

### 2.2.3 一些关键词

**最长**:  [300. 最长递增子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence)；[剑指 Offer 42. 连续子数组的最大和](https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof)；==[5. 最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring)==；[516. 最长回文子序列](https://leetcode-cn.com/problems/longest-palindromic-subsequence)；[1143. 最长公共子序列](https://leetcode-cn.com/problems/longest-common-subsequence)；

**最小**：[120. 三角形最小路径和](https://leetcode-cn.com/problems/triangle)；

**跳楼梯**；

**零钱兑换**；

**子串**：[647. 回文子串](https://leetcode-cn.com/problems/palindromic-substrings/)

```c++
 int countSubstrings_(string s) {

        int i,j;
        int num=0;
        int n=s.size();

        //dp[i][j]: s[i:j]是否为回文串
        
        vector<vector<bool>> dp(n,vector<bool>(n,false));

        for(i=0;i<n;i++)
            dp[i][i]=true;

        //从下往上遍历
        for(i=n-1;i>=0;i--){

            // 从左往右
            for(j=i;j<n;j++){
                if(s[i]==s[j]){
                    // 相差不超过1，子串长度为1或者2
                    if(j-i<=1){
                        dp[i][j]=true;
                        num++;
                    // 长度超过2
                    }else if(dp[i+1][j-1]){
                        num++;
                        dp[i][j]=true;
                    }
                }
            }
        }

        return num;
    }
```

> 遍历顺序的思考：
>
> ​	dp\[i]\[j] 依赖于dp\[i+1]\[j-1]
>
> ​	即：i+1->i  j-1->j 则遍历顺序为从下往上，从左往右。
>
> ​    以一个长度为3的字符串为例：
>
> ![image-20210827102739277](E:\SelfStudy\DamonWang888.github.io\_posts\images\image-20210827102739277.png)

### 2.2.4 

一维动态规划

```
dp[i]
i 表示下标范围0~i。如连续子数组的最大和。
```

二维动态规划

```
dp[i][j]
i,j可以表示范围。如最长回文子序列，最长公共子序列。
i,j分别表示，i表示一种变量，j表示另外一种变量。如背包问题中分别表示物品编号范围和背包容量。

```

## 2.3 注意事项

* dp数组下标及其含义；
* 递推公式；
* dp数组如何初始化；
* 遍历顺序；
* 调试：打印dp数组。

# 3 贪心

## 3.1 基本思想

* 找出问题的最优子结构；
* 设计一个递归算法来求解问题；
* 在每个决策点做出当前看来是最优的决策，并且做出当前决策以后只剩下一个待求解子问题。
* 这种启发式策略并不能总是找到最优解，但是对某些问题确实可以求得最优解。

## 3.2 实例

哈夫曼编码



# 4 图拓扑排序(活动安排)

## 4.1 基本思想

图遍历算法的一种，基于图中节点的先后顺序，来遍历节点。没有先后关系的节点可以任意排序。

## 4.2 求最小生成树

### 4.2.1 Prim（选顶点）

每一步都会为一棵生长中的树添加一条==边==，该树最开始只有一个[顶点](https://zh.wikipedia.org/wiki/顶点_(图论))，然后会添加V-1条边。每次总是添加生长中的树和树中除该生长的树以外的部分形成的切分的具有最小权值的横切边。

> 时间复杂度：
>
> 邻接矩阵：o($v^2$)
>
> 邻接表：o(elog(e))

### 4.2.2 Kruskal （选边）

按照边的==权重==顺序（从小到大）将边加入生成树中，但是若加入该边会与生成树形成环则不加入该边。直到树中含有v-1条边为止。这些边组成的就是该图的最小生成树。

# 5 二叉树遍历/查找

##  5.1 深度优先

### 5.1.1 递归

### 5.1.2 非递归

## 5.2 广度优先

###  5.2.1 递归

### 5.2.2 非递归

# 6 二分
## 6.1 元素全部有序

## 6.2 元素部分有序

[611. 有效三角形的个数](https://leetcode-cn.com/problems/valid-triangle-number)



# 7 排序
## 7.1 稳定排序
插入，冒泡，归并。
## 7.2 非稳定排序
快排，堆排，希尔，直接选择。

==快排+链表==

# 8 回溯法模板

## 8.1 枚举子集

相当于1个篓子，里面有n个数字，选n次，分别选择0，1，2，3，...，n个数字，求所有不同的选择情况。明显什么都不选有一种情况，每次选1个有n种情况，每次选两个有$c^2_n$种情况。。。

```c++
vector<int> t;
void dfs(int cur, int n) {
    if (cur == n) {
        // 记录答案
        // ...
        return;
    }
    // 考虑选择当前位置
    t.push_back(cur);
    dfs(cur + 1, n);
    t.pop_back();
    // 考虑不选择当前位置
    dfs(cur + 1, n);
}

```

## 8.1 全排列

相当于1个篓子，里面有n个数字，选n次作为一次选择情况，求所有不同的选择情况。

``` c++
void collection(vector<vector<int>> &res,vector<int>&cur,vector<int>&nums,int n,vector<int> &used){
    //候选元素达到排列总数，存储当前排列并返回
    if(cur.size()==n){
        res.push_back(cur);
        return;
    }
    //遍历所有候选，生成以每一个候选元素为起点的排列
    for(int i=0;i<used.size();i++){
        if(used[i]==0){
            cur.push_back(nums[i]);
            //标记已使用
            used[i]=1;
            collection(res,cur,nums,n,used);
            //弹出已选元素并标记复位
            cur.pop_back();
            used[i]=0;
        }
    }
}
```

## 8.2 电话号码的字母组合

相当于n个篓子，每个里面有若个数字，各个数字互不相同，每次只能从篓子里面选一个数字，求能选的数字的所有组合。因为每次只能从一个篓子里面选数字，不存在一次组合中需要从一个篓子里面取两次数字，因此不需要像全排列那样记录已经选过的，防止出现一个数字被选两次的情况。

```c++
 void num_dfs(vector<string> &total_str,int index,vector<string> &res,string cur){
        if(cur.size()==total_str.size()){
            res.push_back(cur);
            return;
        }
        if(index<total_str.size()){

            for(auto &it:total_str[index]){
                cur+=it;
     
                num_dfs(total_str,index+1,res,cur);
                cur.pop_back();
            }
        }
    }

```

## 8.3 组合总和

相当于1个篓子，里面有n个数字，任意选取(一个数字可以选择多次，当然可以不选)，求所有使得选择的数字和总和为某一给定目标和的数字选择情况。==是带条件的子集，组合选择问题==。

```c++
  void add_elment(vector<int>&candidates,int index,int target,vector<int>&res,vector<vector<int>>&final_res){
       //下标越界
       if(index==candidates.size())
            return;
      	//满足条件
        if(target==0){
            final_res.push_back(res);
            return;
        }
      	// 不选不用判断
      	//不选当前:从后往前回溯，进行本次选择前先选择下一个位置
        add_elment(candidates,index+1,target,res,final_res);
      
       	// 选择需要判断
        //选择当前:更新下一次选择的目标和，下一次选择尝试继续选择当前
        if(target-candidates[index]>=0){
            res.push_back(candidates[index]);
            add_elment(candidates,index,target-candidates[index],res,final_res);
            res.pop_back();
        }
    }
```

## 8.4 目标和

```c++
void sumdfs(vector<int> &nums,int index,int target,int sum,int &total){
      
        if(index==nums.size()){
            if(sum==target)
                total++;
        }
        else{
            sumdfs(nums,index+1,target,sum+nums[index],total); //选这个元素
            sumdfs(nums,index+1,target,sum-nums[index],total); //不选这个元素
        }
    }
```



# 9 TF-IDF

TF-IDF(term frequency-inverse document frequency) 词频-逆文档频率，一种统计方法。基于思想：**字词的重要性随着它在文件中出现的次数成正比增加，但同时会随着它在语料库中出现的频率成反比下降。总结就是, 一个词语在一篇文章中出现次数越多, 同时在所有文档中出现次数越少, 越能够代表该文章。**

一个衡量某一个单词对一篇文档重要性的指标。

$TF_w=\frac{w在文件/文档中出现的次数}{文档总数N}$

$IDF=log\frac{语料/文件库所有文件总数}{包含词条w的文档数+1}$

$TF-IDF=TF*IDF$

# 10 字符串如何去重

* 关心字符串顺序，直接比较。
* 如果不关心字符串顺序
  * 用一个26位的数组统计字符串中每个字符出现的次数，再比较即可；
  * 将字符串按字典序排序后比较。
* 利用set。

# 11 一些思路

* 两次遍历
  * 记录一些跟某个位置元素前后元素相关信息，便于后续操作。
  * 相关信息：元素出现次数。

* 先排序后遍历
  * 便于找最大，最小，中位数（最中间两个数值的平均数）。
  * 排序后方便利用元素的大小信息，省去不必要的遍历次数。
    * [15. 三数之和](https://leetcode-cn.com/problems/3sum)
    * [18. 四数之和](https://leetcode-cn.com/problems/4sum)

* 一边遍历一遍统计
  * [560. 和为K的子数组](https://leetcode-cn.com/problems/subarray-sum-equals-k)
  * [1. 两数之和](https://leetcode-cn.com/problems/two-sum)

# 12 哈希

* 建立映射，常数时间定位。
  * 元素到出现次数
  * 元素到元素
    * [560. 和为K的子数组](https://leetcode-cn.com/problems/subarray-sum-equals-k)

