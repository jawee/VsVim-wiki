## VimRc Behavior

In order to allow developers to have different settings for VsVim it prefers vimrc files in a different order.  It will look for the following files in the listed order

* .vsvimrc
* _vsvimrc
* .vimrc
* _vimrc

VsVim will look for these files in the following directories: HOME, VIM and USERPROFILE

## Tabs

By default VsVim will prefer Visual Studio specified tab settings over Vim tab settings.  This affects *et* and *tabstop*.  If you would prefer VsVim ignore Visual Studio tab settings and instead use *et* and *tabstop* then use the following command.

    set novsvim_useeditorsettings

## Indentation

By default VsVim will prefer Visual Studio indentation logic over that specified by standard Vim autoindent behavior.  This can be disabled by the following command

    set novsvim_useeditorindent

## Integration with Visual Studio

You can run Visual Studio commands (i.e. the type of commands you would run in the *Command Window*) using `:vsc Command.Name`. For example, to go to the next error (Visual Studio command: *View.NextError*) you would execute: 

    :vsc View.NextError

## Jumps

Vim tracks [jump motion history](http://vimdoc.sourceforge.net/htmldoc/motion.html#jump-motions) per window, whereas Visual Studio tracks it across its entire session. As such, some of the jump motions will behave differently, although not by a significant amount, between Vim and Visual Studio.

Should you find the Visual Studio behavior acceptable, you can map it to the `C-O` and `C-I` normal mode commands:

    nmap <C-O> :vsc View.NavigateBackward<CR>
    nmap <C-I> :vsc View.NavigateForward<CR>


Similarly, Visual Studio's *Go To Definition...* command is a good approximation of the `C-]` [jump to tag definition](http://vimdoc.sourceforge.net/htmldoc/tagsrch.html#CTRL-]) motion:

    nmap <C-]> :vsc Edit.GoToDefinition<CR>

Vim jumps to definition in the current window; if the definition is in another file, Visual Studio will open that file in a separate tab (or activate the tab that contains the file if already open).


