### enumerate

単純なfor文と違って要素と要素のインデックスを同時に取得することができる
- 使い方

1. インデックスの初期値を設定しない
2. インデックスの初期値を設定する

2.の場合、enumerate(list, indexの初期値)と第二引数なので注意

上記二通りある

```python
# forの場合
tmplist = ["a", "b". "c"]
for s in tmplist:
	print(s)

# a, b, cと改行されて表示

# enumerateを利用する場合

# 1. のとき
for item in enumerate(tmplist):
	print(item)
	
# タプルで返される
# (0, 'a')
# (1, 'b')
# (2, 'c')

for num, item in enumerate(tmplist):
	print(num, item)
	
# 0 a
# 1 b
# 2 c

# 2.のとき
# 今回はインデックスの値を1に設定
for num, item in enumerate(tmplist, 1):
	print(num, item)
	
# 1 a
# 2 b
# 3 c
```


