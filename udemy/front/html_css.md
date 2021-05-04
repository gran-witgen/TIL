### フロントエンジニア向けの基礎知識

雛形

```html
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title></title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
  
</body>
</html>
```

<input>タグの書式

```
<input type="hoge" name="hogehoge">  
type:それぞれの書式を選ぶ。email, password, text, etc..  
name:inputタグがたくさんあった場合、nameによって区別をする。  
```

<button>タグ
```
<button type="submit">
これで送信ボタン
```

#### css配置

cssで体裁を整える。  

headタグ内でlinkタグから指定する
```
<link rel="stylesheet" href="cssfile_path">
```

### ブラウザが自動で固有のcssを適用させないよう、リセットする

以下のurlからcssをダウンロードする。  

https://csstools.github.io/sanitize.css/


cssファイルから、sanitize.cssを読み込む方法  

下記のcssファイルがあったとする。

```css
h1 {
  font-size: 24px;
}
```

それをいかに変更する。  

```css
@import url("path_of_sanitize.css");

h1 {
  font-size: 24px;
}
```
