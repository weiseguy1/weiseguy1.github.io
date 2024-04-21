---
title: "Vim Series: Buffers & Splits"
date: 2022-09-08T21:19:20-05:00
description: "The 4th and final part of how to use vim"
author: "Kyle Weise"
draft: false
type: "post"
showTableOfContents: true
tags: ["Vi", "Vim", "Neovim", "Series", "Text Editor"]
---

![Buffers Logo](/images/posts/series/vim/buffers.png)

## Introduction

Hello everyone, and welcome back to the final entry in the vim series. In this post we will be talking 
about buffers, splits and some helpful options in command mode. Now, this information is going to be a 
bit advanced. However, we'll look at this topic in more bite sized chucks to make the content easier to 
understand. With that said let's get started. 

## What are Buffers?

The definition that you need to comprehend is the namesake of this article, *Buffers*. 

*Buffers hold the content read from a file inside a chuck of memory.* 

The allocated chuck of memory is what vim displays in front of you when you open the program. This makes it 
so that if vim were to crash, your original file would be safe from corruption. Another added benefit of opening
files in memory is that multiple splits are able to view that bit of memory at the same time. For more information, 
be sure to check out [Vim Wiki's](https://vim.fandom.com/wiki/Buffers) section on buffers. 

## Playing with Buffers

Now that we have the definition down, we can start playing with buffers. 

| Keybinding | Description |
| --- | --- |
| :e file | Opens a file in another buffer, Default opens current document |
| Ctrl + ^ | Switch between the last opened file |
| Ctrl + o | Go backwards in movement history |
| Ctrl + i | Go forwards in movement history |
| Ctrl + w + v | Open a vertical split |
| Ctrl + w + s | Open a horizontal split |
| Ctrl + w + o | Closes everything but current buffer |
| Ctrl + w + = | Equally spread spacing between splits |
| Shift + H | moves vertical split to horizontal split |

## Using Tabs 

| Keybinding | Description |
| --- | --- |
| :tabedit file | Opens a tab with the name file |
| gt | Move to next tab |
| g + Shift + T | Move to previous tab |
| num + gt | Move to specific number of tab |
| :tabs | List all open tabs |
| :tabsclose | Close a single tab |

## Command Mode

| Keybinding | Description |
| --- | --- |
| :%s/find/replace/ | Find and replace first result |
| :%s/find/replace/g | Find and replace all results |
| :terminal | Opens Terminal Mode |
| :ls | List all open buffers |
| :resize | Resize the amount of rows in a split |
| :vertical resize | Resize the amount of columns in a split |

## Wrapping it up

Well that wraps up the Vim Series! Thank you so much for following along and congrats on reaching 
the finish line. You have learned more that **80** commands in this series. You have gone from 
the very basics to the more advanced movements. If this series has interested you, please fell free 
to check out any of the other posts on my blog.
