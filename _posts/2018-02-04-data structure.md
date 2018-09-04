---
title: 数据结构
categories:
- Algorithms
tags: 
- data structure






---





﻿1. 基础

　　数据结构：是相符之间存在一种或多种特定关系到数据元素的集合。
1.1 逻辑结构： 数据对象中数据元素之间的相互关系

　　1.1.1 集合结构：集合结构的数据元素除同属于一个集合外，它们之间没有其他的关系；

　　1.1.2 线性结构：数据元素之间是一一对应的；

　　 1.1.3 树形结构：数据元素之间存在一种一对多多层次关系；

　　 1.1.4 图形结构：数据元素是多对多多关系；

1.2 物理结构：数据的逻辑结构在计算机中的存储形势

　　 1.2.1 顺序存储结构：把数据元素存放在地址连续的存储单元里，其逻辑关系和物理关系一致（数组）；

　　 1.2.2 链式存储结构：数据元素存放在任意的存储单元里，这组存储单元可以联系也可不连续；

1.3 抽象数据类型

　　数据类型：一组性质相同的值的集合及定义在此集合上的一些操作的总称

　　类型就是用来说明变量或表达式的取值范围和所能进行的操作

　　  抽象：取出事物具有普遍性的本质；
1.3.1 抽象数据类型：指一个数学模型及定义在该模型上的一组操作；
2. 算法

　　　是解决特定问题求解步骤等描述，在计算机中表现为指令等有限序列，并且每条指令表示一个或多个操作；

　　特性：输入输出，

　　　　　有穷性：执行有限步骤之后，自动结束而不会出现无限循环，并且每一个步骤在可接受的时间内完成；

　　　　　确定性：算法的每一步骤具有确定的含义，不会出现二意性；

　　　　　可行性：算法的每一步都必须可行，每一步都能够通过执行有限次数完成；

　　　　　正确性，可读性，      健壮性：对不合法的输入做出相关处理；

　　　　　时间效率高，存储量低；

　　2.7 算法效率的度量方法

　　　　事前分析估算方法：在计算机程序编制前，依据统计方法对算法进行估算；

　　　　函数的渐进增长：给定两个函数f(n)和g(n)，如果存在一个整数N，使得对于n>N，f(n)和总比g(n)大，那么，我们说f(n)的增长渐进快于g(n)

　　2.8 算法时间复杂度

　　　　：语句总的执行次数T(n)是关于问题规模n的函数，进而分析T(n)随n变化的情况并确定T(n)的数量级。算法的时间亮度，记作：T(n)＝O(f(n))。它表示随着问题规模n的增大，算法执行时间的增长率和f(n)的增长率相同，称作算法的渐进时间复杂度，简称时间复杂度。集中f(n)是问题规模n的某个函数。

　　　　O(1)  < O(lgn)  <  O(n) <  O(nlgn)  < O(n2)< O(n3)<O(2n)  < O(n!) < O(nn)

　　2.12 算法的空间复杂度

　　　　S(n)＝O(f(n))：n为问题规模，f(n)为语句关于n所占存储空间的函数；

3. 线性表

　　线性表元素个数定义为线性表长度，n＝0，为空表；

　　线性表的顺序存储结构：用一段地址连续的存储单元依次存储线性表的数据元素（一维数组）

　　3.4.3 数组长度：存储空间的长度；   线性表的长度：线性表中数据元素的个数；

　　存储器中的每个单元都有自己的编号，称为地址；

　　Loc(ai)＝Loc(a1) ＋(i－1)＊c     时间复杂度：存取时间性能O(1) －－－随机存储结构

　　3.5.4 优点：无须为逻辑关系增加额外存储空间，可以快速存取表中任意位置；

　　　　   缺点：插入删除需移动大量元素，线性表长度变化难以确定存储空间，存储空间“碎片”

　　3.6 线性表的链式存储结构

　　一个节点：数据（数据域）＋指针（指针域）

　　单链表：每个结点只包含一个指针域

　　头指针：链表中第一个结点的存储位置；   线性链表的最后一个结点指针为空（NULL）

　　头结点：单链表的第一个结点前设的一个结点；数据域一般无意义（可存储链表长度）

　　头指针不为空；头结点不一定是链表必须要素

　　3.8.1 单链表的插入,将s插入到p后: s->next=p->next, p->next=s(赋值顺序不能调换，否则出错)

　　3.9 单链表整表创建：r->next＝p(将新建p结点放在r后面)，r＝p(p为最后结点赋给r)，p->＝NULL

　　3.11 单链表结构优点：插入删除时间O(1)，不需要预分配；

　　确定：查找O(n)

　　3.12 静态链表：用数组描述的链表；

　　优点：插入删除只需修改游标；

　　缺点：表长依然难以确定，失去顺序存储结构的随机性；

　　3.13 循环链表：将单链表中终端结点的指针端由空指针改为头指针；

　　3.14 双向链表：在单链表的每个节点中，再设置一个指向其前驱结点的指针域；(空间换时间)

　　　　插入时需要保证p->next的赋值在四个操作中最后进行

4 栈 

　　限定仅在表尾进行插入和删除操作的线性表；

　　后进先出，操作在栈顶进行，后进先出（LIFO结构）；

　　进栈，压栈：插入操作

　　出栈：删除操作

　　4.6.1 栈的链式存储结构，链栈；

　　链栈：空间大小可不确定 ；      顺序栈：空间大小确定

　　栈的作用：有效解决递归问题

　　递归：直接调用自己或通过一系列的语句间接调用自己的函数；

　　迭代：循环结构；  递归：选择结构；

　　后缀表达式：逆波兰；

　　中缀表达式：标准四则运算表达式；

　　4.9.3 中缀转后缀：从左到右遍历中缀表达式每个数字和符号，若是数字就输出，即成为后缀表达式的一部分；若是符号，则判断其与栈顶符号的优先级，是右括号或优先级低于栈顶符号则栈顶元素依次出栈并输出，并将当前符号进栈，一直到最终输出后缀表达式为止；

　　4.10 队列：允许在一段进行插入操作，在另一端进行删除操作的线性表；

　　　　first in first out(FIFO)

　　队尾：允许插入；  队头：允许删除；

　　队列顺序存储不足，删除队头，需要移动这个数组O(n);

　　front指向队头元素，rear指向队尾元素；

　　front ＝ rear 空队列

　　循环队列：头尾相接；设置flag，以区别front ＝ rear时为空还是满；

　　4.13 队列等链式存储结构

　　就是线性表的单链表，但只能尾进头出，链队列；

　　空队列：front和rear指向头结点；

5. 串

　　是由零个或多个组成的有限序列，字符串；

　　空格串：只包含空格的串；  空串：零个字符串；

　  模式匹配算法，克努特－莫里斯－普拉斯算法（KMP模式）

　　　　http://blog.csdn.net/joylnwang/article/details/6778316

6. 树

　　n(n≥0)个结点的有限集。n＝0时称为空树。在任意一颗非空树中：有且仅有一个特定的称为根(Root)的结点；当n>1时，其余结点可分为m(m>0)个互不相交的有限集T1,T2...Tn，其中每一个集合本身又是一颗树，并且称为根的子树(SubTree)。  

　　结点拥有的子树的数称为结点的度(Degree)。度为0度结点称为叶结点(Leaf)或终端结点；度不为0的结点称为非终端结点或分支结点，也称为内部结点。树的度是树内各结点的度的最大值。

　　结点子树的根称为该结点的孩子(Child)，该结点称为孩子的双亲(Parent)。同一个双亲的孩子之间互称兄弟(Sibling)。结点的祖先是从根到该结点所经分支上的所有结点。

　　结点的层次从根开始定义，根为第一层，根的孩子为第二层。树中结点的最大层次称为树的深度(Deoth)或高度。

　　如果将树中结点的各子树看成从左至右是有次序的，不能互换的，则称该树为有序树，否则称为无序树。森林是棵互不相交的树的集合。

　　6.5 二叉树(Binary Tree)：n(n≥0)个结点的有限集合，该集合或者为空集，或者由一个根结点和两棵互不相交的，分别为根结点的左子树和右子树的二叉树组成。

　　特点：每个节结点最多两棵子树，即度不大于2，左右子树次序一定；

　　五种基本形态：空二叉树，只有一个根结点，根结点只有左子树，根结点只有右子树，根结点既有左子树又有右子树；

　　6.5.2 斜树：所有结点都只有左子树为左斜树，只有右子树为右斜树，这两种统称斜树；

　　满二叉树：所有分支结点都存在左子树和右子树，并且所有叶子都在同一层上；

　　完全二叉树：一个有n个结点的二叉树按层序编号，如果编号为i的结点与同样深度的满二叉树中编号为i的结点在二叉树中位置完全相同，则这棵二叉树称为完全二叉树；

　　满二叉树一定是完全二叉树，但完全二叉树不一定是满二叉树；

　　完全二叉树特点：叶子结点只能出现在最下两层；最下层的叶子一定集中在左部连续；倒数二层若有叶子结点，一定都在右部连续位置；当结点度为1，则该结点只有左孩子；同样结点树的二叉树，完全二叉树的深度最小；

　　二叉树性质

　　　　1：在二叉树的第i层上至多有2^(i－1)个结点(i≧1)；  

　　　　2：深度为k的二叉树至多有(2^k)－1个结点(k≧1)；

　　　　3：任意一棵二叉树T，如果终端结点数为n0，度为2的结点数为n2，则n0=n2+1；

　　　　4：具有n个结点的完全二叉树深度为「㏒2(n) 」+1（「x」表示不大于x的最大整数）

　　　　5：如果对一棵有n个结点的完全二叉树的结点按层序编号（从第1层到第「㏒2(n) 」+1层），对任意一结点有：　　

　　　　　　如果i＝1，则结点i是二叉树的根，无双亲；i≧1，则其双亲是结点「i／2」；

　　　　　　如果2*>n，则结点i无左孩子(结点i为叶子结点)；否则其左孩子是结点2*i；

　　　　　　如果2\*i>n，则结点i无右孩子；否则其右孩子是结点2\*i＋1；

　　6.7 二叉树的存储结构

　　二叉链表：链表中结点设计一个数据域和两个指针域（表示两个孩子）

　　6.8 二叉树都遍历：

　　　　从根结点出发，按照某种次序依次访问二叉树中所有结点，使得每个节点被访问一次且仅被访问一次；

　　　　前序遍历：若二叉树为空，则空操作返回，否则先访问根结点，然后前序遍历左子树，再前序遍历右子树；

　　　　中序遍历：若树为空，则空操作返回，否则从根结点开始（并不是先访问根结点），中序遍历根结点左子树，然后访问根结点，最后中序遍历右子树；

　　　后序遍历：若树为空，则空操作返回，否则从左到右先叶子后结点到方式遍历访问左右子树，最后访问根结点；

　　　　层序遍历：若树为空，则空操作返回，否则从树第一层，也就是根结点开始访问，从上而下逐层遍历，同一层从左到右顺序访问；

　　6.8.6 二叉树遍历性质

　　　　已知前序遍历序列和中序遍历序列可以唯一确定一棵二叉树；

　　　　已知后序遍历序列和中序遍历序列可以唯一确定一棵二叉树；

　　6.9 二叉树的建立

　　　　扩展二叉树：将二叉树的每个结点的空指针引出一个虚结点，其值为一特定值；

　　6.10 线索二叉树

　　　　指向前驱和后继的指针称为线索，加上线索的二叉链表称为线索链表，相应的二叉树称为线索二叉树；

　　　　线索化：对二叉树以某种次序遍历使其变为线索二叉树的过程；

　　6.12 赫夫曼编码

　　　　带权路径长度WPL最小的二叉树称作赫夫曼树；

7. 图

　　由顶点的有穷非空集合和顶点之间边的集合组成，通常表示为：G(V,E)，其中，G表示一个图，V是图G中顶点的集合，E是图G中边的集合；

　　图中数据元素称为顶点；

　　图结构中不允许没有顶点；

　　任意两点之间都可能有关系，顶点之间的逻辑关系用边来表示，边集可以为空；

7.2.1 各种图定义

　　无向边：顶点V1和Vi之间的边没有方向，则称这条边为无向边（Edge），用无序偶对（Vi Vj）来表示；

　　如果图中任意两个顶点之间的边都是无向边，则称该图为无向图；

　　有向边：若顶点从V1到Vi的边有方向，则称这条边有方向，也称为弧（Arc），用有序偶

<Vi Vj>表示，Vi称为弧尾（Tail），Vj为弧头（Head）；

　　若图中任意两个顶点之间的边都是有向边，则称该图为有向图；如：顶点A到D的有向边，A是弧尾，D是弧头，<A,D>表示弧；

　　简单图：若不存在顶点到其自身的边且同一条边不重复出现；

　　无向完全图：在无向图中任意两个顶点都存在边；含有n个顶点的完全图有n*(n-1)/2条边；

　　有向完全图：有向图中任意两个顶点之间都存在方向互为相反的两天弧，有n*(n-1)条边；

　　有很少条边或弧度图称为稀疏图，反之称为稠密图；

　　图的边或弧相关的树叫做权（Weight），带权的图称为网（Network）；

　　假设图G=(V,{E})，图G'=(V',{E'})，如果V'⊆V且E'⊆E,则称G'为G的子图（Subgraph）；

　　对于无向图G=(V,{E})，如果边(v,v')∈E，则称顶点v和v'互为邻接点，即v和v'相领接边(v,v')依附于顶点v和v'，顶点v的度是和v相关联的边的数目，记为TD(v)；

　　边数就是各顶点度数和道一半：e＝ 0.5* **∑**_TD_(vi)  (i=1,2,3...n)

　　对于有向图G=(V,{E})，以顶点v为头的弧度数目称为v的入度，记为ID(v)，以v为尾的弧的数目称为v的出度，记为OD(v);顶点v的度为TD(v)=ID(v)+OD(v);

　　无向图中从顶点v到顶点v'的路径是一个顶点序列；有向图的路径也是有向的；

　　路径的长度是路径上的边或弧度数目；

　　第一个顶点到最后一个顶点相同的路径称为换或回路，序列中不重复出现的路径称为简单路径；

7.2.3 连通图

　　无向图中，从顶点v到v‘有路径则称为v和v’是连通的；如果对于图中任意两点都是连通的，则称图是连通图；

　　无向图中的极大连通子图称为连通分量；

　　　　连通分量条件：子图／子图连通／连通子图含有极大顶点树／具有极大顶点数的连通子图包含依附于这些顶点的所有边；

　　在有向图G中，如果每一对v，v‘∈V，v≠v’，从v到v‘和从v’到v都存在路径，则称G是强连通图；有向图中的极大强连通子图称作有向图的强连通分量；

　　一个连通图的生成树是一个极小的连通子图，它含有图中全部的n个顶点，但只有足以构成一棵树的n－1条边；

　　如果一个有向图恰有一个顶点的入度为0，其余顶点的入度均为1，则是一棵有向树；

　　一个有向图的生成森林由若干棵有向树组成，含有图中全部顶点，但只有足以构成若干棵不相交的有向树的弧；

7.4 图的存储结构

　　7.4.1 邻接矩阵：一个一维数组存储图中顶点信息，一个二维数组存储图中的边或弧度信息；

　　　　二维数组就是矩阵形式存储，v\[i\]\[j\]表示顶点i到j的边或弧；

　　　　n个顶点和e条边的无向网图创建时间复杂度O(n*n+n+e);

　　7.4.2 邻接表：数组与链表相结合的存储方式

　　　　顶点右一位数组存储，每个数据元素存储指向第一个领接点的指针，每个顶点的所有领接点构成一个线性表；

　　　　有向图的逆邻接表：对每个顶点vi建立一个链接为vi为弧头的表；

　　7.4.3 十字链表

　　　　将邻接表和你邻接表结合起来；

　　　　结点存储数据／入边表头指针／出边表头指针；

　　7.4.4 邻接多重表

　　7.4.5 边集数组

　　　　由两个一维数组构成，一个是存储顶点的信息；另一个存储边的信息，这个边数组每个数据元素由一条边的起点下表，终点下表和权组成；

7.5 图的遍历

　　从图中某一顶点出发遍历图中其余顶点，且每个顶点仅被访问一次，称为图的遍历；

　　深度优先遍历：从某顶点v出发，访问该顶点，然后从v的未被访问邻接点出发深度优先遍历图，直到图中所有和v有路径相同的顶点都被访问；

　　7.5.2 广度优先遍历

　　　　与深度优先遍历时间复杂度相同；（类似树的层序遍历）

7.6 最小生成树

　　构造连通网的最小代价生成树称为最小生成树；

　　7.6.1 普里姆(Prim)算法

　　　　时间复杂度：O(n*n);

　　7.6.2 克鲁斯卡尔(Kruskal)算法

　　　　时间复杂度O(e*log e)

7.7 最短路径

　　迪杰斯特拉算法：时间复杂度O(n*n);

　　弗洛伊德算法：时间复杂度O(n\*n\*n);

7.8 拓扑排序

　　AOV网：在一个表示工程的有向图中，用顶点表示活动，用弧表示活动间的优先关系；

　　拓扑序列：有向图G，满足从顶点vi到vj有一条路径，则在顶点序列中顶点vi必在vj之前；

　　拓扑排序：对一个有向图构造拓扑序列对过程；

　　　　时间复杂度：O(n+e)

　　AOE网：在一个表示工程的带权有向图中，用顶点表示事件，用有向边表示活动，用边上的权值表示活动的持续时间，

7.9 关键路径：

　　从源点到汇点具有最大路径；

8. 查找

　　根据给定某个值，在查找表中确定一个其关键字等于给定值的数据元素(或记录)；

　　查找表：由同一类型的数据元素构成的集合；

　　关键字：数据元素中某个数据项的值，又称键值；

　　主关键字：此关键字可以唯一表示一条记录；

　　数据项对应数据码；

　　查找：根据给定的某个值，在查找表中确定一个其关键字等于给定值的数据元素（或记录）；

　　静态查找表：只做查找操作的查找表；

　　动态查找表：在查找过程中同时插入不存在的数据元素，或者从查找表中删除已经存在的某个数据元素

8.3 顺序表查找

　　顺序查找／线性查找：从表中第一个（或最后一个）记录开始，逐个进行记录的关键字和给定值比较，若相等则查找成功，直到最后一个（或第一个）记录，不等则查找不成功；

顺序查找优化：将给定值赋予a\[0\]，从尾部遍历，循环条件为是否等于关键字，省去判断越界环节；

8.4 有序表查找

　　二分查找／折半查找：在有序表中，取中间记录作为比较对象，若给定值与关键字相等则成功，小于则在左半区查找，大于在右半区查找，直到成功或查找所有区域无记录而查找失败（前提为线性表中记录必须是关键码有序，通常从小到大，且为顺序结构）；

　　　　时间复杂度O(log n)；

　　插值查找：根据要查找的关键字key与查找表中最大最小记录的关键字比较后查找，将二分查找的mid设为mid = low + (key - a\[low\])/(a\[high\] - a\[low\]) * (high - low)

　　斐波那契查找：利用斐波那契函数给mid赋值，mid=low+F\[k-1\]-1；

　　　　时间复杂度O(log n);

8.5 线性索引查找

　　索引就是把一个关键字与它对应的记录相关联的过程；

　　线性索引：将索引项集合组织为线性结构，也称索引表；

　　8.5.1稠密索引

　　　　在线性索引中，将数据集中的每个记录对应一个索引项；

　　　　索引项一定是按照关键码有序排列；

　　8.5.2分块索引

　　　　分块有序，是把数据集的记录分成若干块，并且这些快需要满足，块内无序，块间有序；

　　　　块间有序：要求第二块所有记录关键字均大于第一块中所有记录的关键字；

　　　　最佳分块索引情况为块m＝√￣n（n为记录数），此时平均查找长度L＝（√￣n）＋1；

　　8.5.3倒叙索引

　　　　记录号表存储具有相同次关键字的所有记录的记录号（可以是指向记录的指针或者是该记录的主关键字），由属性值来确定记录的位置；

8.6 二叉排序树

　　二叉查找树／二叉排序树：

　　　　　　　　若它的左子树不空，则左子树上所有结点的值均小于它的根结构的值，

　　　　　　　　若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值，

　　　　　　　　它的左右子树也分别为二叉排序树；

　　二叉排序树查找：利用递归在二叉链表中递归查找；

　　二叉排序树插入操作：利用查找函数将key插入到最终查找到合适结点到子树上；

　　二叉排序树构建：利用插入函数构建（根结点，将之后元素与结点对比，小的在左树中去对比，大的在右树中去对比，直到结点没有孩子，则插入）；

　　二叉排序树删除：找到删除的结点的直接前驱，用该前驱替换删除的结点；

　　二叉排序树以链接的方式存储

8.7 平衡二叉树

　　－－是一种二插排序树，其中每一个节点的左子树和右子树高度差至多等于1；

　　平衡因子：左子树与右子树深度差值；

　　最小不平衡子树：距离插入节点最近的，且平衡因子的绝对值大于1的结点为根的子树；

8.8 多路查找树（B树）

　　每一个结点孩子树可以多于两个，且每一个结点处可以存储多个元素；

　　2-3树：

　　　　每个结点有两个2个孩子（2结点）或3个孩子（3结点）；

　　　　一个2结点包含一个元素和两个孩子（或没有孩子）；

　　　　一个3结点包含一小一大两个元素和3个孩子（或没有孩子）；

　　　　所有叶子在同一层次上；

　　2-3-4树：

　　　　2-3树的扩展，包括4结点；

　　　　一个4结点包括小中大3个元素和4个孩子（或没有孩子）；

　　B树（B－tree）：一种平衡的多路查找树，结点最大的孩子数目称为B树的结；（2-3树是3阶B树）

　　　　如果根结点不是叶结点，则至少有两棵子树；

8.9 散列查找

　　散列技术：在记录的存储位置和它的关键字之间建立一个确定的对应关系f，使得每个关键字k对应一个存储位置；散列函数（哈西函数）

　　K1≠K2，但f（K1）＝f（K2），此时称为冲突，K1和K2称为这个散列函数的同义词；

8.10 散列函数的构造方法

　　直接定值；数字分析法；平方取中；折叠法；除留余数法；

8.11 处理散列冲突

　　开放定值法：一旦发生冲突，就去寻找下一个空的散列地址；

　　再散列函数法：发生冲突，更换散列函数进行计算；

　　链地址法：发生冲突，在当前位置给单链表增加结点；

　　公共溢出法：给发生冲突的关键字重新建立一个溢出表；

8.12 散列表查找

9. 排序

　　似的序列成为一个按关键字有序的序列；

　　排序稳定：Ki＝Kj，且排序前Ri领先于Rj，排序后任然领先；

　　排序不稳定：Ki＝Kj，且排序前Ri领先于Rj，排序后Rj领先Ri；

　　内排序：排序过程待排序所有记录放置在内存中；

　　外排序：整个排序过程需要在内外存之间切换；

　　性能影响：

　　　　1 时间性能：尽可能少的关键字比较次数和尽可能少的纪录移动次数；

　　　　2 辅助空间：存放待排序占用空间加上执行算法所需要其他存储空间；

　　　　3 复杂性： 算法本身复杂度，不止时间；

　　9.3 冒泡：

　　　　时间：O（nˇ2）；

　　9.4 简单排序：

　　　　通过n－i次关键字比较，从n－i＋1个记录中选出关键字最小的值，并和第i个交换；

　　　　时间：O（nˇ2）；

　　　　略优于冒泡（每次只交换一个值）；

　　9.5 直接插入：

　　　　将一个记录插入到已排序的序表中；

　　　　时间：O（nˇ2）；

　　　　略优于冒泡（比较次数少）；

　　9.6 希尔排序：

　　　　基本有序：小的关键字基本在前面，大的基本在后面，不大不小的基本在中间；

　　　　时间：O（nˇ(2/3)）；

　　9.7 堆排序：

　　　　堆：完全二叉树；

　　　　大顶堆：每个结点堆值都大于或等于其左右孩子结点的值；

　　　　小顶堆：每个结点堆值都小于或等于其左右孩子结点的值；

　　　　堆排序（大顶堆）：将待排序序列构造一个大顶堆；最大值此时在根结点，移走根结点，剩余n－1个结点从新构造一个堆，得到次小值，如此反复得到一个有序序列；

