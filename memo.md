# 道中メモ

# 12.3

## Box<dyn Error>>

トレイトオブジェクトについては、第17章で講義します。 とりあえず、Box<dyn Error>は、関数がErrorトレイトを実装する型を返すことを意味しますが、 戻り値の型を具体的に指定しなくても良いことを知っておいてください
これにより、 エラーケースによって異なる型のエラー値を返す柔軟性を得ます。dyn キーワードは、"dynamic"の略です。

→ エラーだけどどのエラーかは実行時に確定する

## ?

expectの呼び出しよりも?演算子を選択して取り除きました。第9章で語りましたね。 エラーでパニックするのではなく、?演算子は呼び出し元が処理できるように、現在の関数からエラー値を返します。

## Result 使ってないって warning 出してくれるの優しいな

## if let

if let は、match のようなものですが、match よりもシンプルです。

```rust
if let Ok(num) = String::from("1").parse::<i32>() {
    println!("num is {}", num);
}
```

## ライブラリクレートへ（切り出し）

```rust
extern crate minigrep;

use minigrep::Config;
```

`extern crate minigrep;` は、Cargo が minigrep クレートをビルドするために必要です。

`use minigrep::Config;` は、minigrep クレートの Config 型を使用するために必要です。

→ `extern crate minigrep` の書き方は古い、不要

# 12.4 TDD

失敗するテストを書き、走らせて想定通りの理由で失敗することを確かめる。
十分な量のコードを書くか変更して新しいテストを通過するようにする。
追加または変更したばかりのコードをリファクタリングし、テストが通り続けることを確認する。
手順1から繰り返す！


## ライフタイム注釈


```rust
pub fn search<'a>(query: &str, contents: &'a str) -> Vec<&'a str> {
    vec![]
}
```

明示的なライフタイムの'aがsearchのシグニチャで定義され、contents引数と戻り値で使用されていることに注目してください。 第10章からライフタイム仮引数は、どの実引数のライフタイムが戻り値のライフタイムに関連づけられているかを指定することを思い出してください。 この場合、返却されるベクタは、 (query引数ではなく)contents引数のスライスを参照する文字列スライスを含むべきと示唆しています。

言い換えると、コンパイラにsearch関数に返されるデータは、 search関数にcontents引数で渡されているデータと同期間生きることを教えています。 

# 12.5 Env

## to_lowercase() は3章ではなく新しくメモリを確保する -> String

# 12.6 output error in stderr
