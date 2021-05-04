## unittest

【前提】  
Pycharm利用 

Pycharmの環境を設定する  
1. 「Edit Configrations」
2. 「+」から「Python tests」-> 「Unittests」を選択
3. 対象となるテスト用ファイルを選択しOK押下

流れ  

1. テスト対象となるファイルを作成
2. テスト用ファイルを作成
3. テスト用ファイル内でunittestのインポート。unittest.TestCaseを継承したクラスを作成。  
4. 作成したクラス内で、テスト用の関数を作成する。その時、作成する関数の命名は<b>「test_テスト対象としたい関数名」</b>にすること
5. テスト用の関数内でテストを実行する

【テスト対象ファイル】
calculator.py
```python
class Calculator(object):
  def cal_add(self, x: object, y: object) -> object:
    result = x + y
    return result
```

【テスト用ファイル】
test_calculator.py
```python
import unittest
import calculator

class CalcuTest(unittest.TestCase):
  # テスト用関数の命名を気を付けること
  def test_cal_add(self):
    cal = calculator.Calculator()
    # resultが一致するか確認する
    self.assertEqual(
      cal.cal_add(1, 1), 2
      )
# pycharmを利用している場合は不要だが、使っていないときは
if __name__ == '__main__':
  unittest.main()
```

### unittestで例外処理についてテストしたいとき

流れ


1. self.assertEqual()などのテスト確認用の関数を使う前に「self.assertRaises()」で発生する例外を指定する
2. その前にwithを利用する

test_calculator.py
```python
import unittest
import calculator

class CalcuTest(unittest.TestCase):
  def test_cal_add(self):
    cal = calculator.Calculator()
    # ここまでは一緒
    with self.assertRaises(ValueError):
      self.assertEqual(
        cal.cal_add("3", "5"), 8
        )
```

### setUpとtearDown

それぞれテストを行う関数の前後に処理を挟みたい場合に利用する

setUp　・・・テスト関数の前に実行  
tearDown　・・・テスト関数の後に実行

test_calculator.py
```python
import unittest
import calculator

class CalcuTest(unittest.TestCase):
  
  # setUp()でコンストラクタを
  def setUP(self):
    self.cal = calculator.Calculator()
    print("test start")
    
  def tearDown(self):
    print("test end")
    del self.cal

  def test_cal_add(self):
    self.assertEqual(
      self.cal.cal_add(1, 1), 2
      )
      
  def test_cal_add(self):
    with self.assertRaises(ValueError):
      self.assertEqual(
        self.cal.cal_add("3", "5"), 8
        )
```

### unittestのスキップ  

特定の条件でテストを行いたいor行わないときに有効  

ポイント 

テストしたい関数の前にデコレータとして@unittest.skip()をつける  
unittest.skip()の引数は文字列が入る。

使い方:unittest.skip(reason)  
何も表示させたくない場合はreason=""を入れればよさそう  

test_calculator.py
```python
import unittest
import calculator


class CalcuTest(unittest.TestCase):

    def setUp(self):
        self.cal = calculator.Calculator()

    def test_cal_add(self):
        self.assertEqual(
        self.cal.cal_add(1, 1), 2
    )
    
    # 以下のテスト関数はスキップされる
    @unittest.skip("")
    def tests_cal_add_raise(self):
        # self.assertRaises()で発生する例外を指定する
        # その際withを使うこと
        with self.assertRaises(ValueError):
            self.assertEqual(
                self.cal.cal_add("2", "3"), 5
            )
```

@unittest.skipIf()を使うことで特定の条件下のみでテスト対象の関数をスキップすることができる

test_calculator.py
```python
import unittest
import calculator

app_env = "dev"

class CalcuTest(unittest.TestCase):

    def setUp(self):
        self.cal = calculator.Calculator()

    def test_cal_add(self):
        self.assertEqual(
        self.cal.cal_add(1, 1), 2
    )

    # app_envがdevの場合、この関数をスキップする
    @unittest.skipIf(app_env=="dev", "")
    def tests_cal_add_raise(self):
        # self.assertRaises()で発生する例外を指定する
        # その際withを使うこと
        with self.assertRaises(ValueError):
            self.assertEqual(
                self.cal.cal_add("2", "3"), 5
            )
```


