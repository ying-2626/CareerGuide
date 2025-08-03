## 编译器版本、依赖安装、项目启动

激活venv环境
```
.\.venv1\Scripts\activate
```
查看python编译器的位数32/64
（目前使用的是64位3.8python）注意python编译器和django、mysqlclient版本兼容
```bash
python -c "import platform; print(platform.architecture())"
```

```bash
#使用清华源安装项目依赖，
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
```
>出现问题：下载mysqlclient显示缺少mysql.h失败
>解决方法：将对应版本和位数的whl文件放到项目目录下（该文件已放置到github仓库上）

启动django项目
```bash
python manage.py runserver
```

## 数据库配置

 `./学生信息管理系统/MxOnline/settings.py` 文件中的 `DATABASES` 配置项里
查找如下内容进行配置：

新建一个数据库（名称和配置中一样，我写的是careerguide）
用户名和密码在新建连接的时候根据自己的设置修改
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',  # 数据库引擎
        'NAME': 'your_db_name',                # 数据库名
        'USER': 'your_db_user',                # 用户名
        'PASSWORD': 'your_db_password',        # 密码
        'HOST': 'localhost',                   # 主机
        'PORT': '3306',                        # 端口
    }
}
```
数据迁移命令如下，运行后就可以在已连接的数据库看到表
```bash
python manage.py makemigrations
python manage.py migrate
```

该项目只有完整的后端代码，前端static静态资源下的css/js缺失，有templates/目录下的html文件，所以打开127.0.0.1:8080前端资源没有正常渲染是正常的

---
## 原项目业务

Django框架实现学生信息管理系统  
[视频链接]!(https://v.qq.com/x/page/l3072o8woc9.html)  

### 注册流程  
  
首先进行输入用户名（邮箱）、密码以及验证码，输入完之后点击注册按钮。如果输入的不正确，提示错误信息。  
  
如果一切信息填写正确无误，调用STMP模块发送激活邮件，用户必须要点击接收到邮箱链接，进行邮件激活后才方可登陆。  
  
即使注册成功，没有激活的用户也不能登陆，用户以get的方式直接重定向到注册页面。  
  
#### 注册登录  
用户能在系统中进行登陆注册和忘记密码进行找回的功能。  
  
#### 个人中心
修改头像，修改密码，修改邮箱，可以看到我的信息。  
  
### 日志记录
  
记录后台人员的操作，方便发现BUG和查看各项调用进行时间。  
  
#### 导航栏
学生信息中有基本信息、年级及成绩信息的模块，能够排序筛选等功能。  
  
#### 多选操作
可以选择多条记录进行删除操作，还可以在课程列表页可以对不同课程进行排序。  
  
#### 数据页码
  
可以设置各项数据在每一页中显示的数量多少，进行翻页功能。  
  
  
### 模块列表页  
  
能够有过滤器功能，在范围内进行查看数据。还能将数据导出为csv，xml，json等数据格式。  
  
[网络毒刘」]!(https://blog.csdn.net/qq_41856814)  
[个人博客」]!(https://www.wakemeupnow.cn)  
