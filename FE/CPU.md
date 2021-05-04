## CPU

CPUとコンピュータの装置  

- 制御装置
- 演算装置
- 記憶装置
- 入力装置
- 出力装置

CPU = 制御装置+演算装置  

データの流れ  

制御装置→入力装置  
制御装置→補助記憶装置  
制御装置→演算装置  
制御装置→出力装置  
演算装置⇔主記憶装置  
補助記憶装置⇔主記憶装置  
etc  

プログラム  
補助記憶装置→実行時、主記憶装置へ移動→CPUがプログラムの命令を一つずつ取り出し実行　　

主記憶装置の一定の区画ごとに番号が振られており、それがアドレス  

主記憶装置へ移ったプログラムの命令を取り出し実行して得られた情報はCPUのレジスタという内部記憶装置に保存される

### レジスタの種類

- プログラムカウンタ　次の実行する命令が入るアドレスを記憶するレジスタ
- 命令レジスタ　取り出した命令を一時的に保存するレジスタ
- インデックスレジスタ　連続したデータの取り出しに使うための増分値を保存する。よくわからん
- ベースレジスタ　プログラムの先頭のアドレスを保存する
- アキュームレータ　演算の対象となる数や演算結果を保存する
- 汎用レジスタ　とくに機能を限定していないレジスタ
- 命令デコーダ　取り出した命令を解読する


命令の実行手順と利用するレジスタ

①命令の取り出し。フェッチ  
利用するレジスタ

- 命令レジスタ
- プログラムカウンタ

②命令の解読  
利用するレジスタ

- 命令レジスタ
- 命令デコーダ

命令レジスタに保存された命令は、命令部とオペラント部(対象となるデータが入ったメモリアドレス)に分けられ、命令部(命令の種類)が命令デコーダに渡される  

③対象データの読み出し  
利用するレジスタ

- 命令レジスタ
- 汎用レジスタ  

オペラント部を参照し、特定のメモリアドレスから必要な情報を取得後、それを汎用レジスタに保存する  

④命令の実行  
利用するレジスタ

- 汎用レジスタ

そのまま実行。　　
以後この繰り返し  

###   機械語のアドレス指定方式

計算を行い、もとめた主記憶装置上のアドレスを実行アドレスなどという。  
オペラント部には主記憶装置の対象となるデータが入ったメモリアドレスが入っている場合も入っていない場合等様々ある。  
したがって何らかの方法でメモリアドレスを求める必要があり、これをアドレス修飾、指定などという。  

- 即値アドレス指定方式
- 直接アドレス指定方式
- 間接アドレス指定方式
- インデックスアドレス指定方式
- ベースアドレス指定方式
- 相対アドレス指定方式

#### 即値アドレス指定方式

オペランド部に対象のデータそのものの値が入っている  

#### 直接アドレス指定方式

オペランド部に記載してあるアドレスが、実行アドレスである

#### 間接アドレス指定方式

オペランド部に記載しているアドレスの中に、対象となるデータの場所を示すアドレスが入っている  

#### インデックスアドレス指定方式

命令レジスタに渡された命令が命令部、インデックスレジスタ番号、オペランド部に分けられる場合  
インデックスレジスタ番号の示すインデックスレジスタの値(dictみたいな感じ)とオペランド部に記載されているアドレス先のデータの値とを加算することで  
実行アドレスを求める  

example  
```
main_storage = {"0100": 1, "0110": 5} # 便宜上2こまで
index_register = {"1": 5, "2": 10} # 便宜上2までとする
operand = 100
execute_address = index_register[1] + operand
# 欲しい実行アドレスのデータ
main_storage[execute_address]
```

### ベースアドレス指定方式

ベースレジスタの値とオペランド部の値を加算し、メモリ上の実行アドレスを取得する  
ベースレジスタとは、プログラムがメモリ上にロードされた時の先頭アドレスを記憶するレジスタのこと。

### 相対アドレス指定方式

プログラムカウンタの値をオペランド部の値を加算し、メモリ上の実行アドレスを取得する。  
プログラムカウンタは次に実行される命令へのメモリアドレス。  

### CPUの性能指標

CPUの性能はクロック周波数、CPI、MIPSなどの指標値を用いる。  

#### クロック周波数

クロックと呼ばれる周期的な信号。時計のようにちくたく動くと考える。  
この周期的な運動が早ければ早いほど多くの処理ができる。ﾁｸﾀｸﾁｸﾀｸﾁｸﾀｸﾁｸﾀｸ  
クロックが一秒間に繰り返す回数をクロック周波数という。単位はHz。  

1クロックにかかる時間  

example  

クロック周波数5HzのCPUがあるとする。  
一秒間にクロックが5回繰り返される　-> 1/5秒  

つまり1回クロックにどれくらい時間が必要か、の計算は  

### 1 / クロック周波数　　

で求める。  
ちなみに、この時間のことをクロックサイクル時間と呼ぶ。  

### CPI(Clock cycles Per Instruction)

1命令あたり、クロックサイクルが何回必要かを表す。  

example

1命令に4クロック必要　-> 4CPI  

CPIとクロックサイクル時間を利用することで、命令の実行時間を求められる。  

命令実行時間　= 1クロックに必要な時間 * CPI  

example  

クロック周波数10Hz、一命令に5クロック必要だとすると  

クロックサイクル時間(1クロックに必要な時間) = 1 / 10 秒  
1命令に必要なクロックサイクル数　= 5  
したがって 1/10 * 5 = 1/2秒  

※補助単位は別に記載する  

### MIPS (Million Instructions Per Second)

一秒間に実行できる命令の数を表す  

数字が大きくなりがちなので、命令の数は「100万」単位となる。  

example  

20MIPS -> 一秒間に2000万の命令を実行できる  
100MIPS -> 一秒間に10000万の命令を実行  

「一つの命令を実行するのに平均していくらいくらかかる」CPUがあったとすると、MIPS値の算出は以下になる。  

* 途中