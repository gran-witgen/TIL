# 相対パス、絶対パスの相互変換  

- 基本的な使い方

pathlib.Path(filename)でOSに合ったpathオブジェクトを取得する

```python
import pathlib
import os

# Desktopにtest.txtというファイルがあるとする
filepath = pathlib.Path("test.txt")

# 今回windows環境なのでwindows用のpathオブジェクトが表示される
filepath
# WindowsPath('test.txt')
```

- カレントディレクトリの絶対パスを取得する

pathlib.Path.cwd()でOSに合ったカレントディレクトリの絶対パスを表すpathオブジェクトを取得する

```python
import pathlib

currentdir = pathlib.Path.cwd()
currentdir
# WindowsPath('C:/XXXXXX/XXXXXX/Desktop')
```

osモジュールでもカレントディレクトリは文字列として取得できる

```python
import os

currentdir = os.getcwd()
currentdir
# 'C:\\XXXXX\\XXXXXX\\Desktop'
```

osモジュールではディレクトリの移動ができるが、pathlibモジュールでは移動はできない

- 相対パスを絶対パスへ変換

pathlib.Path.resolve()を利用する
```python
import pathlib

absolute_path = pathlib.Path("test.txt").resolve()
absolute_path
# WindowsPath('C:/XXXXX/XXXXX/Desktop/test.txt')
```

- 絶対パスを相対パスへ変換

pathli.Path.relative_to(起点となるパス)を利用する

```python
import path
import os

absolute_path = pathlib.Path("test.txt").resolve()
# WindowsPath('C:/XXXX/XXXXX/Desktop/test.txt')

relative_path = absolute_path.relative_to(os.getcwd())
# WindowsPath('test.txt')

# 以下でも同じ
relative_path2 = absolute_path.relative_to(pathlib.Path.cwd())
# WindowsPath('test.txt')
```
