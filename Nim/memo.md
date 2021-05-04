# 参考になる

- [Syntax of Nim](https://gist.github.com/miyakogi/b1df00c8bc99927d9d0d)

- https://github.com/nim-lang/Nim/wiki/Nim-for-Python-Programmers


### for

```nim
# 10まで表示する
for i in 0..10:
  echo(i)
  # 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
  
# 10まで表示しない。9で終わる
for i in 0..<10:
  echo(i)
  # 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
```

### ビルトインProcedures呼び出し
nimのprocedure呼び出しは、組み込みについては()を付けてもつけなくても動く
```nim
let test_string:string = "what beautiful day!"
echo(test_string.len())
# 19

let test_string:string = "what beautiful day!"
echo(test_string.len)
# 19
```

個人的には()つけていた方が見やすい。

### forでのインデックス取得
for counter, item in sequence
で、そのインデックスが取得できる。
```nim
let test_string:string = "what beautiful day!"
for counter, letter in test_string:
    echo("this position is ", counter, " and letter is ", letter)
# this position is 0 and letter is w
# this position is 1 and letter is h
# this position is 2 and letter is a
# this position is 3 and letter is t
# this position is 4 and letter is
# this position is 5 and letter is b
# this position is 6 and letter is e
# this position is 7 and letter is a
# this position is 8 and letter is u
# this position is 9 and letter is t
# this position is 10 and letter is i
# this position is 11 and letter is f
# this position is 12 and letter is u
# this position is 13 and letter is l
# this position is 14 and letter is
# this position is 15 and letter is d
# this position is 16 and letter is a
# this position is 17 and letter is y
# this position is 18 and letter is !
```

pythonでいうenumerate()と同じ
```python
msg = "what beautiful day!"
for i, item in enumerate(msg):
    print(f"this position is {i} and letter is {item}")
    
# オフセットを1にしたい場合は以下
for i, item in enumerate(msg, 1):
    print(f"this position is {i} and letter is {item}")
```

aが抜けてる。。

### procedureの引数について

procedure外で宣言した変数を変更する場合、以下の方法では認められない
```nim
proc add_int(x:int):int =
  x += 5
  return x
  
var variable_proc_out:int = 6
var res:int = add_int(variable_proc_out)
echo(res) # error
```

以下のように、procedureの引数の型の前にvarを付けると可能になる
```nim
proc add_int(x:var int):int =
     x += 5
     return x
    
var variable_proc_out:int = 6
var res:int = add_int(variable_proc_out)
echo(res)
# 11
```

### データ操作

まだ途中  
以下を参照する  
http://flat-leon.hatenablog.com/entry/nim_howto


  




