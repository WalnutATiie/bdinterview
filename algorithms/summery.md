## 1. Data Structure
### 1.1 线性表、链表, 队列, 堆栈
线性表
链表: 链表相加（进位与长度不一的边界问题）、链表部分翻转（给定区间翻转）、链表去重（删除节点）、链表划分（快速排序）、链表公共节点（链表长度，遍历）  
队列：图的拓扑排序（DAG）、最短路径条数（单源最短路径退化成广度优先搜索）  
堆栈：括号匹配（栈）、逆波兰表达式（栈）、树的三种遍历的递归与非递归形式（后序遍历非递归，双栈）  
### 1.2 字符串
字符串处理（学会借助std::string与STL中的api）  
字符串循环移位（三次拷贝、(x'y')'=yx）  
LCS、LIS（动态规划、二维长度数组、滚动数组、LIS转化成LCS）  
字符串全排列（递归、有重复字母递归、非递归借助字典序下一个排列、哈希降低时间复杂度）、字典序的下一个排列  
字符串编辑距离（动态规划）
字符串旋转  
最长回文子串（Manacher算法）  
atoi实现       
KMP  
DFA、NFA与正则表达式  
海量字符串还是要借助于Trie树、哈希、BF    
### 1.3数组
天平称量问题（理论下界、3^n>=12*2）  
局部最大值（二分查找）  
第一个缺失的整数（循环不变式）  
旋转数组的最小值（二分查找）  
寻找0子数组（和数组相邻元素差的绝对值的最小值）  
最大子数组和（DP）  
荷兰国旗问题（快速排序中的partition思想）  
Cantor数组  
排序数组最大间隔  
子集和数问题    
### 1.4 树
树转换成二叉树（左孩子右兄弟）  
二叉查找树：增删改查（删右子树最左子孙代替删除位置）  
先序中序后序层次遍历：递归、非递归；先中求后、中后求先  
平衡二叉树：  
- 四种分类：LL、LR、RL、RR  
- 四种旋转：左旋和右旋、单旋转和双旋转  
- 增删改查

堆
B树及其变种：分裂合并节点、B树与B+树区别  
其他树：RB-tree、区间树、二项堆、fibonacci堆
应用：huffman树、字典树(双数组字典树)、线段树、并查集  
#### trie树
字典树对应有限状态自动机    
双数组字典树（待总结）  
### 1.5 图
并查集  
图的存储：链接表、链接矩阵、稀疏图存储  
最短路径：Dijkstra、Floyd、Bellman-Ford  
最小生成树：Prim、Kruskal、带权的最小生成树  
图搜索：DFS、BFS、A*、alpha/beta剪枝 
拓扑排序   
最大流最小割 
回路问题：欧拉图、哈密顿图、TSM  
二分图匹配   
### 1.6 哈希表
常用哈希函数：直接地址法、平方取中法、折叠法、取余法  
字符串的哈希函数：字符串->整数，BKDR哈希，AP哈希
冲突解决：开放定址法、链地址法、再哈希法
实践：使用BKDRhash作为基础的哈希函数；使用链地址法作为冲突处理方法，实现哈希表的插入与查找工作   
应用：哈希分片：Round Robin、Virtual Box、一致哈希  
### 1.7 Data Structure in Big Data
bloom filter、bitmap  
skiplist  
LSM树  
一致哈希 Cuckoo哈希  
### 1.8 排序
插入排序  
选择排序  
冒泡排序  
shell排序  
堆排序  
归并排序  
快速排序  
基数排序  
桶排序  
外部排序  
复杂度、稳定性比较
## 2. Algorithm
### 2.1 初等数论
素数与整数唯一分解  
最大公约数与最小公倍数  
高精度加减乘除
进制转换  
### 2.2 组合数学
加法与乘法原理  
Fibonacci数：O(n)、O(logn)  
Catalan数：矩阵连乘的计算次序、合法出栈次序、圆桌握手、二叉排序数总数、凸多边形三角划分  
排列组合  
### 2.3 概率统计
古典概率模型  
抽样原理  
### 2.4 递归与分治
递归  
分治：最大最小值、矩阵乘法、骑士周游问题、大整数乘法、棋盘覆盖问题  
### 2.5 贪心
背包问题  
机器任务调度算法：多机调度问题、活动安排问题  
### 2.6 动态规划
最优子结构  
递推表达式  
空间换时间  
应用：矩阵连乘问题、LCS、LIS、多段图最短路径、资源分配问题
### 2.7 搜索技术
盲目搜索算法：二分搜索、DFS、BFS  
回溯法：八皇后问题及其并行求解  
启发式搜索：A*算法
博弈问题：博弈树  
alpha-beta剪枝