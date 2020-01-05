---
layout: post
title: Rust installation
date:   2019-10-09 11:57:00 +0100
categories: [backend, rust]
tags: [programming, backend, rust, how-to-install]
---

## Installing Rustup  
~~~ bash
curl https://sh.rustup.rs -sSf | sh
~~~
~~~ bash
vim ~/.zshrc
# add following line  
export PATH=$PATH:/home/msanchez/.cargo/bin
source ~/.zshrc
~~~

<!--more-->

## IDE  
I use _PyCharm_ from _Jetbrains_. There's a plugin to do it compatible with _Rust_.

## Hello World
Create a new file, on rust composed words are marked with underscore as `hello_world.rs`  

~~~ rust
fn main() {
  println!("hello world");
}
~~~

Compile it into binaries `rustc hello_world.rs`  
Execute the binaries `./hello_world`

## Reference(s)  
[https://doc.rust-lang.org/book/ch01-01-installation.html](https://doc.rust-lang.org/book/ch01-01-installation.html)  
[https://doc.rust-lang.org/book/ch12-00-an-io-project.html](https://doc.rust-lang.org/book/ch12-00-an-io-project.html)
