## Django Tips

仮想環境を整えactivateした時、ソースコード用のフォルダを作り  
そこでdjango-admin startproject <project_name>を行うとよい  
また、プロジェクト名の後、「.」をいれることで、作成されるプロジェクトのフォルダ構成が  
よりわかりやすくなる。

```cmd
mkdir src
cd src
django-admin startproject <projectname> .
```


adminサイトの編集の際、テーブルの各カラムを表示させたい場合に、以下のようなコードを書く  

admin.py  
```django
from django.contrib import admin
from .models import Class_name1
from .models import Class_name2


# adminサイトでテーブルの各カラムのデータを見たいため、以下のクラスを追加
class Class_name1_Admin(admin.ModelAdmin):
	
	# list_displayという変数名は変えない
	list_display = (
		"column_name1",
		"column_name2",
		"column_name3"
		)
		
# adminサイト上でテーブルを表示するため、以下を記入
# 同じテーブルのものは必ず、ワンライナーで書くこと
admin.site.register(Class_name1, Class_name1_Admin)
admin.site.register(Class_name2)
```

