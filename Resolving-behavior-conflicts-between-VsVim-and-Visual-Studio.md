**Note! This page applies to VsVim 1.7 and above which is not yet released**

VsVim strives to be as true of a vim emulator as possible while still letting the great features of Visual Studio shine through.  In general these two goals mesh well together but in certain cases there are fundamental differences between vim and Visual Studio that must be resolved.  

* How are new lines indented?
* How is tab / backspace handled in insert mode?
* Which settings are used?

The default for all of these is to use the Visual Studio behavior over the Vim.  This can be toggled through either the options menu (Tools -> Options -> VsVim -> Defaults) or by updating the appropriate setting in the vimrc file (listed below).

## What scenarios are affected? 

### How are new lines indented?
When creating a new line through commands like `o` VsVim must choose a position for the caret.  Vim uses `autoindent` and sometimes `cindent` to choose this value while Visual Studio generally has a language specific mechanism.  By default VsVim uses the language mechanism if it exists and will fall back to `autoindent` if it does not.  

The setting which controls this is `vsvim_useeditorindent`

### How is tab / backspace handled in insert mode? 
The vim handling of tab and backspace in insert mode is governed by a number of settings: `backspace`, `softtabstop`, `tabstop`, `expandtab`, etc ...  This allows for a great deal of behavior customization as best described by this [vim cast](http://vimcasts.org/episodes/tabs-and-spaces/)

Visual Studios handling of tab / backspace is much simpler.  But it's also ingrained into how Visual Studio behaves and often tied to the underlying language service.  By default VsVim will use Visual Studio behavior. 

The setting which controls this is `vsvim_useeditortab`

### Which settings are used? 
Vim and Visual Studio share a number of common settings.  Vim has consistent defaults across its versions but Visual Studio defaults differ between languages and versions (so much fun!)

- `tabstop`: vim = 8, vs = 4
- `shiftwidth`: vim = 8, vs = 4
- `cursorline`: vim = false, vs 2010 = false, vs 2012 = true
- `expandtab`: vim = false, vs = (C# false) (C++ true)
- `number`: vim = false, vs = false

VsVim must choose a winner between these settings and by default it picks Visual Studio as the winner.  Hence values like `tabstop` will be ignored if specified in a vimrc file.  

The setting which controls this is `vsvim_useeditordefaults`

## Why did you pick Visual Studio defaults over Vim? 
I chose Visual Studio behavior as the default winner over vim because it appears to match the expectation of users.  The majority of bug reports / emails I get where there isn't actually a bug occur because of a misunderstanding on how one of the above behavior differences operate.  In nearly every case the user expected Visual Studio behavior not vim.  

## Will vim behavior will suffer quality because it's not the default?
No.  I actually prefer the vim behavior and my setup almost always uses it.  As do a number of the more vocal users of VsVim.  Vim behavior will always be as close to vim as I can make it.  




