---
layout: post
title: Vim advanced commands
date:   2019-10-24 07:25:00 +0100
categories: [linux]
tags: [linux, vim]
---

Useful commands to master vim

#### Tips
All delete commands which are run with `d`, may use instead `c`. This will do the same delete operation, but will open directly on _insert mode_ afterwards.

#### Help  
Type `:help change.txt`
#### Redirect input into a Vim buffer
`cat input | vim -` This, ran from bash, outputs the result of a command or a file into a vim buffer, where we can do whatever with it, without modifying the original source.     

<!--more-->

#### Useful vim commands  
All of this are executed in **command mode**.  

`:w filename` - writes the content we are modifying, into another file  
`:%! grep -v delete-this` - the part `:%!` executes bash commands for the content we're modifying. This example will delete all the lines from our file, which contain the String `delete-this`.  

`:set rnu` - see relative line numbers to your caret. `:set rnu!` turns off.  
`:set nu` - see absolute line numbers.  

##### Search something
`f` - find and travel to next ocurrence. For example `f.` searches for the next `.`

`/whatever` - searches for the string in the documment. Forward search  
`?whatever` - reverse search. `n` will now search back  

`shift + n` `n` - go to previous / next match  
`ggn` `Gn` - go to first / last match  
`*` `#` - searches for next / previous ocurrence of current word  

##### Replace something
`:%s/original_string/new_string/gc` - replaces _original_string_ for _new_string_   
`g` is do this for all matches  
`c` is interactive mode  

##### Delete something  
`:-6-4d` deletes from the relative line `-6` to `-4`

`di"` when run inside two `"` it will delete the content between them.  
`dt.` delete from my position until the next `.`  
`df.` delete from my position until, and including, the next `.`

##### Copy and paste  
`:-6,-4co.` copies from the relative lines `-6` to `-4` into your current position    

`shift + v` select whole lines  
`y` / `d` copy / cut  
`P` / `p` paste before / after the cursor

## Reference(s)
[https://www.youtube.com/watch?v=l8iXMgk2nnY](https://www.youtube.com/watch?v=l8iXMgk2nnY)  
[https://www.youtube.com/watch?v=1alWK5ByNMc](https://www.youtube.com/watch?v=1alWK5ByNMc)
