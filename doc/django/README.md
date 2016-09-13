# Django 入门 - 学习笔记

## 1. 简介
>  Django框架负责处理大部分Web开发的底层细节，我们可以专注开发web应用；

- 快速开发：Python语言、数据库ORM系统；
- 大量内置应用：后台管理 admin、用户认证 auth、会话系统sessions；
- 安全性高：表单验证、SQL注入、跨站攻击；
- 易于扩展；

## 2. 开发环境
- `python`
- `ipython`
- `danjo`

## 3. 创建工程
### 3.1 工程基本结构
- `manage.py`
- `mysite`
	- `__init__.py`
	- `settings.py`
	- `urls.py`
	- `wsgi.py`
- `db.sqllite3`

### 3.2 manage.py
`manage.py`是Django的一个用于管理任务的命令行工具。
```
# 启动服务
python manage.py runserver 0.0.0.0:8080
```

### 3.3 settings.py
Django 的设置，配置文件，比如 DEBUG 的开关，静态文件的位置等。
- `ALLOWED_HOSTS` ：允许访问的IP域；
- `INSTALLED_APPS`：已经安装的应用；
- `MIDDLEWARE`： django的中间件；
- `ROOT_URLCONF`：根目录；
- `TEMPLATES`：模板引擎；
- `DATABASES`：数据库；

### 3.4 urls.py
网址入口，关联到对应的views.py中的一个函数（或者generic类），访问网址就对应一个函数。
``` python
urlpatterns = [
    url(r'^admin/', admin.site.urls),
]
```
### 3.5 wsgi.py
 `wsgi(Python Web Server Gateway Interface)`服务器网关接口，是Python语言定义的web服务器和web服务程序或者框架之间的一种简单而通用的接口。

## 4. 开发应用

### 4.1 创建应用
调用`manage.py`创建应用，会自动创建app目录：
``` python
python manage.py startapp blog # blog 是一个app的名称
```

应用目录：
- `views.py`
- `models.py`

### 4.2 添加应用
在`settings.py`中的`INSTALLED_APPS`配置项中加入新增的应用；
``` python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog' # 自定义的应用
]
```

### 4.4 定义视图访问函数
`views.py`文件定义了视图，需要在其中定义视图访函数，并在`urls.py`文件中定义其对用的映射URL。
``` python
from django.http import HttpResponse
def hello(request):
    return HttpResponse('<html>hello world</html>')
```

### 4.5 定义视图函数URL
先使用`form...import`语句导入函数，再使用`url()`定义访问的URL，第一个参数为匹配URL的正则表达式，第二个参数为对应的访问函数。
``` python
from django.conf.urls import include, url
from django.contrib import admin
from blog.views import hello
urlpatterns = [
    url(r'^admin/', include(admin.site.urls)),
    url(r'hello', hello)
]
```