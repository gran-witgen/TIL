# Django Tutorialで学んだことをメモする

1. 仮想環境を整える

cmd
```cmd
python -m venv 仮想環境名
仮想環境名/Scripts/activate
# できなければ以下
cd 仮想環境名/Scripts
activate
# (仮想環境名)となればOK

# 仮想環境を抜ける
deativate
# (仮想環境名)が消えればOK
```

なぜ仮想環境を整えるのか

プロジェクト毎に違うライブラリバージョンを楽に扱えるようにするため。

2. djangoインストール

```cmd
pip install django
```

3. djangoのプロジェクト、アプリケーション関係


一つのプロジェクトに対し、その機能としてアプリケーションがいくつもぶら下がるイメージ

プロジェクト作成
```cmd
django-admin startproject project_name

# project_nameというフォルダが出来上がるので、移動してmanage.pyを起動する
cd project_name

# 開発用サーバを立ち上げる
python manage.py runserver
```
設定ファイルを変えて、時刻と言語を日本にあわせる

settings.py
```settings.py
LANGUAGE_CODE = "ja"
TIME_ZONE = "Asia/Tokyo"
```

4. データベースの立ち上げ
デフォルトでついてくるsqliteを利用するが  
その他Mysql, Postgresqlを使いたい場合、settings.pyの  
DATABASESというパラメータに設定すること todo

5. アプリケーション作成
cmd
```cmd
python manage.py startapp app_name
# app_nameフォルダが作られる
```

6. djangoの設計思想

M model。扱うデータのこと。データベースのテーブルのようなもの

V view。 どの処理を行うかを決定し、実際にその処理を行う

T template。 viewで渡されたデータをhtmlで表示させる


### webアプリケーションの簡単な流れ

- 1. WebのURLにアクセスする  
- 2. urlsにより、適切なviewが呼び出される  
- 3. viewで処理された値がtemplateに渡される  
- 4. 値を受け取ったtemplateはhtmlを構成し、ユーザーにwebページを表示する  

7. モデルの設定

- 1. Djangoのmodel(model.py)にDBのテーブルデータを定義する

- 2. その後migrationという機能を使い、DBへ変更を反映する

#### migrationについて
事前に定義していたDBのテーブルに、自動生成したSQLを発行しDBへ反映

実際の設定について

models.pyを編集する

models.py
```python
from django.db import models


class TableName(models.Model)"
	
	class Meta:
		# テーブル名の記載
		db_talble = "tablename"
		
	# カラムの定義
	column_name = models.CharField(max_length=XX, unique=True)
```





