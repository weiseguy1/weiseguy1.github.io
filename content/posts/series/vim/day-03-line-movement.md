---
title: "Vim Day 03: Line Movement"
date: 2022-09-07T09:41:46-05:00
description: "The 3rd part of the vim series"
author: "Kyle Weise"
draft: false
type: "post"
showTableOfContents: true
tags: ["Vi", "Vim", "Neovim", "Series", "Text Editor"]
---

![Line Movement Logo](/images/posts/series/vim/day-03/cover.png)

## Introduction

Hello everyone and welcome back to the Vim Series! In this post we will be covering more advanced movements
in vim. These include:
- Horizontal movements, making editing a single line a snap
- Vertical Movements, allowing you to traverse a document with ease
- Combos, putting together the knowledge you know to allow for more powerful commands. 

These commands will help aid you with the movements you already know and allow you to become more 
proficient in vim. Go ahead and try this commands on the text file you have been using in this series.

## Movement (Horizontal)

| Keybinding | Description |
| --- | --- |
| f | Jumps to preceding character |
| t | Jumps to 1 position before preceding character |
| ; | Goes forward to next character |
| , | Goes backwards to previous character |
| x | Deletes character under cursor |
| s | Deletes character under cursor and enters Insert Mode |
| cw | Deletes word and enters Insert Mode |
| ce | Deletes word and enters Insert Mode | 
| Shift + D | Deletes rest of line |
| Shift + C | Deletes rest of line and enters Insert Mode |
| Shift + S | Deletes entire line |

## Movement (Vertical)

| Keybinding | Description |
| --- | --- |
| gg | Go to top of file |
| Shift + G | Go to bottom of file |
| { | Move up 1 paragraph |
| } | Move down 1 paragraph |
| Ctrl + U | Page up through file |
| Ctrl + D | Page down through file | 
| % | Move between match bracket pairs: () [] {} |

## Combos 

Since you have learned a few commands, lets start to understand combos. Like in a video game where 
you can combo certain moves for a more powerful attack, in vim you can combo certain commands to 
fully unlock your text editor. As Ben McCormick stated in the post 
*[Learning Vim in 2014: Vim as a language](https://benmccormick.org/2014/07/02/learning-vim-in-2014-vim-as-language)* on his blog,
> Vim doesn’t speak English, but it has a language of its own, built out of composable commands, 
that is much more efficient than the simple movement and editing commands you’ll find in other editors. 

This means that you can take the commands that you have learned so far and start to place them together. Look at the 
table below for some examples.

| Keybinding | Description |
| --- | --- |
| 10j | Moves the cursor 10 places down |
| 5dd | Deletes the next 5 lines | 
| dt) | Delete everything up to the ending closing brace |
| vf) | Highlight everything before the ending closing brace |
 
Go ahead and with the commands you know so far, come up with 5 different commands to use on the text file you have been using.

## Wrapping it up

So far, if you have been following along, you have learned roughly **60** commands to use in vim!! Congrats! In this blog post alone 
you have learned how to do basic horizontal line movements to make editing a single line in vim extremely efficient. With this knowledge 
you'll now have the respect of your fellow office workers as you fly through documents in a blink of an eye. 

However, if this is the first post of the series you have landed on, please feel free to start with the [basics](/posts/vim/series/basic-movement/) as well
as learning how to [edit](/posts/vim/series/editing/) in vim. With this said, feel free to join me next time as we start to work with buffers and window splitting 
in vim.

## Change Log

- Updated post to include Vertical Movement (09-08-2022) 
