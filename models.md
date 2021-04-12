## functools
### @functools.cache(user_function)
- cache(user_function, /)
    - lru_cache(maxsize=None)(user_function)
        - decorating_function(user_function)
            - _lru_cache_wrapper(user_function, maxsize, typed, _CacheInfo)
            - update_wrapper(wrapper, user_function)




### lru_cache
- maxsize = 0
    - 无缓存，相当于直接调用原函数
- maxsize = None
    - 对参数进行 hash 后得到的值作为 key，原函数返回值为 value
    - 每次调用会先对参数进行 hash，根据 hash 后的值去字典寻找 key 是否存在
- maxsize > 0
    - 

### cached_property
缓存某个属性，如下,第二次调用时不打印‘---’
```Python
>>> from functools import cached_property
>>> 
>>> class Test:
...     @cached_property
...     def test(self):
...         print('---')
...         return 1
... 
>>> f = Test()
>>> f.test
---
1
>>> f.test
1
```

itertools 库
map，filter，zip


## collecctions
### deque
- 可以限定长度，超出长度后另一端会弹出，deque(maxlen=10)
- 队列满后，insert 会报错
- appendleft、extendleft、popleft
- 索引访问在两端的复杂度均为 O(1) 但在中间则会低至 O(n)
```Python
def tail(filename, n=10):
    'Return the last n lines of a file'
    with open(filename) as f:
        return deque(f, n)
```
### defaultdict
- 设置默认的 value 值为 list：defaultdict(list)
- 查询失败时 __missing__() 会调用 default_factory 属性设置默认值，如果 default_factory 为 None，则报错

### namedtuple
- classmethod  somenamedtuple._make(iterable)：从存在的序列或迭代实例创建一个新实例
- somenamedtuple._asdict()：返回一个新的 dict ，它将字段名称映射到它们对应的值
- somenamedtuple._fields：字符串元组，列出字段名