## Ubuntu + Django2.1.2 +Python3

### 1.1、简单博客系统

#### 1.1 .1 Django 入门

django -网站的开发框架

#### 1.1.2 安装Django(Python3)

打开终端 `$ pip3 install Django == 2.1.2`

<!--more-->

#### 1.1.3 创建项目（project)

“项目”，可以理解为一个网站

首先，创建一个目录mysite（文件夹），将项目创建在这个mysite里

打开终端

$ sudo install python-django-common

$ sudo apt-get install python - django

然后在这个mysite目录下（空白），右键，选择Open in Terminal

`~/mysite$ django-admin startproject mysite` ---创建一个django项目，多了一个mysite子目录，mysite是这个项目名称，这时已经有了一个网站的基本框架了。

创建项目时用到的 django-admin.py，它是Django 的任务管理命令行工具

在有manage.py这个文件的目录下打开终端`$ python manage.py runserver`

若一切正常，可以看到提示信息：

Starting development server at <http://127.0.0.1:8000/> ——启动服务 Quit the server with CONTROL-C. ——control+c 结束当前服务

打开浏览器，输入[http://12.0.1:8000或者http://localhost:8000](http://12.0.xn--1:8000http-xl8ts00z//localhost:8000) ,会看到Django网页

#### 1.1.4 创建应用(application)

网站的具体功能

进入到刚才创建的项目目录中，即manage.py文件所在的目录

`~/mysite$ python manage.py startapp blog` ——在项目mysite中新建了一个blog应用。

对项目结构各个部分简介

##### 1. manage.py

在创建一个Django项目后，manage.py 被自动生成在项目的根目录中，它是对django-admin.py的简单封装，同样能够实现命令行操作，不要修改和删除它。

##### 2. mysite

所建项目的管理功能目录，它里面的文件常用于整个项目进行参数配置

`settings.py` : 包含项目的初始化设置，可以针对整个项目进行有关参数配置，比如配置数据库、添加应用等。

`urls.py`: URL配置表文件，主要将URL映射到应用程序上。当用户请求某个URL时，Django项目会根据这个文件中的映射关系指向某个目标对象（某个应用的urls.py文件或某个具体的视图函数）。这个文件也被称为URLconf.

`wsgi.py` : （Web Server Gateway Interface),是Python所选择的服务器和应用标准。

`__pychache__`: 执行python manage.py runserver命令后出现，时一个编译后的文件夹，里面文件都是以.pyc结尾的文件。

##### 3. blog

项目中创建的应用之一，每创建一个新的应用，Django就会在项目根目录中( ./)中创建一个子目录，目录中会有一些默认的文件。

`admin.py` : 可以自定义Django管理工具。

`apps.py` : 包含对应用的配置

`migrations`: 这是一个目录，用于存储应用的数据库表结构的指令，通过这些指令可以修改和创建数据库，从而在models.py模型类和数据库表之间的迁移。

`models.py` : 应用的数据模型，每个Django应用都应当有一个models.py文件，可以为空。

`tests.py`：在这个文件中编写测试文档来测试所建立的应用。

`views.py`: 用户保存响应各种请求的函数和类。 如果编写的是函数，则称之为基于函数的视图；如果编写的是类，则称之为基于类的视图。保存函数或者类的视图文件。

##### 4. db.sqlite3

默认的数据库SQLite

#### 1.1.5 网站的配置

将应用注册到项目中

在Django项目中，主管信息注册（对本项目进行各种信息声明）的文件时./mysite/settings.py。

**DEBUG**： True or False, 开发过程中，设置成True,在测试功能时，Django能够显示详细的报错信息——“开发模式”。如果将项目部署到真正要对外发布的服务器上——“生产环境”，必须将其值修改为False,从而避免暴露项目的内部信息。

**ALLOWED_HOSTS**: 在DEBUG设置为True时，其值可以为空。当部署到生产环境中时，要把主域名填写到这里，才能通过域名访问到本网站。

**INSTALLED_APPS**： 所有的应用写到这里才能生效。

INSTALLED_APPS = [  'django.contrib.admin', # 针对项目后台管理的应用。  'django.contrib.auth',  'django.contrib.contenttypes',  'django.contrib.sessions',  'django.contrib.messages',
​ 'django.contrib.staticfiles', ​ 'blog', #新增加的，所建立项目的名称，其他项Django默认具有的应用。 ]

**DATABASES**: 配置数据库，默认配置SQLite,小巧灵活，Python标准库所支持。

**LANGUAGE_CODE**:设置项目的语言，汉语，设置为 LANGUAGE_CODE = 'zh-hans'

TIME_ZONE: 设置时区，东八区， TIME_ZONE = 'Asia/Shanghai'

#### 1.1.6 知识点

##### 1. 开发模式

是相对于“生产模式”而言的，即系统尚处于开发阶段，还没正式对外部客户提供服务，在Django开发模式中，不需要配置Apache或者Nginx等服务器，也能够运行网站，这是因为Django本身就提供了简单的Web服务器功能，但是这仅限于开发过程，当网站被正式部署后，即转换为“生产模式”时，就需要对部分配置进行修改。

在开发模式中，Django会自动检测到修改代码并重新加载，不需要每次修改代码后重新启动Web服务器。只有在新增加文件后，才需要重启Django服务。

运行Django服务的指令是： `python manage.py runserver`

##### 2. 项目和应用

Django安装好之后，就有了django-admin这个默认命令，可以用`django-admin starproject projectname`命令创建一个Django项目。

项目是由若干个“应用”(app)组成的，实现具体的功能。创建应用可以用 `python manage.py startapp appname`命令。也可以使用 `django-admin startapp appname`命令。

创建项目和应用后，会生成一些默认的文件，要么是一些默认的配置，要么是一些空文件为了占据位置。

每个应用都要在项目的settings.py文件的INSTALLED_APPS中进行声明，告诉Django这个应用是本项目的一部分。

### 1.2 编写博客的数据模型类

设计数据库和表结构是做网站的基础。在Django中，不需要通过SQL语句直接跟数据库打交道，而是完全用	python的方式创建数据库，之后交给Django完成数据库的操作。

#### 1.2.1 数据模型类

利用Django开发网站系统，一般情况下，要先编写数据模型，就是在./blog/models.py中写一个类，这个类与数据库中的数据表具有对应关系。

在./blog/models.py中编写博客的数据模型类 Blog, 它本质上是一个继承了django.db.models.Models的类。

```
from django.db import models
from django.utils import timezone
from django.contrib.auth.models import User


class BlogArticles(models.Model):
    title = models.CharField(max_length=300)  #1
    author = models.ForeignKey(User,
related_name="blog_posts",on_delete=models.CASCADE,) #2
    body = models.TextField()
    publish = models.DateTimeField(default=timezone.now)
    

    class Meta: #3
        ordering = ("-publish",)

  
    def __str__(self):
        return self.title
```

这个BlogArticles类中定义了一些属性，每个属性对应着将来数据库表中的一个字段。，以后将属性称之为字段。

\#1 字段title的属性为CharFiled()类型，参数说字 段的最大数量.

\#2 通过字段author规定了博客和用户之间的关系——一个用户对应多篇文章。ForeignKey() 就反映了这种“一对多”关系。类User就是BlogArticles的对应对象，related_name="blog_posts"的作用是允许通过类User反向查询到BlogArticles.

\#3 通过 ordering = ("-publish",)，规定了BlogArticles实例对象的显示顺序，即按照publish字段值的倒序显示。

BlogArticles 类的数据模型编写好了，将来数据库表的基本结构就是按照上述各字段及其属性而定的。

**接下来根据数据模型建立数据库表：**

在/mysite/manage.py 位置执行 `~/mysite$ python manage.py makemigrations`,会有Migrations for blog : ...的提示信息，意思就是在blog/migrations目录中创建了一个BlogArticles模型，打开这个001_initial.py文件看一下。

```
# Generated by Django 2.1.2 on 2018-10-13 12:21

from django.conf import settings
from django.db import migrations, models
import django.db.models.deletion
import django.utils.timezone


class Migration(migrations.Migration):

    initial = True

    dependencies = [
        migrations.swappable_dependency(settings.AUTH_USER_MODEL),
    ]

    operations = [
        migrations.CreateModel(
            name='BlogArticles',
            fields=[
                ('id', models.AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                ('title', models.CharField(max_length=300)),
                ('body', models.TextField()),
                ('publish', models.DateTimeField(default=django.utils.timezone.now)),
                ('author', models.ForeignKey(on_delete=django.db.models.deletion.CASCADE, related_name='blog_posts', to=settings.AUTH_USER_MODEL)),
            ],
            options={
                'ordering': ('-publish',),
            },
        ),
    ]
```

这个文件是执行`python manage.py makemigrations`命令后，django自动生成的。这个文件的功能是创建一个名称为BlogArticles的数据库表。这个表的名称由两部分组成，第一部分是blog本应用的名称，第二部分是blogaricles(都小写)是在models.py中创建的数据模型类的名称，中间用单下划线连接。

创建了一个能够建立数据库表的文件，就可以真正创建数据库了。

```
~/mysite$ python manage.py migrate
```

本项目使用SQLite数据库，并且在settings.py中规定了数据库文件存放在项目根目录中

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```

对于db.sqlite3这个文件，可以在FireFox浏览器中安装SQLite Manager 插件来查看。 由于我的火狐浏览器插件不兼容，两种办法：1、直接在Ubuntu Software 搜索 sqlite ,安装DB Browser for SQLite； 2是通过打开终端输入命令：

```
sudo apt-get install sqlite3
sqlite -version
sudo apt-get install sqlitebrowser
```

综上，博客的数据库就建立好了。

#### 1.2.2 发布博客文章

先用最简单的方式实现博客文章的发布,使用Django默认的管理功能就可以发布文章。要使用此功能，必须先创建超级管理员。要牢记所使用的用户名和密码。密码设置要有一定的复杂度，我的是英文字母加数字，至少8位。

```
mysite$ python manage.py createsuperuser
Username(leave blank to use 'qiwsir'): kun
Email address: hk19930914@163.com
Password:*********
Password(again):*********
Superuser created successfull
```

运行服务器 `mysite$ python manage.py runserver`

浏览器地址栏输入 [http://127.0.0.1:8000/admin/或者http://localhost:8000/admin/](http://127.0.0.1:8000/admin/%E6%88%96%E8%80%85http://localhost:8000/admin/), 然后输入刚才创建超级管理员的用户名和密码，就可以进入Django administration页面。 用户(Users)和组(Groups)是Django在用户管理应用中默认的，单击User会看到当前项目仅有的一个用户kun，当然也可以增加用户。

打开./blog/admin.py文件，用编辑工具打开，输入以下代码：

```
from django.contrib import admin
from .models import BlogArticles  #1  将BlogArticles类引入当前环境

admin.site.register(BlogArticles) #2  将该类注册到admin中
```

刷新浏览器页面，看到新注册的BLOG。

单击Blog articless 右侧的Add按钮就可以添加博客文章。内容填写之后，点击保存，该博客文章被保存到数据库中，可以使用DB Browser for SQLite查看数据库。

在./blog/models.py中使用了django.utils.timezone,所以要安装一个pytz模块，用它来提供时区。

```
$ sudo pip3 install pytz
```

安装完毕，重启服务。

在文章列表页，可以看到所有已经发布的文章标题。由于显示的列表信息太单一，为了使列表页的信息更加丰富，继续用编辑./blog/admin.py 文件。

```
from django.contrib import admin
from .models import BlogArticles

class BlogArticlesAdmin(admin.ModelAdmin):
       list_display = ("title",  "author",  "publish")
       list_filter = ("publish",  "author")
       search_fields = ('title',  "body")
       raw_id_fields = ("author",)
       date_hierarchy = "publish"
       ordering = ['publish',  'author']


admin.site.register(BlogArticles, BlogArticlesAdmin)

```

保存，刷新浏览器页面，即可看到效果。

#### 1.2.3 知识点

##### 1. HTTP

Hyper Text Transfer Protocol( 超文本传输协议 )，是客户端( 浏览器、网页爬虫程序 )和服务器端( 网站 )请求和应答的标准(TCP)，封装了Web服务的整个过程，默认端口80。

- 请求 (request): 客户端到服务器端
- 响应 (response): 服务器端到客户端。状态信息（HTTP/1.1 200) 和内容信息。

HTTP/1.1 协议共定义了8种请求方式：OPTIONS、HEAD、GET、POST、 PUT、DELETE、TRACE 和 CONNECT.

本项目中主要使用GET和POST请求

- GET：向指定服务器发出请求，主要用于读取信息并显示
- POST： 向指定服务器提交数据，请求服务器进行处理（例如提交表单或者上传文件）

HTTPS — Hyper Text Transfer Protocol Secure,默认端口443，安全性更高，HTTP以明文方式封装信息，HTTPS以加密方式传送信息。

##### 2. URL

Uniform/Universal Resource Locator 统一资源定位符，俗称网址。

URL标准格式：协议类型://服务器地址(必要时需加上端口号)/路径/文件名

- 协议类型：HTTP/HTTPSu
- 服务器地址： 通常是域名，比如baidu.com,也可以是IP地址，如果默认是80端口，可以不写，否则需要写上端口。
- 路径：以"/"区别目录，对于GET请求方式，可以用“？”发起参数，每个参数以“&”隔开，再以“=”分开参数名称和值。
- 文件名：有必要可写

##### 3. 模型： ORM

动态网站，大多数是通过数据库实现对数据的保存和读取，所以数据库是网站最基本最底层的组成部分。

Django不需要开发者使用SQL语句实现程序和数据库的交互，而是通过ORM，即Object-Relational Mapping（对象关系映射）。

ORM的作用是在关系型数据库和业务实体对象之间进行映射，，只需简单地操作对象的属性和方法。

Django的数据模型层大量使用ORM,表现方式就是编写数据模型类，这些类可以写到任何文件中，通常写在每个应用的models.py文件中，每个数据模型类都是django.db.models.Model的子类。应用的名称（小写字母）和数据模型类的名称（小写字母）共同组成一个数据库表的名称（"appname"_"modelname",例如blog_blogarticles).

当数据模型类写好之后，通过执行Django的数据迁移操作（`python manage.py makemigrations`, `python manage.py migrate`)就能够创建相应的数据库表，用来保存网站项目的数据。以后要更改数据库表的结构，只需要更改数据模型类，迁移数据就能实现数据库结构的调整。

若想改为MySQL数据库,只需要在settings.py文件中做好新数据库的配置，然后进行迁移数据的操作即可完成数据库的迁移，不需要对ORM进行任何修改。
