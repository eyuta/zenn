---
title: "Rust Dojo #01"
emoji: "🦀"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["rust"]
published: true
---

## Rust Dojo #1

[The Rust Programming Language 日本語版](https://doc.rust-jp.rs/book-ja/title-page.html)を中心に進めていく。

### インストール

参考: [インストール - The Rust Programming Language 日本語版](https://doc.rust-jp.rs/book-ja/ch01-01-installation.html)

[Install Rust - Rust Programming Language](https://www.rust-lang.org/tools/install)を参考にする。
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
ファイルを作成後、以下のコードを入力する。

尚、Rust のファイルは`.rs`という拡張子を用いる。
また、単語の区切りには`_`を用いる(ex. `hello_world.rs`)。

```sh
touch main.rs
```

```rs
fn main() {
  // 世界よ、こんにちは
  println!("Hello, world!");
}
```

※`println!`は関数ではなく、[マクロ](https://doc.rust-jp.rs/book-ja/ch19-06-macros.html)と呼ばれるメタプログラミング手法。関数と異なり、コンパイル前に展開される。

コンパイル後にバイナリファイルを実行すると、`Hello World!`が出力される。

```sh
rustc main.rs
./main
# Hello World!
```
