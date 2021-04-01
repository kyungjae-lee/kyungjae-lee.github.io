---
layout: notes
title: "[Linux] Useful Command Line Tips and Tricks"
meta: Useful Linux commands, terminal tricks and shortcuts
reference: Shotts, W. (2019). The Linux Command Line. William Pollock.
category: linux
---

## 1. Quick Copy and Paste Trick
If you are using a mouse, 
1. Highlight some text by holding down the left mouse button and dragging the
   mouse over it, or double-clicking a word. (It is copied into a buffer
   maintained by your system.)
2. Press the middle mouse button to paste the text at the cursor location.

## 2. Command Line Editing
### Cursor Movement Commands
- Ctrl + A
	- Move cursor to the beginning of the line.
- Ctrl + E
	- Move cursor to the end of the line.
- Ctrl + F
	- Move cursor forward one character; same as the right arrow key.
- Ctrl + B
	- Move cursor backword one character; same as the left arrow key.
- Alt + F
	- Move cursor forward one word.
- Alt + B
	- Move cursor backword one word.
- Ctrl + F
	- Clear the screen and move the cursor to the top-left corner. The clear
      command does the same thing.
	
### Text Editing Commands
- Ctrl + D
	- Delete the character at the cursor location.
- Ctrl + T
	- Transpose (exchange) the character at the cursor location with the one
      preceding it.
- Alt + T
	- Transpose the word at the cursor location with the one preceding it.
- Alt + L
	- Convert the characters from the cursor location to the end of the word to
      lowercase.
- Alt + U
	- Convert the characters from the cursor location to the end of the word to
      uppercase.

### Cut-and-Paste Commands
- Ctrl + K
    - Kill text from the cursor location to the end of line.
- Ctrl + U
    - Kill text from the cursor location to the beginning of the line.
- Alt + D
    - Kill text from the cursor location to the end of the current word.
- Alt + Backspace
    - Kill text from the cursor location to the beginning of the current word.
      If the cursor is at the beginning of a word, kill the previous word.
- Ctrl + Y
    - Yank text from the kill-ring and insert it at the cursor location.
