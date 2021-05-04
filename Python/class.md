### クラスで継承した際によく間違える  

Pythonでのクラスの作り方  

```python
class class_name(object):
  pass
```

クラスからインスタンスを作成できる  
インスタンスにそれぞれの初期値を与えることができる  

```python
def __init__(self, param1, param2):
  self.param1 = param1
  self.param2 = param2
```

sample  

```python

class Human(object):
  def __init__(self, name, age):
    self.name = name
    self.age = age
```

クラスを複数作り、それぞれ継承することができる  

```python
class Child_class_name(Parent_class_name):
  pass
 ```

子クラスのinit()にて、super()を使って親クラスのinitを呼び出す。

```python
class Human(object):
  def __init__(self, name, age):
    self.name = name
    self.age = age
    
class Warriror(Human):
  def __init__(self, name, age, weapon):
    super().__init__(name, age)
    self.weapon = weapon
```
