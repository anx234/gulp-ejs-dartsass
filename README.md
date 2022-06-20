# gulp-ejs-dartsass

```command
npm i
```
```command
npx gulp
```
### 開発場所
srcディレクトリで開発します。docsフォルダは納品用です。

### 変数
src/asset/sass/foundation/_system.scss
で各種設定してください。

## mixin
開発時間の短縮、また品質の管理のためにMixinの積極的な使用を推奨します
使用方法は以下の通りです。

### メディアクエリ
メディアクエリは後述のmixinを使って
クラスの中に書いてください。
```scss
OK
.hoge {
  width: 100%
  @include MQ(md){
    width: 50%;
  }
}

NG
@media screen and (max-width: 767px){
  .hoge {
    width: 50%
  }
}
```
ブレークポイントは基本767でナビゲーションだけ切らないと厳しいみたいな場合は
_system.scssに	"nav": "(max-width: 920px)",という形で追加してください

### MQ
メディアクエリの省略記法です。引数には_vars.scssに定義されている文字列が入ります。
```scss
.hoge {
  width: 100%
  @include MQ(md){
    width: 50%;
  }
}
↓
.hoge {
  width: 100%
}
@media screen and (max-width: 767px){
  .hoge {
    width: 50%
  }
}
```
### FHA
@mixin FHA() {
  #{&}:focus,
  #{&}:hover,
  #{&}:active{
    @content;
  }
}


### contentCentering
コンテンツをセンタリングし、かつサイト幅制限や左右に余白を持たせる処理も加えます。処理内容はコードを確認してください。
```scss
@mixin contentCentering(){
  max-width: $contWidth;
  padding-right: $contSpace;
  padding-left: $contSpace;
  margin-right: auto;
  margin-left: auto;
  @include MQ(md) {
    max-width: 100%;
  }
}
```
### line-height計算
@function autoSpace($num:0, $fz:$fz, $lh:$lh){
    //px変換し、単位を除く値のみを取得
    $fzValue: (math.div($fz, (floor($fz) * 2) % 2 + 1)) * 10;
    @return $num - (math.div($lh * $fzValue - $fzValue, 2)) + px;
  }
  
  @function sp_autoSpace($num:0, $fz:$sp_fz, $lh:$sp_lh){
    $fzValue: (math.div($fz, (floor($fz) * 2) % 2 + 1)) * 10;
    @return $num - (math.div($lh * $fzValue - $fzValue, 2)) + px;
  }
