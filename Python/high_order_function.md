## 高階関数

関数を変数のように扱うと関数を関数に渡すことができる。  

これだけだとなんのこっちゃ、なので簡単に説明すると  

- 引数が関数である関数がある・・・外部の関数
- 外部の関数の中身で、引数としてとった関数の引数をとる関数を作る・・・内部の関数
- 外部の関数が、内部の関数をオブジェクトとして返す

うーん、説明だとわからんのでコードを書く  


```python
def outer_function(func):# 1
    def inner_function(*func_args):# 2
        print("関数", func.__name__)
        print("引数", func_args)
        return func(*func_args)# 3
    return inner_function# 4


def add_int(x: int, y: int) -> int:
    return x + y


if __name__ == '__main__':
    result = outer_function(add_int)# 5
    print(result(5, 4))# 6
    """
    関数 add_int
    引数 (5, 4)
    9
    """
```

- 1で関数を引数とした外部関数を作る  
その戻り値は内部で定義する関数オブジェクト
- 2で1で定義した関数の引数をとる内部関数を定義する  
その戻り値は1で定義した関数を実行結果(つまり3)
- 4で内部関数オブジェクトを返す  
- 5で外部関数に内部関数を与え  
- 6でそれぞれを実行している

### デコレーター

上記の挙動を「@」を使うことで簡単に書くことができる。

外部関数をあらかじめ定義し、実行したい関数を定義する前に「@外部関数名」を記入する。


```python
def outer_function(func):
    def inner_function(*func_args):
        print("関数", func.__name__)
        print("引数", func_args)
        return func(*func_args)
    return inner_function
    
@outer_function
def add_int2(x: int, y: int) -> int:
    return x + y


if __name__ == '__main__':
    result2 = add_int2(5, 4)
    print(result2)
```

