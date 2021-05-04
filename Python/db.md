### mysql接続

基本は

- mysql.connector.connect()からオブジェクトを作る (conn = mysql.connector.connect(db_info))
- 作ったconnectオブジェクトからcursor()を呼び出しオブジェクトを作る (cur = conn.cursor(params))
- sqlを組み立てる
- execute()でsqlの実行(cur.execute(sql)
  - sqlがデータの更新作成削除であればconn.commit()を行う
- 結果をfetchall()で受け取る(cur.fetchall())
- curを閉じる(cur.close())
- connを閉じる(conn.close())

注意点

connector.connect()の引数一覧について  

- https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html

conn.cursor(params)の際に、データを取得する、データをDBに挿入する保存するのどちらかで指定するparamsが異なる。

参考  

- https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor.html
- https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursordict.html
- https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursorprepared.html


【データを取得する】

取得するデータがタプルで返却される  
1. conn.cursor()  

取得データが辞書型で返却される  
2. conn.cursor(dictionary=True)  

取得した後が楽なのでこちらを使う気がする。  

【データを挿入保存する】
1. conn.cursor(prepared=True)

#### sqlの組み立て方

> Specify variables using %s or %(name)s parameter style (that is, using format or pyformat style). execute() returns an iterator if multi is True.

とあるので、%sを使うこと。  
もしくは、cursor(prepared=True)をやっているのであれば、「?」もプレースホルダーとして利用することができる。  

https://dev.classmethod.jp/server-side/python/query-with-mysql-connector-python/

```
import mysql.connector

class db(object):

  # db接続に必要な情報を取得する記述をすること
  # 例。conf.iniの設定、loggerの設定、conf.iniからuser, password, 接続するdb, dbの文字コードなど
  def __init__(self, args):
      self.args = args
  
  # 便宜上、ここでのconnect()のparamsは初期化された際の情報が入力されているようわかりやすく記述する
  def connect(self):
      conn = mysql.connector.connect(
          user = self.args, 
          password = self.args,
          database = self.args
          )
      return conn
  
  # 特定テーブルから全データを取得
  def select_all_info(self, TB_NAME):
      try:
          conn = self.connect()
          cur = conn.cursor(dictionary=True)
          sql = "SELECT * FROM TB_NAME";
          cur.execute(sql)
          result = cur.fetchall()
      except Exception as err;
          # ログに吐き出す処理
          # ここではprintする
          print(err)
      
      # 接続を切る
      finally:
          cur.close()
          conn.close()
          return result

  # 指定テーブルから、条件を絞ってデータを取得する
  def select_part_info(self, params):
      try:
          conn = self.connect()
          cur = conn.cur(dictionary=True)
          sql = "SELECT * FROM "<TB_NAME>" WHERE COLUMN_NAME = %S";
          
          # execute()にparamsを与えるときは、タプルになることに注意
          cur.execute(sql, (params, ))
          result = cur.fetchall()
      except Exception as err;
          # ログに吐き出す処理
          # ここではprintする
          print(err)
      
      # 接続を切る
      finally:
          cur.close()
          conn.close()
          return result
      
  def insert_data(self, param1, param2):
      try:
          conn = self.connect()
          cur = conn.cursor(prepared=True)
          sql = "INSERT INTO <TB_NAME> (COLUMN_NAME1, COLUMN_NAME2) VALUES (?, ?);"
          cur.execute(sql, (param1, param2))
      
          # データの保存更新削除系なのでconn.commit()を行い、確定させる
          conn.commit()
      execept Exception as err:
          print(err)
      finally:
          cur.close()
          conn.close()
```
      
