django south script
===

south蛋疼的用法一直让人很郁闷，因此使用这个项目中得脚本简化
south的使用。

使用前的步骤
---
1. 将scripts文件夹copy到django项目下，与app同级
2. 读一下代码,将里面`os.environ['DJANGO_SETTINGS_MODULE'] = 'YOUR_PROJECT.settings'`
得`YOUR_PROJECT`改为你settings.py文件夹得名字

脚本`/scripts/south_migrate.py`

此脚本在有数据库表结构更改时使用

执行此脚本时,必须在项目目录下,而不是scripts 下.

使用方法:
---

在你改变表结构前先truncate、init app，然后修改model,
在使用auto参数

###通用做法

1. 在数据库变更前

    python scripts/south_migrate.py truncate paper_edu
    此操作会删掉app里面south相关信息(包括数据库和文件)

2. 在数据库变更前

    python scripts/south_migrate.py init paper_edu
    此操作会--fake旧数据库

3. 数据库变更

    python scripts/south_migrate.py auto paper_edu
    此操作会更改数据库表结构,删除south相关信息(包括数据库和文件)

###针对于git上面别人代码

1.git pull 之前
    python scripts/south_migrate.py init app1,app2,app3

2.git pull 之后
    python scripts/south_migrate.py auto app1,app2,app3
