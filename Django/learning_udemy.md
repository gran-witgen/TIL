復習

### アプリの作成

```cmd
python manage.py startapp <app_name>
```

settings.pyのinstalled_appsに<app_name>を追加

### modelの作成

<app_name>/models.py
```python
from django.db import models

# 対象となるデータのclassを作成
class TargetModel(models.Model):

    class Meta:
        db_table = <table_name>
        # 管理サイト上で見やすくするための記述
        verbose_name = "App_name or column name"
        verbose_name_plural = "App_name or column name"
  
  # 対象となるフィールドを指定。ここでいうフィールドとは、DBの1カラムに相当する。
  # ここでは、短めの文章を入力できるカラムを指定する。他のフィールドについてはドキュメント参照
  title = models.CharField(max_length=10)
  
  # 管理サイト上でデータを表示するために以下の記述を行う
  # インスタンスが作られた際の挙動を指定している
  def __str__(self):
    return self.title
```

### urlsの編集、追加
アプリフォルダには存在しないため改めて作る

root_project/urls.py
```python
from django.contrib import admin
from django.urls import path
from django.urls import include

urlspatterns = [
  path("admin", admin.site.urls),
  
  # appのurls.pyを呼び出す
  path("", include("app_name.urls")),
  ]
```

app_name/urls.py
```python
from django.urls import path
from .views mport List
from .views mport Detail

urlpatterns = [
    #  show list
    path("list", <app_name>List.as_view()),
    
    # show detail
    # 詳細画面を表示させるには、<int: pk>を付けること
    path("detail/<int:pk>", <app_name>Detail.as_view()),
```

### <app_name>view.pyについて

```python
from django.shortcuts import render
from django.views.generic import ListView
from django.views.generic import DetailView
from .models import <target_model>


class <App_name>List(ListView):
    # 利用するテンプレートhtmlを指定する
    template_name = "<app_name>/list.html
    # 利用するモデルを記述
    model = target_model
    
class <App_name>List(DetailView):
    # 利用するテンプレートhtmlを指定する
    template_name = "<app_name>/detail.html
    # 利用するモデルを記述
    model = target_model
```

### 管理サイト上で、作成したアプリデータを登録する

<app_name>/admin.py
```python

from django.contrib import admin
from .models import target_model

admin.site.register(target_model)
```

### テンプレートについて

settings.pyに設定しない場合、各appフォルダ配下にtemplatesというフォルダを作り、さらにappフォルダを作成し、htmlファイルを格納する。

格納ファイルの例

- list.html
- create.html
- detail.html

などなど。

base.html

- templatesの機能説明
- app_name/urls.pyのurl逆引きのname


各種templatesの格納場所  

- app_name/templates/app_name/

base.html  
他のテンプレートファイルのデザインのもとになるもの。

その際、Jinja2というテンプレート機能を使う。

Jinja2の文法
- {%  %}  
%と%の間に、pythonのプログラムのようなものを書くことができる  

example

```
{% for item in object_list %}
    何かの処理
{% endfor %}
```

### 注意
forやほかのキーワードを使った場合、最後にend××と閉じる必要がある。タグみたいなものだな。  
※ ただしextendsは例外  

- {{ }}  
実際のデータを表示させる

example

```
{% for item in object_list %}
    {{ item.property }}
{% endfor %}
```

item.propertyが表示される。

- {% extends "html_name" %}   

主にhtml_fileにはbase.htmlがはいる。  
base.htmlを継承することを示す。  



