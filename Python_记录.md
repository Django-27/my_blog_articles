#### 对比分析
    os.file.dirname(__file__) 
    >> /home/ubuntu/app_1
    返回脚本的路径；不能再命令行执行，否则返回NameError:name '__file__' is not defined；如果运行python /home/ubuntu/app_1/utils.py 返回如上，如果用相对路径运行python utils.py 返回空字符串
    
    os.file.abspath(__file__) 
    >> /home/ubuntu/app_1/utils.py 
    返回.py文件的绝对路径，所以结合起来使用最好
    
    os.path.abspath(os.path.dirname(__file__)
    >> /home/ubuntu/app_1
#### 偏函数 from functools import partial 局部的、部分的
函数调用的时候有多个参数，但其中一个参数已经知道了，可以通过这个参数重新绑定一个新的函数，之后可以去调用这个新的函数;当函数的参数个数太多，需要简化时，使用functools.partial可以创建一个新的函数，这个新函数可以固定住原函数的部分参数，从而在调用时更简单

    def add(a, b):
        return a + b
    add(4, 3)
    >> 7
    add100 = partial(add, 100) # 将原来的add变为add + 100
    add100(9)
    >> 109
扩展的功能，当含有默认参数时

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