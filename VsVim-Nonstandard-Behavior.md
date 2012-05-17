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