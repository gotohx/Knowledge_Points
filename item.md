    1. 运算符（operator）
    - 算术运算符（Arithmetic operator、Math and logic operators、）：+、-
    - 比较运算符（Comparison operator）：>、<
    - 赋值运算符（Assignment Operators）：=、+=
    - 位运算符（Bitwise Operators）：&、<<、>>
    - 逻辑运算符（Logical Operator）：and、or、not
    - 成员运算符（member operator）：in、not in
    - 身份运算符（identity operator）：is、is not

2. 装饰器(Decorator):用于拓展原来函数功能的一种函数，目的是在不改变原函数名(或类名)的情况下，给函数增加新的功能。 
```Python
# 打印日志
def log(text):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kw):
            print('%s %s():' % (text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator

# 即now = log('execute')(now)
@log('execute')
def now():
    print('2015-3-25')
```


# mooc
## 会话登录
- request.user.is_authenticated

## 密码加密
- hash 
## web 攻击

  

## python多态怎么实现
- 多态：一种接口多种实现，实现接口的重用
- 在不同类中定义相同的方法
- 鸭子类型
    - Python不检查传入对象的类型
    - 当看到一只鸟走起来像鸭子、游泳起来像鸭子、叫起来也像鸭子，那么这只鸟就可以被称为鸭子。




## python怎么读数据库
- 连接数据库（host,user,paw,database,charset）
- sql 查询语句
- fetchone(),fetchall()　　

- python read/readline/readlines的区别
    - read: 读取整个文件
    - readline: 读取文件的一行
    - readlines:按行读取整个文件内容，将读取到的内容放到一个列表    



## 打乱数组优化
 - 从第一张牌开始，将每张牌和这张牌之前的随机的一张牌进行交换


## 磁盘寻址
- CHS
- LBA

## 随机 id 生成
- 数据库自增
- UUID
    - 当前日期和时间
    - 时钟序列
    - 全局唯一的IEEE机器识别号，如果有网卡，从网卡MAC地址获得，没有网卡以其他方式获得。
- Redis生成ID
    - Redis是单线程的，所以可以用来生成全局唯一的ID
-  Twitter的snowflake算法
    - 0 - 0000000000 0000000000 0000000000 0000000000 0 - 00000 - 00000 - 000000000000
    - 第一位为未使用，符号位一直为0
    - 接下来的41位为毫秒级时间
    - 10bit作为机器的ID（5个bit是数据中心，5个bit的机器ID）
    - 最后12位是毫秒内的计数


## 短网址
- 摘要算法
    - 将长网址 md5 生成 32 个字符签名串,分为 4 段, 每段 8 个字符
    - 对这四段循环处理, 取 8 个字符, 将他看成 16 进制串与 0x3fffffff(30位1) 与操作, 即超过 30 位的忽略处理
    - 这 30 位分成 6 段, 每 5 位的数字作为字母表的索引取得特定字符, 依次进行获得 6 位字符串
    - 总的 md5 串可以获得 4 个 6 位串,取里面的任意一个就可作为这个长 url 的短 url 地址
--------
- 自增序列算法（id 自增）（发号器）
    - 一个 10进制 id 对应一个 62进制的数值
    - 低进制转化为高进制时，字符数会减少
    - 高并发场景：
        - 引入多个机器，设定机器A发号只发向100取余等于0的数字100n，同理机器B只发向100取余等于1数字 100n+1
        - 选择301：短地址生成以后就不会变化，无法统计到短地址被点击的次数
        - 选择302：会增加服务器压力，但是可以统计到短地址被点击的次数
        - 预防攻击：
            - 限制IP的单日请求总数
            - 用一台Redis作为缓存服务器，存储的不是 ID->长网址，而是 长网址->ID，仅存储一天以内的数据，用LRU机制进行淘汰。


## 反爬
- ip限制：限制ip访问频率和次数进行反爬.
- 通过Header反爬虫
    - UA限制：UA是用户访问网站时候的浏览器标识.
    - Referer检测:对 Referer （上级链接）进行检测
- 验证码反爬
- Ajax动态加载
- 字体反爬：通过调用自定义的ttf文件来渲染网页中的文字，而网页中的文字不再是文字，而是相应的字体编码
- 
