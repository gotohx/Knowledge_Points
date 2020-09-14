- 命令模式
    - 将一个请求封装成一个对象，支持修改日志和撤销操作。
    - 优点： 易于添加新事务以扩展系统。

```Python
import os


class MoveFileCommand(object):
    def __init__(self, src, dest):
        self.src = src
        self.dest = dest

    def execute(self):
        self()
        
    def __call__(self):
        print('renaming {} to {}'.format(self.src, self.dest))
        os.rename(self.src, self.dest)

    def undo(self):
        print('renaming {} to {}'.format(self.dest, self.src))
        os.rename(self.dest, self.src)


if __name__ == "__main__":
    command_stack = []

    # commands are just pushed into the command stack
    command_stack.append(MoveFileCommand('foo.txt', 'bar.txt'))
    command_stack.append(MoveFileCommand('bar.txt', 'baz.txt'))


    # they can be executed later on
    for cmd in command_stack:
        cmd.execute()

    # and can also be undone at will
    for cmd in reversed(command_stack):
        cmd.undo()

```
- 工厂模式
    - 定义一个创建对象的接口, 但由子类决定要实例化的类是哪一个. 工厂方法让类把实例化推迟到子类.
```Python
class A:

    def __init__(self):
        self.word = "运行A"

    def run(self):
        print(self.word)


class B:

    def __init__(self):
        self.word = "运行B"

    def run(self):
        print(self.word)


def Interface(classname):
    """
    工厂模式接口函数
    :param classname:
    :return:
    """
    run = dict(A=A, B=B)
    return run[classname]()


if __name__ == '__main__':
    test1 = Interface('A')
    test1.run()
    test2 = Interface('B')
    test2.run()
    
```

- 单例模式
 - 单例类只能有一个实例。
 - 单例类必须自己创建自己的唯一实例。
 - 单例类必须给所有其他对象提供这一实例。
 - 单例模式保证了在程序的不同位置都可以且仅可以取到同一个对象实例;
    如果实例不存在，会创建一个实例；如果已存在就会返回这个实例。    
```Python
"""
使用装饰器
装饰器里面的外层变量定义一个字典,里面存放这个类的实例.当第一次创建的收,就将这个实例保存到这个字典中.
然后以后每次创建对象的时候,都去这个字典中判断一下,如果已经被实例化,就直接取这个实例对象.如果不存在就保存到字典中.

"""
def singleton(cls):
    # 单下划线的作用是这个变量只能在当前模块里访问,仅仅是一种提示作用
    # 创建一个字典用来保存类的实例对象
    _instance = {}

    def _singleton(*args, **kwargs):
        # 先判断这个类有没有对象
        if cls not in _instance:
            _instance[cls] = cls(*args, **kwargs)  # 创建一个对象,并保存到字典当中
        # 将实例对象返回
        return _instance[cls]

    return _singleton


@singleton
class A(object):
    a = 1

    def __init__(self, x=0):
        self.x = x
        print('这是A的类的初始化方法')


a1 = A(2)
a2 = A(3)
print(id(a1), id(a2))
```


- 装饰器模式:允许向一个现有的对象添加新的功能，同时又不改变其结构
    - 创建一个装饰类，用来包装原有的类，并在保持类方法签名完整性的前提下，提供了额外的功能
    - 何时使用：在不想增加很多子类的情况下扩展类
    - 使用场景： 1、扩展一个类的功能。 2、动态增加功能，动态撤销。  


- 观察者模式：对象间存在一对多关系时，则使用观察者模式
    - 主要解决：一个对象状态改变给其他对象通知的问题
    - 何时使用：一个对象（目标对象）的状态发生改变，所有的依赖对象（观察者对象）都将得到通知，进行广播通知。