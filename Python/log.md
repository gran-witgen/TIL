## ログの出力について

### ログを別ファイルへ出力するまでの流れ

1. Loggerオブジェクトの作成  
2. Loggerオブジェクトのメッセージレベル設定  
3. Handlerの作成  
4. Handlerのメッセージレベル設定  
5. LoggerにHandler(の設定)を付与  
6. ログ出力  

上記のような流れになる。  

logconf.py
```python
import logging
from logging import StreamHandler
from logging import FileHandler
from logging import getLogger
from logging import Formatter

# loggerオブジェクトの作成。ここに実行するファイル名を記載する
logger = getLogger("main.py")

# メッセージレベルの設定
logger.setLevel(logging.DEBUG)

# 標準出力用のハンドラを作成
stream_handler = StreamHandler()

# メッセージレベルの設定
stream_handler.setLevel(logging.DEBUG)

# 別ファイルへログを吐き出すハンドラの作成。ここにログを排出するファイルを指定する
file_handler = FileHandler("check_status.log", "a", encoding="utf-8")

# メッセージレベルの設定
file_handler.setLevel(logging.DEBUG)

# フォーマットの作成。標準出力、ログ出力の形式を指定する
handle_format = Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')

# ファイル出力のフォーマットをセットする
file_handler.setFormatter(handle_format)

# 標準出力のフォーマットをセットする
stream_handler.setFormatter(handle_format)

# loggerオブジェクトへ標準出力用ハンドラを付与
logger.addHandler(stream_handler)

# loggerオブジェクトへログ出力用ハンドラを付与
logger.addHandler(file_handler)
```

main.py
```python
import logconf

def testshowlog():
    try:
        logconf.logger.info("log test start")
        #何かの処理
    except Exception as err:
        logconf.logger.error(err)
    finally:
        logconf.logger.info("log test end")

if __name__ == "__main__":
    testshowlog()
```

ログ設定を設定ファイルに書き出す
logconfig.conf

```config
[loggers]
;ロガー名の指定。名前は何でもよい
;,で複数作成可能
keys=root, logger_name1, logger_name2

[handlers]
;ハンドラー名の設定。名前は何でもよい
;,で複数作成可能
keys=root_handlers, logger_name1_handlers, logger_name2_handlers

[formatters]
;フォーマットの指定。名前は何でもよい
;,で複数作成可能
keys=root_fmt, logger_name1_fmt, logger_name2_fmt

;個別のフォーマットの設定
;[formatters]で指定したkeyが対象となる。[formatter_formatters_name]
[formatter_root_fmt]
format=%(asctime)s %(name)s %(levelname)s %(message)s
class=logging.Formatter

[formatter_print_test1_fmt]
format=%(asctime)s %(name)s %(levelname)s %(message)s
class=logging.Formatter

[formatter_print_test2_fmt]
format=%(asctime)s %(name)s %(levelname)s %(message)s
class=logging.Formatter

;ハンドラの個別設定。[handlers]で指定したkeyが対象
[handler_root_handlers]
class=StreamHandler
level=DEBUG
formatter=root_fmt
args=(sys.stdout,)

[handler_print_test1_handlers]
class=FileHandler
level=INFO
formatter=print_test1_fmt
;排出するログの指定。タプルにすること
args=("print_test1_check.log",)

[handler_print_test2_handlers]
class=FileHandler
level=INFO
formatter=print_test2_fmt
;排出するログの指定。タプルにすること
args=("print_test2_check.log",)

;ロガーの個別設定。[loggers]で指定したkeyが対象。[logger_loggers_name]
[logger_root]
level=NOTSET
;ハンドラの設定
handlers=root_handlers

[logger_print_test1]
level=NOTSET
;ハンドラの設定
handlers=print_test1_handlers
;logging.getLogger()の引数の指定
qualname=print_test1

[logger_print_test2]
level=NOTSET
handlers=print_test2_handlers
qualname=print_test2
```

以下サンプル例  

logconfig.conf
```config
[loggers]
keys=root, print_test1, print_test2

[handlers]
keys=root_handlers, print_test1_handlers, print_test2_handlers

[formatters]
keys=root_fmt, print_test1_fmt, print_test2_fmt

[formatter_root_fmt]
format=%(asctime)s %(name)s %(levelname)s %(message)s
class=logging.Formatter

[formatter_print_test1_fmt]
format=%(asctime)s %(name)s %(levelname)s %(message)s
class=logging.Formatter

[formatter_print_test2_fmt]
format=%(asctime)s %(name)s %(levelname)s %(message)s
class=logging.Formatter

[handler_root_handlers]
class=StreamHandler
level=DEBUG
formatter=root_fmt
args=(sys.stdout,)

[handler_print_test1_handlers]
class=FileHandler
level=INFO
formatter=print_test1_fmt
args=("print_test1_check.log",)

[handler_print_test2_handlers]
class=FileHandler
level=INFO
formatter=print_test2_fmt
args=("print_test2_check.log",)

[logger_root]
level=NOTSET
handlers=root_handlers

[logger_print_test1]
level=NOTSET
handlers=print_test1_handlers
qualname=print_test1

[logger_print_test2]
level=NOTSET
handlers=print_test2_handlers
qualname=print_test2
```

print_test1.py
```python
import logging.config


def print_test1():
    logging.config.fileConfig("logconfig.conf")
    logger = logging.getLogger("print_test1")

    logger.info("process start!")
    print("test1")
    logger.info("test1")
    logger.info("test1 done")


if __name__ == "__main__":
    print_test1()
 ```
 
 print_test2.py
 ```python
 import logging.config


def print_test2():
    logging.config.fileConfig("logconfig.conf")
    logger = logging.getLogger("print_test2")

    logger.info("process start!")
    print("test2")
    logger.info("test2")
    logger.info("test2 done")


if __name__ == "__main__":
    print_test2()
```


