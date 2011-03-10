## VimRc Behavior

In order to allow developers to have different settings for VsVim it prefers vimrc files in a different order.  It will look for the following files in the listed order

* .vsvimrc
* _vsvimrc
* .vimrc
* _vimrc

VsVim will look for these files in the following directories: %HOME%, %VIM% and %USERPROFILE%

## Tabs

By default VsVim will prefer Visual Studio specified tab settings over Vim tab settings.  This affects 'et' and 'tabstop'.  If you would prefer VsVim ignore Visual Studio tab settings and instead use 'et' and 'tabstop' then use the following command.

> set novsvim_useeditortabsettings

## Identation

By default VsVim will prefer Visual Studio indentation logic over that specified by standard Vim autoindent behavior.  This can be disabled by the following command

> set novsvim_useeditorindent



