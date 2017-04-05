---
title: Python_记录
date:
tags:
---

# 1 对比分析
    os.file.dirname(__file__) 
    >> /home/ubuntu/app_1
    返回脚本的路径；不能再命令行执行，否则返回NameError:name '__file__' is not defined；如果运行python /home/ubuntu/app_1/utils.py 返回如上，如果用相对路径运行python utils.py 返回空字符串
    
    os.file.abspath(__file__) 
    >> /home/ubuntu/app_1/utils.py 
    返回.py文件的绝对路径，所以结合起来使用最好
    
    os.path.abspath(os.path.dirname(__file__)
    >> /home/ubuntu/app_1
# 2 偏函数 from functools import partial 局部的、部分的
函数调用的时候有多个参数，但其中一个参数已经知道了，可以通过这个参数重新绑定一个新的函数，之后可以去调用这个新的函数;当函数的参数个数太多，需要简化时，使用functools.partial可以创建一个新的函数，这个新函数可以固定住原函数的部分参数，从而在调用时更简单
```python
    def add(a, b):
        return a + b
    add(4, 3)
    >> 7
    add100 = partial(add, 100) # 将原来的add变为add + 100
    add100(9)
    >> 109
```
扩展的功能，当含有默认参数时
```python
    def add(a, b, c):
        print a, b, c
        return a + b + c
    plus = partial(add, 1, 2)
    plus(5)
    >> 1 2 5
    >> 8 
    def add(a, b, c=2):
        print a, b, c
    plus = partial(add, 101)
    plus(1)
    >> 101 1 2
    plus = partial(add, 101)(1)
    >> 101 1 2
    plus = partial(add, b=101)(1)
    >> 1 101 2 
``` 

# 3 并发编程
- theading 

- multiprocessing 多进程模块

- multiprocessing.dummy 多线程模块

- 线程模块同步原语，包括锁（Lock），信号量（Semaphore），条件变量（Condition）和事件（EVent）；最好使用Queue模块，它是线程安全的，使用它可以降低程序的复杂度、代码清晰、可读性强。

- 协成Gevent，上下文切换通过yield完成，执行gevent.sleep会触发上下文切换；协成池from Gevent.pool import Pool

- concurrent.futures中包含ThreadPoolExecutor和ProcessPoolExecutor两个执行器，分别用于产生线程池和进程池
- Python2通过生成器（Generator）实现协成，利用yield返回，send或next发送数据；Python对协成的支持大抵如此，一般使用第三方库实现的协成来编写程序。Python3.3中添加yield from，允许生成器把它的部分操作委任给另一个生成器；Python3.4中asyncio被纳入标准库；Python3.5添加async和await两个关键字，协成成为新的语法，不在是一种生成器了。I/O多路复用与协成的引入，极大地提高了高负载下程序的I/O性能。
async用于声明一个协成；await表示一个协成执行完返回，获得协成执行结果，只能在协成内使用。
async简化了asyncio.coroutine，await简化了yield from

# 4 aiohttp替代requests
- 可作为HTTP客户端
- 实现HTTP服务
- 
# 5 zip, izip 和 izip_logest比较
- zip是build-in方法，返回长度为序列中最短的,返回的是<zip object at 0x00008*8>对象
- python2：itertools中的izip，将不同的迭代器元素聚合到一个迭代器中，比zip要快得多
- python2：itertools中的izip_longest，使用最长的迭代器作为返回值的长度，使用fillvalues指定缺失值得默认值
- python3：itertools中只保留了zip_longest,亦可指定默认值；
``` python3
from itertools import zip_longest

class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        newlist, carry = [], 0
        for n, m in list(itertools.zip_longest(l1, l2, fillvalue=0)):
            if n + m + carry < 10:
                newlist.append(n + m + carry)
                carry = 0
            else:
                newlist.append(n + m + carry - 10)
                carry = 1
        return newlist
        
if __name__ == '__main__:'
    s = Solution()
    s.addTwoNumbers([2,4,3], [5,6,4])
```

# 5 按照指定位置旋转字符串,nums, k
```
def rotate(nums, k):
    k = k % len(nums)
    nums = nums[-k:] + nums[:-k]
    return nums

print(rotate('1234567', 4)
>>> 4567123
```
# 6 python 小记
- Queue 和 Stack 在 Python 中都是有 list ,[] 实现的。 在python 中list是一个dynamic array, 可以通过append在list的尾部添加元素， 通过pop()在list的尾部弹出元素实现Stack的FILO， 如果是pop(0)则弹出头部的元素实现Queue的FIFO。
- python 中通过import heapq实现优先队列（Priority Queue),提供push和pop两个最基本的操作和heapify初始化操作。
- 双端队列（deque，全名double-ended queue）可以让你在任何一端添加或者移除元素，因此它是一种具有队列和栈性质的数据结构；Python 的list就可以执行类似于deque的操作， 但是效率会过于慢。 为了提升数据的处理效率， 一些高效的数据结构放在了collections中。 在collections 中提供了deque的类， 如果需要多次对list执行头尾元素的操作， 请使用deque。
- 堆Heap， 一般情况下，堆通常指的是二叉堆，二叉堆是一个近似完全二叉树的数据结构，即披着二叉树羊皮的数组，故使用数组来实现较为便利。子结点的键值或索引总是小于（或者大于）它的父节点，且每个节点的左右子树又是一个二叉堆(大根堆或者小根堆)。根节点最大的堆叫做最大堆或大根堆，根节点最小的堆叫做最小堆或小根堆。常被用作实现优先队列。
- 栈Stack， 栈是一种 LIFO(Last In First Out) 的数据结构，常用方法有添加元素，取栈顶元素，弹出栈顶元素，判断栈是否为空。
- 集合Set， 保存不重复元素的数据结构，是python自带的基本数据结构，有多种初始化方式，s = set()
- 图Graph, 表示通常使用邻接矩阵和邻接表，前者易实现但是对于稀疏矩阵会浪费较多空间，后者使用链表的方式存储信息但是对于图搜索时间复杂度较高。设顶点个数为 V, 那么邻接矩阵可以使用 V × V 的二维数组来表示。 g[i][j]表示顶点i和顶点j的关系，对于无向图可以使用0/1表示是否有连接，对于带权图则需要使用INF来区分。有重边时保存边数或者权值最大/小的边即可。
```
V = 5
g = [[0 for _ in range(V)] for _ in range(V)]
print(g)
>>> [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0]]
```
- 二叉树Binary Tree, 二叉树是每个节点最多有两个子树的树结构，子树有左右之分，二叉树常被用于实现二叉查找树和二叉堆。二叉树的第i层至多有 2^{i-1}个结点；深度为k的二叉树至多有 2^k−1个结点；对任何一棵二叉树T，如果其终端结点数为 n0, 度为2的结点数为 n2 , 则 n0=n2 + 1。一棵深度为 k, 且有 2^k −1 个节点称之为满二叉树；深度为 k，有 n个节点的二叉树，当且仅当其每一个节点都与深度为 k 的满二叉树中序号为 1 至 n的节点对应时，称之为完全二叉树。完全二叉树中重在节点标号对应。
- Binary Search Tree , 二叉查找树,一颗二叉查找树(BST)是一颗二叉树，其中每个节点都含有一个可进行比较的键及相应的值，且每个节点的键都大于等于左子树中的任意节点的键，而小于右子树中的任意节点的键。
使用中序遍历可得到有序数组，这是二叉查找树的又一个重要特征。
- Map 哈希表， 是一种关联数组的数据结构，常被称为字典或键值对。在 Python 中 dict(Map) 是一种基本的数据结构。

# 7 python 小记
- python中有三种方法，实例方法、类方法（@classmethod）、静态方法（@staticmethod）
- 类方法的第一个参数时cls，表示该类的一个实例，静态方法与普遍的方法一样
- self和cls的区别不是强制的，只是PEP8中一种编程风格，slef通常用作实例方法的第一参数，cls通常用作类方法的第一参数。即通常用self来传递当前类对象的实例，cls传递当前类对象。
```
class A(object):
    def foo(self, x):
        print("executing foo(%s,%s)" % (self, x))
        print('self:', self)
    @classmethod
    def class_foo(cls, x):
        print("executing class_foo(%s,%s)" % (cls, x))
        print('cls:', cls)
    @staticmethod
    def static_foo(x):
        print("executing static_foo(%s)" % x)    
a = A()

print(a.foo)           >>> <bound method A.foo of <__main__.A object at 0x0000000004F6B908>>
print(a.class_foo)     >>> <bound method A.class_foo of <class '__main__.A'>>
print(a.static_foo)    >>> <function A.static_foo at 0x0000000004F05488>
```
#### foo方法绑定对象A的实例，class_foo方法绑定对象A，static_foo没有参数绑定。

\ | 实例方法 | 类方法 | 静态方法
---|--- | --- | ---
a = A() | a.foo(x) | a.class_foo(x) | a.static_foo(x)
A  | 不可用 | A.class_foo(x) | A.static_foo(x)

#### 实例是三种方法都可以调用的，而类只可以调用两种;
- 类方法（classmethod）必须要用类对象作为第一个参数，静态方法（staticmethod）可以没有参数
- [详细介绍1](http://stackoverflow.com/questions/12179271/meaning-of-classmethod-and-staticmethod-for-beginner),[详细介绍2](http://blog.csdn.net/a447685024/article/details/52424481)
- 类方法的第一个参数cls，而实例方法的第一个参数是self，表示该类的一个实例;类方法有类变量cls传入，从而可以用cls做一些相关的处理。并且有子类继承时，调用该类方法时，传入的类变量cls是子类，而非父类。 

# 8 闭包
- 可以实现将参数传递给函数，但不立即求值，达到延迟求值的目的。
- 闭包满足三个条件：必须有一个内嵌的函数；内嵌的函数必须引用外部函数中的变量；外部函数返回值必须是内嵌函数。
- 类中定义函方法 PyCharm 提示Method xxx may be ‘static’, 原因是该方法不涉及对该类属性的操作，编译器建议声明为@staticmethod，面向对象思想体现。
```
def dalay_func(x, y):
    def caculator():
        return x + y
    return caculator

msum =dalay_func(3, 4)
print(msum())            >>> 7
```
# 9 *args 和 **kwargs
- 为python中的可变参数，*args表示任意多个无名参数，是一个元祖
- **kwargs表示关键字参数，是一个字典；同时使用时必须*args在前，**kwargs在后

# 10 @property @x.setter @x.deleter
- 通过@property装饰器，将类方法转换为类属性（只读），可通过正常的点符号访问，但不能赋值（AtributeError）
- 可以有@x.setter, @x.getter, @x.deleter
```
class C(object):
    def __init__(self): self._x = None

    @property
    def x(self):
        """I'm the 'x' property."""
        return self._x

    @x.setter
    def x(self, value):
        self._x = value

    @x.deleter
    def x(self):
        del self._x
```
# 10 python 快速排序
```

def qsort(seq):
    if len(seq) <= 1:
        return seq
    else:
        pivot = seq[0]
        lesser = qsort([x for x in seq[1:] if x < pivot])
        greater = qsort([x for x in seq[1:] if x >= pivot])
        return lesser + [pivot] + greater

print(qsort([1, 3, 4, 5, 0, -3, -9, 22])  >>> [-9, -3, 0, 1, 3, 4, 5, 22]
```
