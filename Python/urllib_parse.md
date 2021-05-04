# urllib.parse

urlを解析し、要素に分けるライブラリ

<s>はじめに注意点</s>


<s>何かできなくない？</s>
```python
import urllib

urllib.parse.urlparse()
```

公式を見るとfromを使っている&Pycharm上でもエラーは起きない
```python
from urllib.parse import urlparse

urlparse()
```

そのため、こちらを使うことになる。<s>(現場だと最初の書き方となっている、できなくない？)</s>

### 使い方

- urllib.parse.urlparser()
urlparse()は引数のurlを要素ごとに分けてくれる

```python
from urllib.parse import urlparse

url = 'https://github.com/py-py-py/TIL/new/master/Python'
o = urlparse(url)
print(o)
# ParseResult(scheme='https', netloc='github.com', path='/py-py-py/TIL/new/master/Python', params='', query='', fragment='')

# それぞれ、scheme, netloc, path, params, query, fragmentを指定することで要素を取得できる
print(o.scheme) # https
print(o.netloc) # github.com
print(o.path) # /py-py-py/TIL/new/master/Python
print(o.params) # ""
print(o.fragment) # ""
```

注意点:urlparse()はプロトコル(http: or https:)以下のurlが「//」で始まらない限り、netlocを認識せず、pathから値を取得する
```python
from urllib.parse import urlparse

url = 'https://github.com/py-py-py/TIL/new/master/Python'
o = urlparse(url)
print(o)
# ParseResult(scheme='https', netloc='github.com', path='/py-py-py/TIL/new/master/Python', params='', query='', fragment='')

url1 = '//github.com/py-py-py/TIL/new/master/Python'
o1 = urlparse(url1)
print(o1)
# ParseResult(scheme='', netloc='github.com', path='/py-py-py/TIL/new/master/Python', params='', query='', fragment='')

url2 = 'github.com/py-py-py/TIL/new/master/Python'
o2 = urlparse(url2)
print(o2)
# ParseResult(scheme='', netloc='', path='github.com/py-py-py/TIL/new/master/Python', params='', query='', fragment='')
```

[参考](https://docs.python.jp/3/library/urllib.parse.html)
