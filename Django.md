### 如何定义 url route
### 如何组织 request handler 函数
- 学出一个最简单得 request handler 函数
- 如何从 get/post 请求中取出参数
- 如何定义全局 url 拦截函数
- 如何获取 /修改 /储存 cookie 和 session 的数据
- 如何输出 /修改 http header 数据
### 如何部署 app 程序
- 如何部署服务器
- 如何配置开发环境
- 如何配置静态文件访问
### 如何访问数据库（支持 ORM ）
- 如何维护表结构的变更
- 如何定义 /组织 /初始化数据表
- 如何对接 orm 系统和现有的表结构
- 掌握最基本的 add/delete/按字段查询 /count/slice/order by
- 如何直接使用 sql 访问数据库
### 如何使用模板系统
- 如何组织 /访问 模板文件的目录结构
- 如何在模板中嵌入代码
- 模板是否支持继承结构
- 模板之间如何 include
- 如何自定义模板函数
### 如何通过 http get/post 获取远程数据
### 如何 parse json
### 如何 parse xml
### 如何输出为 json
### 如何处理状态码:404 和 50x
### 如何处理文件上传        

MVT:
model:负责业务对象与数据库的映射    
template：负责如何把页面展示给用户  
view：负责页面逻辑，并在适当的时候调用Model和Template       


Form作用    
- 在前端生成HTML代码
- 对数据做有效性校验
- 返回校验信息并展示    

ModelForm作用：根据模型类生成Form组件， 并且可以操作数据库  

WSGI：规定了服务器怎么把请求信息告诉给应用，应用怎么把执行情况回传给服务器。
uWSGI：实现了WSGI协议的一个web服务器。