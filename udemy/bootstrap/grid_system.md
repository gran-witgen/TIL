# grid system  

1ページ全体を横幅12分割で構成する。  
各コンテンツが何列分で構成するかを指定する。  

以下は3等分をサンプルに記載  


```html
<div class="container">
  <div class="row">
    <div class="col bg-primary">ブロック1</div>
    <div class="col bg-secondary">ブロック2</div>
    <div class="col success">ブロック3</div>
  </div>
</div>
```

col-numberで何列分の幅を持たせるかで指定することができる
```html
<div class="container-fluid">
  <div class="row">
    <div class="col-3 bg-primary">ブロック1</div>
    <div class="col-5 bg-primary">ブロック2</div>
    <div class="col-4 bg-primary">ブロック3</div>
  </div>
</div>
```
      
