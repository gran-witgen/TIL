## splitとjoin

### split()  

文字列に対し、引数で与えた値によって文字列を分割する。  

### join()  

join()の正しい使い方は、"文字列".join(リスト)であり、リストの各要素に対し、文字列でつなげ、結果文字列を返す。  
注意点として、リスト内の要素が文字列型である場合に使え、数値型の場合は使えない  

```python
s: str = "test1, test2, test3"
ts: list = s.split(",")
# ['test1', ' test2', ' test3']
"!".join(ts)
# 'test1! test2! test3'
```
