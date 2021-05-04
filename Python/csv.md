## CSVモジュールの使い方

目的：csvファイルへデータを書き込む  
想定：カラムが指定されている    
前提：書き込むデータが二重配列

コードの流れ
1. 格納用変数を用意、初期化
2. ヘッダーがあれば1. で用意した変数に追加
3. csvモジュールからwriterクラスを呼び出し、書き込むデータをfor文で回し、1.の変数に追加
4. 1.の変数をwriterクラスのwriterows()で書き込む

```python
import csv

csv_header = ["id", "コード", "名前"]

original_data = [
    [
        "1", "100", "akira"
    ],

    [
        "2", "200", "kanako"
    ],

    [
        "3", "300", "ken"
    ]
]
csv_data = []
csv_data.append(csv_header)
with open("check.csv", "w", encoding="utf-8_sig") as f:# excelソフトで開くため、encodingはこれを指定
    writer = csv.writer(f, lineterminator="\n")
    for data in original_data:
        csv_data.append(data)
    writer.writerows(csv_data)
 
# id,コード,名前
# 1,100,akira
# 2,200,kanako
# 3,300,ken
```

目的：csvファイルのデータを読み込む  

コードの流れ  

1. with文でcsvファイルを開く  
2. csvモジュールよりreader()クラスを呼び出す  
3. ヘッダーを読み込むか読み込まないかを決める
4. for文で回す

```python
import csv

with open("check.csv", "r", encoding-"utf-8") as f:
	reader = csv.reader(f)
	
	# headerを読み込まない場合、以下の一文を入れる
	next(reader)
	# これを実行することで先頭行をスキップ
	
	for content in reader:
		print(content)
		
# ['1', '100', 'akira']
# ['2', '200', 'kanako']
# ['3', '300', 'ken']
```
