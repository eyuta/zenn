---
title: "Rust Dojo #01"
emoji: "🦀"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rust"]
published: true
---

## Rust Dojo #01

### はじめに

社内で Rust Dojo を行ったので、内容をメモしていく。
教材は[Rust By Example 日本語版](https://doc.rust-jp.rs/rust-by-example-ja/index.html)を中心に進めていく。

`#01` の内容は以下の通り

- [Rust Dojo #01](#rust-dojo-01)
  - [はじめに](#はじめに)
  - [インストール](#インストール)
  - [Hello World](#hello-world)
    - [演習](#演習)
  - [コメント](#コメント)
    - [通常のコメント (Non-doc comments)](#通常のコメント-non-doc-comments)
    - [ドキュメンテーションコメント (Doc comments)](#ドキュメンテーションコメント-doc-comments)

### インストール

参考: [インストール - The Rust Programming Language 日本語版](https://doc.rust-jp.rs/book-ja/ch01-01-installation.html)

wsl の場合、以下のコマンドを実行する。

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
# Rust is installed now. Great!

# To get started you may need to restart your current shell.
# This would reload your PATH environment variable to include
# Cargo's bin directory ($HOME/.cargo/bin).

# To configure your current shell, run:
# source $HOME/.cargo/env
source $HOME/.cargo/env
```

インストール完了!
以下のコマンドでインストールされたツールを確認できる。

```sh
rustc --version
# rustc 1.53.0 (53cb7b09b 2021-06-17)
cargo --version
# cargo 1.53.0 (4369396ce 2021-04-27)
rustup --version
# rustup 1.24.3 (ce5817a94 2021-05-31)
# info: This is the version for the rustup toolchain manager, not the rustc compiler.
# info: The currently active `rustc` version is `rustc 1.53.0 (53cb7b09b 2021-06-17)`

```

### Hello World

参考: [Hello, World! - The Rust Programming Language 日本語版](https://doc.rust-jp.rs/book-ja/ch01-02-hello-world.html)

ソース: <https://github.com/eyuta/the-rust-programming-language/blob/01__hello_world/hello.rs>

ファイルを作成後、以下のコードを入力する。

尚、Rust のファイルは`.rs`という拡張子を用いる。
また、単語の区切りには`_`を用いる(ex. `hello_world.rs`)。

```sh
touch hello.rs
```

```rs
// This is a comment, and is ignored by the compiler
// You can test this code by clicking the "Run" button over there ->
// or if you prefer to use your keyboard, you can use the "Ctrl + Enter" shortcut
// これはコメントです。コンパイラによって無視されます。
// 右にある「Run」ボタンからこのコードをテストできます。
// キーボードを使いたければ「Ctrl + Enter」もOKです。

// This code is editable, feel free to hack it!
// You can always return to the original code by clicking the "Reset" button ->
// このコードは編集可能です。ぜひハックしてみましょう！
// 「Reset」ボタンでいつでも元のコードに戻すことができます ->

// This is the main function
// main関数です
fn main() {
    // Statements here are executed when the compiled binary is called
    // コンパイルされたバイナリが実行されるとこの関数が呼び出されます

    // Print text to the console
    // コンソールに文字列を出力する
    println!("Hello World!");
}
```

※`println!`は関数ではなく、[マクロ](https://doc.rust-jp.rs/book-ja/ch19-06-macros.html)と呼ばれるメタプログラミング手法。関数と異なり、コンパイル前に展開される。

コンパイル後にバイナリファイルを実行すると、`Hello World!`が出力される。

```sh
rustc hello.rs
./hello
# Hello World!
```

#### 演習

> 上に書いている'Run'をクリックしてアウトプットを見てみましょう。 次に、println!マクロをもう一行追加してアウトプットがどうなるか見てみましょう。
>
> ```txt
> Hello World!
> I'm a Rustacean!
> ```

最後の行に `println!("I'm a Rustacean!")`を加える。

```sh
rustc hello.rs && ./hello
# Hello World!
# I'm a Rustacean!
```

因みに、Rustacean とは Rust 使いのこと(Python 使いを Pythonista と呼ぶのと同様)。
以下によると、`Rustacean`は`Crustacean`(甲殻類)が由来とのこと。
参考: <https://mobile.twitter.com/rustlang/status/916284650674323457>

### コメント

参考:

- [コメント - Rust By Example 日本語版](https://doc.rust-jp.rs/rust-by-example-ja/hello/comment.html)
- [Comments - The Rust Reference](https://doc.rust-lang.org/reference/comments.html)

ソース: <https://github.com/eyuta/the-rust-programming-language/blob/02__comments/hello.rs>

コメントには以下の 2 種類がある

#### 通常のコメント (Non-doc comments)

C++スタイルのコメント。
コンパイル時に空白として解釈される。

- `//` Line comments. 行末までコメントアウト
- `/*` Block comment.ブロックによって囲まれた部分をコメントアウト `*/`

#### ドキュメンテーションコメント (Doc comments)

以下の形式のコメントはドキュメンテーションコメントであり、[doc attribute](https://doc.rust-lang.org/rustdoc/the-doc-attribute.html)のシンタックスシュガーとして解釈される。
`rustdoc`コマンドでドキュメントを生成する際に使用される。

- Outer doc
  - このコメントの後続の内容に関するドキュメント。以下の 2 種類がある
    - `///` Outer line doc.
    - `/**` Outer block doc. `*/`
- Inner doc
  - このコメントの親の内容に関するドキュメント。以下の 2 種類がある
    - `//!` Inner line doc.
    - `/*!` Inner block doc. `*/`

ドキュメントに関する詳細は[こちら](https://doc.rust-jp.rs/rust-by-example-ja/meta/doc.html)

試しにドキュメントを作成してみる。

```sh
touch documents.rs
```

ソースコードは[こちら](https://doc.rust-lang.org/reference/comments.html#examples)を活用した。

```rs

//! A doc comment that applies to the implicit anonymous module of this crate
/// Outer line doc
pub mod outer_module {

  //!  - Inner line doc
  //!! - Still an inner line doc (but with a bang at the beginning)

  /*!  - Inner block doc */
  /*!! - Still an inner block doc (but with a bang at the beginning) */

  //   - Only a comment
  ///  - Outer line doc (exactly 3 slashes)
  //// - Only a comment

  /*   - Only a comment */
  /**  - Outer block doc (exactly) 2 asterisks */
  /*** - Only a comment */

  pub mod inner_module {}

  pub mod nested_comments {
      /* In Rust /* we can /* nest comments */ */ */

      // All three types of block comments can contain or be nested inside
      // any other type:

      /*   /* */  /** */  /*! */  */
      /*!  /* */  /** */  /*! */  */
      /**  /* */  /** */  /*! */  */
      pub mod dummy_item {}
  }

  pub mod degenerate_cases {
      // empty inner line doc
      //!

      // empty inner block doc
      /*!*/

      // empty line comment
      //

      // empty outer line doc
      ///

      // empty block comment
      /**/

      pub mod dummy_item {}

      // empty 2-asterisk block isn't a doc block, it is a block comment
      /***/

  }

  /* The next one isn't allowed because outer doc comments
     require an item that will receive the doc */

  /// Where is my item?
mod boo {}
}

```

ドキュメントを生成する。

```sh
rustdoc documents.rs
# /doc/ が作成される
```

`/doc/documents/index.html`をブラウザで開くと、以下のように表示されるのが確認できる。

![the-rust-programming-language__01_01.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/110860/c52ceb0b-7608-9aa2-4f2c-68bb56009dce.png)

`outer_module`をクリックすると、モジュール(`mod`)の中身を表示できる。

![the-rust-programming-language__01_02.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/110860/f140bf73-1eaf-172b-e161-b1d09ed37b31.png)
