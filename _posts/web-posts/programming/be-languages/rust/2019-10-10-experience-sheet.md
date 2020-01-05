---
layout: post
title: Rust experience sheet
date:   2019-10-22 08:57:00 +0100
categories: [backend, rust]
tags: [programming, backend, rust, experience-sheet]
---

[_Relevant Post: From Java to Rust_]({% post_url /web-posts/programming/be-languages/rust/2019-10-15-from-java-to-rust %})

Answers to questions I've spent some time looking on the Internet to find an answer to, or which come to be relevant often.

### Compare between String and &str
If we're comparing 2 Strings and _Rust_ shows the error `expected 'String', found '&str'` is because we forgot to add the `.trim()` part to `buffer`.

~~~ rust
let mut buffer = String::new();
io::stdin().lock()
  .read_line(&mut buffer)
  .expect("Couldn't read user input");

if buffer.trim() == "yes" {
  // do action
}  
~~~

<!--more-->

### Parse from &str to i32  
~~~ rust  
let index_str: &str = _matches.value_of("index")
    .unwrap();
let index: i32 = index_str.parse::<i32>()
    .unwrap();
~~~

## Reference(s)  
[https://doc.rust-lang.org/std/](https://doc.rust-lang.org/std/)  
[https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html](https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html)  
[http://danielnill.com/rust_tip_compairing_strings](http://danielnill.com/rust_tip_compairing_strings)  
