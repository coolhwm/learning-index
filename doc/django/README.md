# Django 入门 - 学习笔记

## 1. 简介
>  Django框架负责处理大部分Web开发的底层细节，我们可以专注开发web应用；

- 快速开发：Python语言、数据库ORM系统；
- 大量内置应用：后台管理 admin、用户认证 auth、会话系统sessions；
- 安全性高：表单验证、SQL注入、跨站攻击；
- 易于扩展；

## 2. 开发环境

安装开发环境：
- `python`
- `ipython`
- `djanjo`

环境变量配置：
- 将`PYTHON_HOME\Scripts`目录加入`PATH`环境变量；

## 3. 创建工程
### 3.1 工程基本结构
通过命令创建工程：

``` python
django-admin startproject mysite
```

工程结构：
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
- 使用该命令会启动的一个开发服务器，它使用纯`python`进行编写，可以快速进行开发。不要在开发环境使用该服务。
- `runserver`服务器具备热部署的功能，但是如新增字段等某些操作还是需要重启服务器；

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

### 3.6 \__init__.py
标识这是一个`python`的包；

## 4. 构建应用

### 4.1 创建应用
调用`manage.py`创建应用，会自动创建app目录：
``` python
python manage.py startapp blog # blog 是一个app的名称
```
- 在`django`中，`project`是用多个`app`组成的；
- 可以使用`manage.py`的自动化构建工具自动生成`app`的结构；

应用目录：
- `views.py` - 定义视图访问函数；
- `models.py` - 定义数据表；
- `migrations` - 和数据库相关；
- `test.py` - 测试；
- `admin.py` - 给django自带的admin应用使用，管理数据库后台；


### 4.2 添加应用
#### 4.2.1 添加自定义应用
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
也可以使用`apps.py`引入：
``` python
INSTALLED_APPS = [
	# .....
    'polls.apps.PollsConfig',
]
```

#### 4.2.2 默认应用
默认引入一些便利、通过的app，这些应用有可能对数据库有所依赖，如果不需要这些模块，可以将其删除：
- `django.contrib.admin` – 后台管理模块；
- `django.contrib.auth` – 权限控制模块；
- `django.contrib.contenttypes` – 一个用于引入文档类型的框架；
- `django.contrib.sessions` – 会话框架；
- `django.contrib.messages` –消息框架；
- `django.contrib.staticfiles` – 静态文件管理框架；

使用`migrate`指令可以创建app依赖的数据库表；
```
python manage.py migrate
```

### 4.4 定义视图访问函数

#### 4.4.1 访问函数
`views.py`文件定义了视图，需要在其中定义视图访函数，并在`urls.py`文件中定义其对用的映射URL。
- 视图访问函数需要返回一个`HttpResponse`对象或引发抛出异常，例如`Http404`；
- `HttpResponse`可以使用已渲染的视图及`request`进行构造；
- 使用`loader.get_template('blog_list.html')`可以获取视图模板；
- 使用`template.render(context)`可以对模板进行渲染；
- 可以使用`request.POST`和`request.GET`获取表单提交的参数；

``` python
def vote(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    try:
        selected_choice = question.choice_set.get(pk=request.POST['choice'])
    except(KeyError, Choice.DoesNotExist):
        return render(request, 'polls/detail.html', {
            'question': question,
            'error_message': 'You did not select a choice'
        })
    else:
        selected_choice.votes += 1
        selected_choice.save()
        return HttpResponseRedirect(reverse('polls:results', args=question_id))
```

#### 4.4.2 快捷定义
- 可以使用`render(request, template_name, context)`可以快捷构造一个`HttpResponse`；

```python
from django.shortcuts import render

def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)
```

#### 4.4.3 抛出异常
当对象找不到时可以使用`try except`捕获异常，并使用`raise Http404`抛出404错误：
```python
def detail(request, question_id):
    try:
        question = Question.objects.get(pk=question_id)
    except Question.DoesNotExist:
        raise Http404("Question does not exists")
    return render(request, 'polls/detail.html', {'question': question})
```
可以使用`get_object_or_404()`简化这个过程；


#### 4.4.4 重定向
可以使用`HttpResponseRedirect`进行重定向，重定向需要传入一个`URL`，需要使用`reverse`函数将模板名称和参数转换成URL进行访问：
``` python
def vote(request, question_id):
	# ...... 
	return HttpResponseRedirect(reverse('polls:results', args=question_id))
```

#### 4.4.5 抽象视图
利用抽象视图，可以专注于特殊数据提取的逻辑与返回模板的名称，而不关心结果怎么放到视图中、视图渲染的过程、通用的数据提取逻辑，可以进一步简化视图访问函数的代码。
``` python
# 列表抽象视图
class IndexView(generic.ListView):
	# 视图模板
    template_name = 'polls/index.html'
    # 结果保存在context里的名称
    context_object_name = 'latest_question_list'

	# 获取数据集合的方法
    def get_queryset(self):
        return Question.objects.order_by('-pub_date')[:5]

#详情抽象视图
class DetailView(generic.DetailView):
	# 模型类
    model = Question
    # 视图模板
    template_name = 'polls/detail.html'

```
抽象视图对URL的配置也有一定的要求：
- 视图使用`views.类名.as_view()`；
- 参数名称有约定，如主键使用`pk`；

``` python
urlpatterns = [
    url(r'^$', views.IndexView.as_view(), name='index'),
    url(r'^(?P<pk>[0-9]+)$', views.DetailView.as_view(), name="detail"),
    url(r'^(?P<pk>[0-9]+)/results/$', views.ResultView.as_view() , name="results"),
    url(r'^(?P<question_id>[0-9]+)/vote/$', views.vote, name="vote"),
]
```

### 4.5 定义视图函数URL
#### 4.5.1 直接定义
先使用`form...import`语句导入函数，再使用`url()`定义访问的URL，第一个参数为匹配URL的正则表达式，第二个参数为对应的访问函数。
``` python
from django.conf.urls import include, url
from django.contrib import admin
from blog.views import hello
urlpatterns = [
    url(r'^admin/', include(admin.site.urls)),
    url(r'^$', show_list),
    url(r'^blog/(\d+)$', show_blog),
]
```

#### 4.5.2  配置模块的urls.py
也可以在`app/urls.py`目录下定义局部的`urls.py`：
``` python
from django.conf.urls import url
from . import views
urlpatterns = [
    url(r'^$', views.index, name='index'),
]
```
在全局的`urls.py`中进行引用，并为模块设定统一的前缀：
- 当遇到`include`函数时，`django`总是会截断已匹配的部分，然后将剩余部分传递到下一个`URLconf`中；
- 当引用另外一个`URL patterns`时，总是需要使用`include()`函数；

``` python
from django.conf.urls import include, url
from django.contrib import admin

urlpatterns = [
    url(r'^polls/', include('polls.urls')),
    url(r'^admin/', admin.site.urls),
]
```

#### 4.5.3 url()函数
函数参数：
- `regex` - 匹配URL的正则表达式
	- 不限定根域名及`GET`/`POST`请求的参数；
	- 具备较强的匹配性能；
	- 被正则表达式捕获的分组，会按照顺序依次作为参数传入；
	- 如果使用命名分组`(?P<param_name>)`，那么将会作为关键词参数传入；
- `view` - 视图处理函数
	- 传入视图处理函数的第一个参数固定为`HttpRequest`；
- `kwargs` - 关键词参数
	- 可以传递任意的关键词参数到视图中；
- `name` - 命名URL
	- 可以避免混淆发生，可以使用`url`命令访问指定的url‘；

``` python
urlpatterns = [
	# ex: /polls/
    url(r'^$', views.index, name='index'),
    # ex: /polls/5/
    url(r'^(?P<question_id>[0-9]+)$', views.detail, name="detail"),
    # ex: /polls/5/results/
    url(r'^(?P<question_id>[0-9]+)/results/$', views.results, name="results"),
    # ex: /polls/5/vote/
    url(r'^(?P<question_id>[0-9]+)/vote/$', views.vote, name="vote"),
]
```

#### 4.5.4  URL的命名空间
可以在`urlpattern`前定义`app_name`变量，指定其命名空间：
``` python
app_name = "polls"

urlpatterns = [
]
```

#### 4.5.5 访问命名URL
可以在模板中使用`url`命令访问命名的URL，而不是依赖于特定的URL字符串：
``` html
<a href="{% url 'detail' question.id %}">{{ question.question_text }}</a>
```
或使用命名空间前缀进行访问：
```
<a href="{% url 'polls:detail' question.id %}">{{ question.question_text }}</a>
```


### 4.6 数据模型
#### 4.6.1 基本概念
- `Django`的模型基于DRY原则，即仅在一个地方定义数据模型，并自动生成数据库结构；
- 使用`migrations`可以自动维护数据库结构，使其满足当前的模型；

#### 4.6.2 构建模型
- 每个`Django`的模型都是`django.db.models.Model`的子类；
- 每个模型都会定义一些类变量，代表其映射的数据库字段；
- 字段名称即为`python`的字段名、也是数据的列名；
- 常用字段类型：
	- `DateTimeField`
	- `CharField`
	- `IntegerField`


Django 模型是与数据库相关的，与数据库相关的代码一般写在 `models.py` 中：
``` python
class Blog(models.Model):
    title = models.CharField(max_length=50)
    content = models.TextField()
    counter = models.IntegerField()
    pubDate = models.DateField(auto_now_add=True)
    author = models.ForeignKey(Author)

    def __unicode__(self):
        return self.title
```
#### 4.6.3 生成数据库表
需要使用命令同步数据库，生成数据库表：
``` python
python manage.py makemigrations
python manage.py migrate
```
- `makemigrations`命令告诉`Django`模型发生改变；
- `migrate`命令应用变更，执行数据库变更的脚本；
- 生成库表的名称为`模块名_小写类名`；
- 主键会自动生成，命名为`id`，在`MySql`会配置为自增字段；
- 外键的命名为`对端对象名_id`；
- `Django`通过特殊的库表`django_migrations`判断哪些变更已经执行过了、哪些没执行过；

#### 4.6.4  数据访问API
- `get()`
- `filter()`
- `exclude()`

字段查询使用双下划线作为条件限定和对象导航：`field__lookuptype=value`；
- `lte`,`gte`,`gt`,`lt`：比较符；
-  `iexact`,`exact`：严格匹配，如大小写；
-  `contains`：包含；
-  `startswith`,`endswith`：开头、结尾匹配；

``` python
# 获取全部对象
from polls.models import Question, Choice
# 根据字段获取对象
Question.objects.filter(id=1)
# 模糊查询
Question.objects.filter(question_text__contains='up')
# 创建关联对象
q.choice_set.create(choice_text='The sky', votes=0)
# 获取关联对象
q.choice_set.all()
```


### 4.7 视图模板
#### 4.7.1 视图模板配置
- `TEMPLATES`：配置节点描述了Django的模板配置信息；
- `APP_DIRS`：为`Ture`是会查找每个安装应用`INSTALLED_APP`子文件夹内部的`templates`文件夹；
- 需要在`APP`的子目录下简历`templates`文件夹，并再建立子文件夹作为模板的命名空间，避免重复；
- 模板通常的路径格式：`polls/templates/polls/index.html`；

Django 的模板系统会自动找到app下面的templates文件夹中的模板文件：
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>博客列表</title>
</head>
<body>
    {% for blog in blogs %}
    <p>{{ blog.title }}</p>
    {% endfor %}
</body>
</html>
```
模板支持一些基本表达式语法：
```
<!-- 输出变量 -->
{{ string }}
{{ info_dict.content }}

<!-- 迭代输出 -->
{% for i in TutorialList %}
{{ i }}
{% endfor %}

<!-- 判断分支 -->
{% if var >= 90 %}
成绩优秀，自强学堂你没少去吧！学得不错
{% elif var >= 60 %}
需要努力
{% else %}
不及格啊，大哥！多去自强学堂学习啊！
{% endif %}
```

### 4.8 后台管理
需要先为管理后台创建一个用户：
``` python
python manage.py createsuperuser
```

修改模块的`admin.py`文件，注册模型，登录`http://localhost:8000/admin/ `即可进入管理页面：
``` python
from django.contrib import admin
from .models import Blog, Author

# Register your models here.
admin.site.register(Blog)
admin.site.register(Author)
```
推荐定义 Model 的时候 写一个 `__unicode__` 函数(或 `__str__`函数)，以便支持更友好的展示效果
``` python
def __unicode__(self):
    return self.title
```



## 5. 连接MySQL数据库
### 5.1 配置DATABASE
``` python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'blog_system',
        'USER': 'root',
        'PASSWORD': 'root',
        'HOST': '192.168.125.134',
        'PORT': '3306',
    }
}
```

### 5.2 安装MySQL驱动
- 下载并安装：[Microsoft Visual C++ 9.0 is required](http://www.microsoft.com/en-us/download/confirmation.aspx?id=44266)
- 下载并安装：[mysql-connector-python](https://dev.mysql.com/downloads/connector/python/)
- 检查安装：
``` python
pip install MySQL-python
# Requirement already satisfied (use --upgrade to upgrade): MySQL-python in d:\python27\lib\site-packages
```
- 运行迁移命令，创建数据库表：
```
python manage.py migrate
```




