# configparseの使い方

設定ファイルを用意する

conf.ini
```conf
[setting]
url:xxxxx
```

設定ファイルを読み込む
read_conf.py
```
import configparser

config = configparser.ConfigParser()
config.read("conf.ini")

print(config["setting"]["url"])
# "XXXXX"
```

設定ファイルを書き込む
write_conf.py
```
import configparse

config = configparser.Configparser()

config["setting"] = {
	"url":"XXXXX"
}

with open("config.ini", "w") as config_file:
	config.write(config_file)
```

なお、config.iniは直接ファイルを作成してもよい
