---
title: "Vim Series (Day 02): Editing"
date: 2022-08-29T11:30:29-05:00
description: "The 2nd part of the vim series"
author: "Kyle Weise"
draft: false 
type: "post"
showTableOfContents: true
tags: ["Vi", "Vim", "Neovim", "Series", "Text Editor"]
---

![Editing Logo](/images/posts/series/vim/day-02/cover.png)

## Introduction

Welcome back to the Vim Series! In this post, we will be looking at how to increase your editing speed 
from the commands we learned last time. If you haven't checked out the [Vim Series: Movement](https://www.weiseguy.com/posts/vim-series-movement/) 
post, I would recommend you read that before moving on here. With that said, let's get started.

## Editing (Normal Mode)

To increase speed editing, there are a few commands you should try out in **Normal Mode**. Go ahead and try them out in the file 
you used in the previous post.

| Keybinding | Description |
| --- | --- |
| o | Moves cursor down 1 line and enters Insert Mode |
| Shift + O | Moves cursor up 1 line and enters Insert Mode |
| Shift + P | Pastes content in buffer up 1 line |
| a | Append, Enters Insert Mode w/ cursor on the right |
| Shift + A | Enters Insert Mode at the end of the line |
| Shift + I | Enters Insert Mode at the beginning of the line |
| ea | Enters Insert Mode at the end of the word |

## Searching (Command Mode)

When you are using a text editor, it can be very important to be able to search. With vim, this is also the case. Check out the commands below on the 
file you used last time.

| Keybinding | Description |
| --- | --- |
| / | Search for a word |
| n | Cycle through results from search |
| Shift + N | Go back through results from search |
| * | Cycle through results from search | 
| # | Go back through results from search |

## Editing (Visual Mode)

As stated in the previous post, **Visual Mode** is very versatile and with theses commands you can see why. Go ahead and indent some lines and upper case 
some words.

| Keybinding | Description |
| --- | --- |
| > | Moves text to the right |
| < | Moves text to the left |
| ~ | Switch case of character |
| u | Switch text to lower case | 
| Shift + U | Switch text to upper case |

## Wrapping it up

Congrats, you have just finished the second post of the Vim Series. Again, thanks for reading and I hope this was helpful. If you haven't checked out the 
first post on [Movements](https://www.weiseguy.com/posts/vim-series-movement) please do so. Next post we will go over single-line movements. See ya next time! 

