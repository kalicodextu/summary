# ==Summary==

## 1. vim 
### Build Development Environment
* theme
* font color, font size
* virtual venv

### Basic Content	
* __Two Basic Modes__
		* Normal mode
		*In Normal mode the charactors that you type are commands.*
		* Insert mode
		*In Insert mode the  charactors are inserted as text.*

* __Basic Operator__
	* Inserting Text
		* i
		*switch to Insert mode, befor the cursor.*
		* a
		*switch to Insert mode, after the cursor.*
		* <ESC\>
		*switch to Numal mode*
	
	* Basic Moving
		* h ←
		* j ↓
		* k ↑
		* l  →
		
	* Deleting Charactors
		* x
		*delete a charactor.*
		* dd
		*delete a whole line.*
		
	* Undo and Redo
		* u
		*undoes the last edit*
		* CTRL-R
		*to reverse the preceding command*
		
	* Other Editing Commamd
		* i
		*insert*
		* a
		*append*
		* o
		*create a new, empty line below the cursor and put vim in Insert mode.*
		* O
		*open a line above the cursor.*
	
	* Getting out
		* ZZ
		*write the files and exit.*
		* q!
		*quit-and-throw-things-away.*
		* e!
		*reload the original version of the file.* 
		
	
* __Moving Around__	
	* Word Movement
		* (N)w 
		*move the cusor forward the start of N's word.*
		* (N)b
		*move backword to the start of the previous Ｎ'S word.*
		* (N)e
		*move to the next end of N's word*
		* (N)ge
		*move to the previous end of N's word*
		**Note:**
		> A word ends at a non-word character, such as a ".", "_" or  ")", use:
		W, B, E, gE
		
	* Start or End of Line Movement
		* $
		*move the cursor to the end of line.*
		* g_
		*move the cursor to the last non-blank charactor of line.*
		* 0
		*move the cursor to the vey first charactor of the line.*
		* ^
		*move the cursor to the first non-blank charactor of the line.*
		
	* Charactor Movement
		* (N)f(charactor)
		*search forward  in the line for the N's single charactor, and the cursor move to the charactor.*
		* (N)F(charactor)
		*search to the left.*
		* (N)t(charactor)
		*search forward  in the line for the N's single charactor, and the cursor move to a charactor before the charactor.*
		* (N)T(charactor)
		*search to the left.*
		
	* Parenthesis Matching
	*% can work for (), [], {} pairs.*
	
	* Line Movement
		* :N or NG
		*move to the start of N's line.*
		* gg
		*move to the start of first line.*
		* G
		*move to the start of last line.*
		* N%
		*move  to the line N%. 
		eg: 50% move to halfway line of the file*
	
	* Telling Where You Are
		* CTRL-G
		* :set number (display the line numer)
		* :set ruler
	
	* Scrolling Around
		* CTRL-U
		*scroll down half a screen of text.*
		* CTRL-D
		*move the viewing window down half a screen in the file.*
		* CTRL-E
		*scroll up one line*
		* CTRL-Y
		*scroll down one line*
		* CTRL-F
		* scroll forward by a whole screen.*
		* CTRL-B
		*scroll backward by whole screen.*
		* zz
		*Move the file so that the cursor is in the middle of the screen.*
		* zt
		*put the cursor line at  the top.*
		* zb
		*put the cursor line at the bottom.*
	
	* Simple Searches
		* /string
		*find the first string after the cursor.*
		* ?srting
		*find the first string before the cursor.*
		
	* Using Marks
		* ``
		*jump back*

		
## 2. PEP 333 WSGI
* 
