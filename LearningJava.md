# Javaメモ  

継承関係にあるクラスのコンストラクタについて  
スーパークラスで定義されているコンストラクタは、サブクラスでは継承されない。  
サブクラスでコンストラクタを設定しない場合、デフォルトコンストラクタが実行される  
デフォルトコンストラクタとは、スーパークラスのコンストラクタである  

sample  
```java
class A{
  A(){
    System.out.println("引数なし");
  }
  A(String a){
    System.out.println("引数あり");
  }
}

class B extends A {
}
```

上記の際に  
```java
B b = new B();
```
と実行すると、「引数なし」と表示される  
これはclass Bにおいて、コンストラクタが設定されていないため、デフォルトコンストラクタである  
「super()」が実行された。このデフォルトコンストラクタは、サブクラスでコンストラクタを定義した場合に削除される  

また、サブクラスで設定されたコンストラクタが実行された際に、スーパークラスのコンストラクタも一度実行している。  
これは仮想的に追加されているもののため、明示的にしたい場合、super()やsuper("a")など引数ありなしと定義しても良い  


アクセス修飾子  

- public  
- protected  
- private  
- なし  

public  
他のクラスからでもアクセス可  

protected  
サブクラスもしくは同じパッケージ内のクラスのみアクセス可  

なし  
同一パッケージのクラスのみアクセス可  

private  
同じクラス内のみアクセス可  

抽象クラス  
インスタンスを作れないクラス  

sample
```java
abstract classs Sample{
}
```
抽象メソッド  
abstractがついたメソッド。宣言方法は  

sample  
```java
abstract void sample();
```  

と具体的な{}をつけない  

抽象メソッドを含むクラスは必ず抽象クラスにする必要があり、さらに抽象クラスを継承したクラスは抽象メソッドをオーバーライドしないと  
抽象クラスのまま  

インターフェース  

インターフェースとはクラスが持つべきメソッドを記したルールみたいなもので、クラスはインターフェイスを実装(implements)することができる  
インターフェースを実装するクラスは、インターフェースで宣言されたメソッドをすべて実装しなければならない  

インターフェースの宣言  
sample  
```java
interface SampleInterfaceName{
}
```

インターフェイスを実装する  

sample  
```java
class Sample implements SampleInterfaceName{
}
```

なお、インターフェイスで宣言されたメソッドは、public abstract修飾子がついているため、クラスで実装する際にも  
public修飾子を付ける必要がある  

Javaの配列作成  


sample
```java
型名 [] 変数名 = new 型名 [要素数];
```

例外処理  

基本構文  
```java
try {
} catch (例外型名 変数){
}
```  

例外オブジェクトはExceptionクラスのサブクラス　　

sample  
```java

class NotHaveMoney extends Exception{
    NotHaveMoney(String message){
        super(message);
    }
}

class Me {
    int money;

    void setMony(int money){
        try {
            if (money < 0) {
                throw new NotHaveMoney("お金がマイナスです");
            }
            this.money = money;
            System.out.println("所持金は " + this.money + "です");
        } catch (NotHaveMoney e){
            e.printStackTrace();
            System.out.println(e);
        }
    }

    void calcZero(int a, int b) {
        try {
            int c = a / b;
            System.out.println(c);
        } catch (Exception e){
            e.printStackTrace();
        }
    }
}

public class Sample {
    public static void main(String [] args){
        int [] moneyList = new int [2];
        moneyList[0] = 5;
        moneyList[1] = -5;
        Me a = new Me();
        Me b = new Me();
        a.setMony(moneyList[0]);
        b.setMony(moneyList[1]);
        int c = 10;
        int d = 0;
        a.calcZero(c, d);
    }
}
```

setMoneyの「throw new Exception Name」で(自作)例外を読んでいる  
Pythonのraiseみたいなもの  

例外をメソッドの呼び出し元へ渡す  

基本構文
```java
戻り値 method_name(引数) throws 例外の型 {
　例外可能性のある処理;
}
```

sample
```java
class NotHaveMoney extends Exception{
    NotHaveMoney(String message){
        super(message);
    }
}

class TestThrowsException extends Exception {
    TestThrowsException(String message){
        super(message);
    }
}

class Me {
    int money;

    void testThrowsExcept() throws TestThrowsException{
        throw new TestThrowsException("例外を呼び出し元に渡します");
    }

    void setMony(int money){
        try {
            if (money < 0) {
                throw new NotHaveMoney("お金がマイナスです");
            }
            this.money = money;
            System.out.println("所持金は " + this.money + "です");
        } catch (NotHaveMoney e){
            e.printStackTrace();
            System.out.println(e);
        }
    }



    void calcZero(int a, int b) {
        try {
            int c = a / b;
            System.out.println(c);
        } catch (Exception e){
            e.printStackTrace();
        }
    }
}

public class Sample {
    public static void main(String [] args){
        int [] moneyList = new int [2];
        moneyList[0] = 5;
        moneyList[1] = -5;
        Me a = new Me();
        Me b = new Me();
        a.setMony(moneyList[0]);
        b.setMony(moneyList[1]);
        int c = 10;
        int d = 0;
        a.calcZero(c, d);
        try {
            a.testThrowsExcept();
        } catch (TestThrowsException e){
         e.printStackTrace();
        }
    }
}
```

Thread

Threadの作り方  

1. Threadクラスを継承したサブクラスのインスタンスでrun()をオーバーライドして、start()を実行する　　
2. Runnableインターフェイスを実装したクラスのインスタンスをThreadクラスのコンストラクタの引数として扱い、start()を行う  

1. example  
```java
class SampleThread extends Thread {
    public void run(){
        for (int i =0; i < 100; i += 1){
            System.out.println("sample threadのrunメソッド" + i);
        }
    }
}

public class Sample {
    public static void main(String [] args){
        SampleThread sh = new SampleThread();
        sh.start();
        for (int i =0; i < 100; i +=1){
            System.out.println("main関数の実行です" + i);
        }
    }
}
```
2. exmaple
```java
class SampleThread extends Thread {
    public void run(){
        for (int i =0; i < 100; i += 1){
            System.out.println("sample threadのrunメソッド" + i);
        }
    }
}

class SampleThread2 implements Runnable {
    public void run(){
        for (int i =0; i < 100; i += 1) {
            System.out.println("sample thread2のrunメソッド" + i);
        }
    }
}

public class Sample {
    public static void main(String [] args){
        SampleThread2 sh2 = new SampleThread2();
        Thread th = new Thread(sh2);
        th.start();
        for (int i =0; i < 100; i +=1){
            System.out.println("main関数の実行です" + i);
        }
    }
}
```

スレッドの処理が終わるまで待つ  

マルチスレッドのプログラムだと各々スレッドが独自に処理を進めてしまうが  
join()を使うことで、処理を待つことができる  

```java
class SampleThread extends Thread {
    public void run(){
        for (int i =0; i < 100; i += 1){
            System.out.println("sample threadのrunメソッド" + i);
        }
    }
}

class SampleThread2 implements Runnable {
    public void run(){
        for (int i =0; i < 100; i += 1) {
            System.out.println("sample thread2のrunメソッド" + i);
        }
    }
}


public class Sample {
    public static void main(String [] args){
        SampleThread2 sh2 = new SampleThread2();
        Thread th = new Thread(sh2);
        th.start();
        // 以下の記述でthの処理が終わるまでmainスレッドは処理を始めない
        try{
            th.join();
        }catch (InterruptedException e){
            System.out.println(e);
        }
        System.out.println("スレッドの処理が終わりました");
        for (int i =0; i < 100; i +=1){
            System.out.println("main関数の実行です" + i);
        }
    }
}
```

Threadの同期  
同期を行わないと想定外の処理結果となる  
その場合、synchronized修飾子をつけることで同期を取ることができる。  
該当修飾子がある関数が実行されるとがロックされ、処理が完了するまで、他のスレッドから呼び出せなくなる
