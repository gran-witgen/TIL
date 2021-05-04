## doctest  

関数直下のドキュメント部分にテストケースを書く  

Calculator.py
```python
class Calculator(object):
	def add_cal(self, x:object, y:object) -> object:
	
	"""ここにテストケースを書く
	add_cal
	>>> cal = Calculator()
	>>> cal.add_cal(1, 1)
	# 「>>>」で始まる記述のすぐ下に、テストケースの結果を書く
	2
	```
	# 順番としては先に関数を作ってから、その確認のためにdoctestを書く
	result = x + y
	return result
	

if __name__ == '__main__':
    import doctest
	# doctestのtestmod()を実行することでdoctestが可能になる
    doctest.testmod()
```
