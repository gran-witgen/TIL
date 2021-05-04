# scssの書き方  

必要なもの  

- vscode 拡張機能 live sass compiler  

### scssとは  

cssファイルを作成しやすくするもの。拡張子はscss  

scssファイルを作成後、sass compilerを実行するとcssファイルが作成される  

scssでできること  

##### 変数の利用  

変数を宣言、その値を利用することが可能  

$変数名: プロパティ名;  

```scss
// 色を指定
$color_black:black;

.btn{
  background-color: $color_black;
}
```

#### ネストの利用  

ブロックの中で入れ子を作成することで、特定の要素だけをスタイルを充てられる  

practice_index.html
```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="practice_style.css">
</head>
<body>
    <div id="container">
        <button class="btn temp_element1">Button1</button>
        <button class="btn temp_element2">Button2</button>
    </div>
</body>
</html>
```

practice_style.scss(compilerによりpractice_style.cssに変換される)  

```scss
//変数の宣言
$color_black: black;
$color_blue: blue;
$color_red: red;
$color_white: white;

#container{
    text-align: center;
}

.btn{
    // 変数の代入を行う
    border: 1px solid $color_black;
    font-weight: 600;
    padding: 10px 40px;
    
    // ネストを用いてクラスにより適用させるスタイルを変更する
    &.temp_element1{
        background-color: $color_black;
        color: $color_white;
    }
    &.temp_element2{
        background-color: $color_red;
        color: $color_blue;
    }
}
```
