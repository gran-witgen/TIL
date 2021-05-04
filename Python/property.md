## Pythonのgetter, setter, propertyについて  

非公開変数への他クラスからのアクセスを可能にするには@propertyを使う  


通常、以下のコードだとエラーが出る。  

user.py
```
class User(object):
    def __init__(self, name):
        self.__name = name
```

animal.py
```
class Animal(object):
    def __init__(self, name, family):
        self.name = name
        self.family = family
        
    def show_family(self):
        return self.family
```

main.py
```
from user import User
from animal import Animal

def main():
    user = User("tarou")
    # 以下のコードでuser.nameが見えないためエラー
    animal = Animal("conny", user.name)
    animal_family = animal.show_family()
    
    
 if __name__ == "__main__":
    main()
```

Userクラスのnameが非公開変数となっており、他クラスから参照できない。  
これを可能にするには、Userクラスに@property及び@変数.setterを用意する。  

user.py
```
class User(object):
    def __init__(self, name):
        self.__name = name
        
    @property
    def name(self):
        return self.__name
        
    @name.setter
    def name(self, name):
        self.__name = name
```

ポイントは  

- @propertyと@変数名.setter以下で定義する関数名を一緒にする
- 呼出し先の他クラスでは変数への参照ないし、代入として扱うこと
