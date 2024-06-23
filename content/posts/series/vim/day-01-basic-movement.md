---
title: "Vim Series (Day 01): Movement"
date: 2022-08-21T13:27:08-05:00
description: "The 1st part of the vim series"
author: "Kyle Weise"
draft: false
type: "post"
showTableOfContents: true
tags: ["Vi", "Vim", "Neovim", "Series", "Text Editor"]
---

![Image Name](/images/posts/series/vim/day-01/cover.png)

## Introduction

Hello everyone and welcome back to my blog. In this series we will be covering the infamous text editor, Vim.
For those that don't know, **Vi IMproved** or Vim is a modal text editor that is made for command line use. This means that 
Vim works by using "Modes" to accomplish certain tasks. There are a total of 5 different modes that Vim has. They are:

- **Normal Mode** - allows for movement from keybindings, (Default Mode).
- **Insert Mode** - allows user to *insert* text into the document.
- **Visual Mode** - allows user to highlight text. This has multiple use-cases.
- **Command Mode** - allows user to execute regex commands, terminal commands and more.
- **Replace Mode** - allows user to replace text, paragraphs, etc.

This first part of the series will cover basics in every mode than a beginners needs to know. 
All you need to follow along is to install vim on your computer, and open a text file by running `vim filename.txt` or 
by running `:vimtutor` when you open vim in your terminal.

It is important to know Vim as you more than likely will be working with servers in a business environment. You might not have a 
choice as to what editor you can use. Vim or is predecessor Vi are usually installed by default on most Unix-like boxes and 
offer many advantages like creating macros or the use of regex in **Command Mode** to help make editing text quick and efficient.
Also, if you enjoy this series you might want to checkout Neovim as an editor of choice as it offers the ability to write configuration
files as well as use plugins written in the Lua programmming language.

## Basics of Vim 

First off, lets start by moving a cursor around the screen. If you ever played a video game that used the ASWD keys, then this should be 
slightly familiar. However, instead of those keys, movement of the cursor is done like so:

### Cursor Movement (Normal Mode)
| keybinding | Description |
| --- | --- |
| h | Move cursor to the left one character |
| j | Move cursor down one line |
| k | Move cursor up one line |
| l | Move cursor to the right one character |
| w | Move cursor to the right by one word | 
| b | Move cursor to the left by one word |

Try this in your file of choice. 

### Basic Editing (Normal Mode)

Now that you are able to move around in your file, lets try to edit it in **Normal Mode**. Use these commands on your file.

| keybinding | Description |
| --- | --- |
| yy | yank (copy) current line into buffer |
| p | paste content of buffer |
| dd | delete (cut) current line into buffer |
| u | undo last command |

### Basic Visual Mode

Visual Mode is used to highlight text in the file. This has many use cases, like indenting curtain lines of text, copying & deleting 
text, and a few other things. To start with, use one of the commands below in conjunction with `y` or `d`.

| keybinding | Description |
| --- | --- |
| v | highlight character under cursor |
| Shift + V | highlight current line |

### Basic Insert Mode

Next, lets enter some text in the file. Use the commands below to work with **Insert Mode**.

| keybinding | Description |
| --- | --- |
| i | Enter Insert Mode |
| esc | Leave Insert Mode |
| Ctrl + i | Leave Insert Mode |
| Ctrl + [ | Leave Insert Mode |

### Basic Replace Mode

There are 2 different ways of working with **Replace Mode**. As you can see below, you can either replace a single character or 
enter **Replace Mode** for a larger replacement of text. While in **Replace Mode** you can replace text just by typing over it.
To leave **Replace Mode**, you can use the same commands to leave **Insert Mode**.

| keybinding | Description |
| --- | --- |
| r | Replace a single character |
| Shift + R | Enter Replace Mode |

Try out **Replace Mode** by entering the sentence below, and replace the name with your own:
```
Hello, my name is Mark.
```

### Basic Command Mode

To work with **Command Mode**, it is pretty easy. Make sure you are in **Normal Mode** to start, then enter a colon `:` and ta-da! 
You are in **Command Mode**. You will need to engage with **Command Mode** to save your documents as well as to do other things, 
like working with regex commands. Try out the commands below on your file.

| keybinding | Description |
| --- | --- |
| :q | Quit file if file was not changed |
| :w | Save file |
| :x | Save and exit file |
| :wq | Save and exit file |
| :q! | Quit and not save file |

## Wrapping it up

You have just completed this post of the Vim series! Hopefully this information was helpful with getting started with vim. If you like this
post then look out for the next post on increasing [editing](https://www.weiseguy.com/posts/vim-series-editing) speed in vim.

## Change Log
- Updated [Wrapping it up](#wrapping-it-up) to link to editing post (08-29-2022)
