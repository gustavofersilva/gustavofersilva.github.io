---
layout: post
title: From Java to Rust
date:   2019-10-21 11:57:00 +0100
categories: [backend, rust]
tags: [programming, backend, rust, from-java-to]
---

[_Relevant Post: Initial Steps with Rust_]({% post_url /web-posts/programming/be-languages/rust/2019-10-09-installation %})

Relevant changes to adapt to [_Rust_](https://doc.rust-lang.org/book/title-page.html), coming from a _Java_ background. Contains information about _Rust's_ environment and the language structures.  

For code snippets on how to do specific things as we do in _Java_, [_check my Rust experience post_]({% post_url /web-posts/programming/be-languages/rust/2019-10-10-experience-sheet %})  

# Rust Environment
## Cargo
[_Cargo_](https://doc.rust-lang.org/cargo/index.html) is _Rust's_ dependencies manager and most projects should be created and managed with it, for easier use.  
Commands I used so far:  

`cargo new hello_cargo` creates a new project.  
_Cargo.toml_ is a file which cargo creates and it contains the project's metainformation and its dependencies.  

`cargo build` builds binaries from source code.    
`cargo run` directly compiles and starts the programm.  

`cargo install --path .` installs from binaries to your system. Useful to use and test my own programs.  
`--force` needed if it already was installed

<!--more-->

### Dependencies  
#### Add new dependency
Just open the file _Cargo.toml_ and add the name under `[Dependencies]`. This adds _Randoms v0.3.14_ into the build.  

~~~
[dependencies]
rand = "0.3.14"
~~~

# Language Structures
## Variables
### Create a variable  
In _Rust_, variables are **inmutable** by default. `mut` allows them to be mutable.  
Several words-variables are separated by underscore.

~~~ rust
// new() is a static method from String
let your_guess: String = String::new();
let mut another_guess: String = String::new();
~~~

### Shadowing a variable  
This is often used to reuse the name of a variable, when we want to change its type without needing to have 2 separated variables, one as `my_var` and another as `my_var_str`.  

~~~ rust
let x = 5;  
let x = x + 1;
println!("the value of x is: {}", x); // 6
~~~

### References
_(Check code! Change it to a simpler example)._  

`&` indicates that this argument is a _reference_. This is a way to access a piece of data, without needing to copy it into memory multiple times. Like _variables_, _references_ are inmutable by default. To do it _mutable_ we'd to write `&mut guess`.

~~~ rust
let mut guess: String = String::new();
io::stdin().read_line(&mut guess)
  .expect("bla");
~~~

### Constants
They are declared with `const` instead of `let`. They have to be a literal and may not be the result of a function.  

~~~ rust  
const MAX_POINTS: u32 = 100_000;
~~~

The main difference of _mutables_ vs _shadowing_ is with the former, we may change the variable type, as we're creating a new one with the keyword `let`.

## Functions
### Template  
Is it possible to return sooner than at the end of the function with the keyword `return`, most functions should return the last _expression_ implicitly though.

~~~ rust  
fn main() {
  let x = plus_one(5);
  // do something with x
}

fn plus_one(x: i32) -> i32 {
  x + 1 // this is an statement
}
~~~

### Statements vs Expressions
_Statements_ are instructions that perform some action and do not return a value.  
_Expressions_ evaluate to a resulting value. An example of this is the block we use to create new scopes `{}`.

~~~ rust
fn main() {
  let x = 3; // this is an statement.  

  // this whole block between {} is an expression
  let y = {
    let x = 6; // this is valid only at this scope
    x + 2 // notice there is no semicolon
  }

  println!("x is {} and y is {}", x, y);
  // will print the values 3 and 8
}
~~~

## Control Structures  
### if as a let statement  
Because `if` is an _expression_, we can use it to the right of a _statement_.  

~~~ rust  
let condition = true;  
// both have to be of the same type.
let number = if condition {
  5
} else {
  6
};
~~~

### loop
This creates an infinite loop, which stops with `break`. It's also possible to directly return a value for a _statement_. _Rust_ also has a `while` loop.  

~~~ rust  
let mut counter = 0;
let result = loop {
  counter += 1;

  if counter == 10 {
    break counter * 2;
  }
};
println!("The result is {}", result); // 20
~~~

#### for .. in
~~~ rust
for number in (1..4) {
  println!("{}", number);
}
~~~

## Error Handling  
### Crash on Error
~~~ rust
let mut guess: String = String::new();
io::stdin()
    .read_line(&mut guess)
    .expect("oh no!");
~~~

### Handling an error
Switching from `expect` to a `match` expression is generally how an error is handled.  

The method `.parse()` returns a `Result` type, which is an Enum with the variants `Ok` and `Err`. We use `match` to compare against this `Result`.

~~~ rust
loop {
  // ...
  let guess: u32 = match guess.trim()
    .parse() {
      Ok(num) => num,
      Err(_) => continue,
    }
}
~~~  

The underscore `_` here is a _catchall_ value. In this example, it means we want to catch all `Err` values, no matter the information inside them.  

## Original Reference(s)  
_(I'm slowly following all chapters here + own learn by doing)_  
[https://doc.rust-lang.org/book/ch01-00-getting-started.html](https://doc.rust-lang.org/book/ch01-00-getting-started.html)
