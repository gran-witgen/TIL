- having句

```
select 
  * 
from 
  XX 
where 
  XXX 
group by XXXX asc
having XXXXX;
```

- count関数
```
# テーブル行を数える
select count(*) from XX;

# 指定した列で重複を省く
select count(distinct XXX) from XX;
```

- order by 
```
select * from XX order by XXX;

# 重複した場合、XXX以下に列名を書くことで、列に従い重複レコードをソートする
select * from XX order by XXX desc, XXXX asc;
```

- nullについて  

データが存在しないことを示す。  
空白や0とは異なる。  
設計する際は、nullが出ないような工夫が必要。  
nullを含んだ計算はnullが返る。  
avg()などの関数では、nullがあるレコードは対象外となる。

- round()

四捨五入を行う。 

```
# 小数点第一位で四捨五入を行う
round(float, 0)

# 小数点第二位で四捨五入を行う
round(float, 1)

# 小数点第三位で四捨五入を行う
round(float, 2)
```

- 文字列の演算について

「|」を利用する。  
string_a || string_b;  

# concat()でもできる

concat(string_a, string_b);

- 日付の計算

代表的な関数

# 今日の日付を取得  
- current_date()  

# 今のタイムスタンプを取得  
- current_timestamp()  

# 前後の日付を取得  
- 「internal n day」  
- 「internal - n day」  

```
select current_date();
# 2019-09-01

# 5日後を表示
select current_date() + interval 5 day;
# 2019-09-06

# 5日前を表示
select current_date() - interval 5 day;
# 2019-08-27
```

- n時間前後を表示する  
- 「interval "n hour";」  
- 「- interval "n hour";」

```
select current_timestamp();
# 2019-09-01 22:05:59

select current_timestamp() + interval 5 hour;
# 2019-09-02 03:06:35

select current_timestamp() - interval 5 hour;
# 2019-09-01 17:07:02
```

- extract()

特定の年、日付を取得する 

```
select * from XXX where extract(date_string from date_field) = XXXX;
```

### テーブルの内部結合

- inner join

結合することで、正規化する前のテーブルを表示する。  
正規化とは、データの重複がないようにテーブルを分けること。  

```
select 
 table_name1.field, # inner joinでテーブルを結合した際、どちらのテーブルのfieldかわからないため、table_name.fieldと明確化すること。
 table_name2.field 
from table_name1 
 inner join table_name2 # テーブルの結合
on table_name1.field = table_name2.field; # 結合したテーブルでの検索条件 
```

- 内部結合したテーブルで、さらに条件を絞る  

inner joinした後にwhere句でさらに条件を絞ることができる。  
whereでfromで選択したテーブルの情報のデータを絞る。

```
select 
 table_name1.field,
 table_name2.field 
from table_name1 
 inner join table_name2 # テーブルの結合
on table_name1.field = table_name2.field
where table_name1.field = XXX;
```

- 外部結合

(left) outer join  

内部結合との違い。  
指定したテーブルに欠損情報があったとしても、結合してテーブルを表示する。  
一方、内部結合は欠損データがあった場合、それは結合対象のデータとして扱わない。  

構文  

```
select 
 table_name1.field, 
 table_name2.field 
from 
 table_name1 
left outer join　# from句で取得するテーブルをマスタとする
 table_name2
on table_name1.field = table_name2.field
```

- テーブルの足し算  

union, union allを利用する。  

union前のselectで取得したレコードに、union以下で取得したレコードを足している。  

【注意点】  
unionして足し算をする際、くっつけるテーブルのカラムとカラムのデータ型はそろえる必要がある。   

```
select column1, column2 from table_name1 union (union all) select column1, column2 from table_name2;
```

unionとunion allの違いについて  
union allはどちらのテーブルにも存在するレコード(重複レコード)も出力するが、unionは重複レコードを削除して結果を出力する。

またorder by column_nameは全体で一つしか扱えない。

- create view  

select文で取得した結果を一時的に保存して扱うことができる。  

```
create view view_name(view_column_name1, view_column_name2) as select ,,,
```

select文以下で取得したデータをview_nameというviewにして保存することができる。

- サブクエリ  

サブクエリとは、ある問い合わせの結果に基づいて、異なる問い合わせを行う  


```
select
 column_name,
from
 table_name1
where
 column_name 演算子 (select column_name from table_name2,,,);
 ```
 
 - スカラサブクエリ  
 
 単一の行しか返さないクエリのこと。  
 例えば、価格の平均値など。


- case  

caseをつかうことで条件分岐が可能  

```
case
 when condition_express then X
 when condition_express then Y
 else Z
end
``` 

example  

```
select
 filed_column,
 case
  when 条件式 then 'A'
  when 条件式 then 'B'
  else 'C'
 end as rank
from
 table_name;
```

- データの挿入  

- insert  

```
insert into table_name(column_name1, column_name2) values(value1, value2);
```

- データの更新  

- update

```
update table_name set column_name = 値;
update table_name set column_name = 値 <条件式>;
```

複数のカラムの値も変更可能  

```
update table_name set column_name1 = value1, column_name2 = value2 where <以下略>;
```

- データの削除  

- delete  

```
delete from table_name <条件式>
```

- データベースの操作  

- データベースの作成
```create database daba_base_name;```  

- 現在あるデータベースの表示  
```show databases;```  

- 現在のデータベースの中にあるテーブルを表示する  
```show tables;```  

- 利用するデータベースを指定する  
```use database_name;```  

- テーブルの追加  

データベース内にテーブルを追加する  
```
create table table_name(

 # ここでカラムの指定をする
 # idとtitleを用意
 id int not null auto_increment primary key,
 title varchar(xxx) not null
 );
 ```  
 
 - テーブルのカラムを表示させる  
 ```show columns from table_name;```  
 
 - テーブルの構造を変更する  
 
 - 列追加  
 - 列変更  
 - 列削除  
 
 - 列の追加  
 
 ```
 alter table <table_name> add column_name <data type(int or varchar etc>) after <column_name>;
 ```
 
 - 列の変更  
 名前を変更したいとき  
 
 ```
 alter table <table_name> change old_column_name new_column_name <data type>;
 ```
 
 - 列の削除  
 
 ```
 alter table <table_name> drop <column_name>;
 ```
 
 - テーブルの削除  
 
 - drop  
 
 ```
 drop table <table_name>;
 ```
 
 - データベースの削除  
 
 ```
 drop database <database_name>;
 ```
 
 
