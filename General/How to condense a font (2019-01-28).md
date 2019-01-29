<div style="font-size:1rem;font-family:Verdana, sans-serif">
# How to condense a font

If you want to display more source code text in a limited window, you can:
1. Use a proportional font.
2. And/or condense horizontally your favourite font.

Let's compare three fonts displaying the same source code text:

<img src="How to condense a font - fonts anim.gif" style="width:40rem;max-width:100%" alt="" >

## FontForge (GPL)

[FontForge](https://github.com/fontforge/fontforge/releases) is an open-source visual font editor.

Here is the procedure to reduce the width of a font:
- Run FontForge.
- In the favourite directories list, choose `C:\Windows\fonts` (if you are on Windows).
- Select the font to be used as a base.  
Example: _verdana.ttf_.
- _OK_.
- Menu _Edit_ / _Select_ / _Select all_ (Ctrl+A).
- Menu _Element_ / _Transformations_ / _Transform_ (Ctrl+\\).
   - _Center of selection_ (can be named _Origin_ too) : _Glyph's origin_.
   - _Move_ : _Scale_.
      - _H_ : 90 %.
	  - _V_ : 100 %.
   - Check _Transform all layers_ (can be named _Transform background_ too).
   - **Un**check _Round to int_.
   - _OK_.
-  Wait for the generation process.
   - Some warnings may appear. Just ignore them.
- Menu _Element_ / _Font info_ (Ctrl+Shift+F).
- Section _Postscript names_ (can be just named _Names_).
	- Modify the three names.  
	Please note some of them do not accept spaces.
	- _OK_.
- Accept the generation of a new identifier.
- Menu _File_ / _Generate fonts_ (Ctrl+Shift+G).
	- Be sure the selected type is _TrueType_.
	- Uncheck _Validate before saving_.
	- Select a directory, not _fonts_ because you need write access rights.
	- _Generate_ (can be named _Save_ too).
- Close FontForge.
	- You probably do not need to save the project file _untitled.sfd_.  
It is not necessary anyway.

Open your favourite file manager, then:
- Open the directory where you saved your font.
- Open the font.
- On Windows, the font manager displays your font and gives you the opportunity to install it so it is available to all software (admin rights may be needed).

Of course, I can't distribute the fonts I modified since I don't have rights on them.  
But now you can tune fonts by yourself.  
Enjoy !

## Proportional fonts for programming

By the way, you may have noticed I personally use a proportional font for programming, in that instance a condensed version of _Verdana_.  
The reasons are:
- Fixed-width fonts usually display less text than proportional fonts.  
Of course, when a 'i' is as wide as a 'X', sure we waste some surface.
- Fixed-width fonts are less readable.  
Mainly because they are inconsistent with usual fonts such as the GUI, word processors and Web fonts, and in fact the real world fonts.  
Naturally, our brain needs time and efforts in order to adapt to new fonts, new character sizes, new colors, etc.
- Verdana has something most other proportional fonts doesn't have: it differentiates upper '**I**' and lower '**l**'.  
Very important when many names begin with a **I**, such as _Interface_.
- I simply consider fixed-size fonts as prehistoric antiquities.  
They should not have survived to typewriters.

---
N.B. The color theme visible on the screen shots is available on [Notepad++](https://github.com/ChrisBertrandDotNet/Programming-in-blue/tree/master/Notepad%2B%2B) and on [Visual Studio](https://github.com/ChrisBertrandDotNet/Programming-in-blue/tree/master/Visual%20Studio).

</div>