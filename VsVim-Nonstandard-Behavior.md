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

<a name="clipboard"></a>
## Ctrl-X, Ctrl-C, Ctrl-V

A normal installation on gVim on Windows will not enable the `Ctrl-X`, `Ctrl-C`, `Ctrl-V` shortcuts that typically control clipboard operations on Windows. Indeed, the Vim documentation on [clipboard operations on Windows](http://vimdoc.sourceforge.net/htmldoc/gui_w32.html#gui-clipboard) instructs the user on adding `source $VIMRUNTIME/mswin.vim` to the `_vimrc` file in order to be able to use the standard Windows behavior.

As VsVim tries to stay as close to the default behavior of Vim as possible, there are two ways to handle the `Ctrl-X/C/V` shortcuts:
* Visual Studio handles the `Ctrl-X/C/V` combinations, or,
* Vim handles the `Ctrl-X/C/V` combination and uses mapping directives to mimic the standard Windows behavior.

The downside of choosing *Handled by Visual Studio* in the VsVim option dialog is that VsVim will not exit insert mode when `Ctrl-C` is pressed. Similar restrictions apply to the rest of the commands.

If you choose to have VsVim handle `Ctrl-X/C/V`, you can add the following to the `_vsvimrc` file in order to arrive at a standard Windows behavior:
```vim
" copied from Vim 7.3's mswin.vim:

" CTRL-X and SHIFT-Del are Cut
vnoremap <C-X> "+x
vnoremap <S-Del> "+x

" CTRL-C and CTRL-Insert are Copy
vnoremap <C-C> "+y
vnoremap <C-Insert> "+y

" CTRL-V and SHIFT-Insert are Paste
map <C-V>		"+gP
map <S-Insert>		"+gP
imap <C-V>		<Esc>"+gpa

cmap <C-V>		<C-R>+
cmap <S-Insert>		<C-R>+


imap <S-Insert>		<C-V>
vmap <S-Insert>		<C-V>

" Use CTRL-Q to do what CTRL-V used to do
noremap <C-Q>		<C-V>
```

Here are other entries from the `mswin.vim` file that you can use with VsVim in order to allow all keys to be handled by VsVim:

```vim
" set 'selection', 'selectmode', 'mousemodel' and 'keymodel' for MS-Windows
behave mswin

" backspace and cursor keys wrap to previous/next line
set backspace=indent,eol,start whichwrap+=<,>,[,]

" backspace in Visual mode deletes selection
vnoremap <BS> d

" Use CTRL-S for saving, also in Insert mode
noremap <C-S>		:update<CR>
vnoremap <C-S>		<C-C>:update<CR>
inoremap <C-S>		<C-O>:update<CR>

" CTRL-Z is Undo; not in cmdline though
noremap <C-Z> u
inoremap <C-Z> <C-O>u

" CTRL-Y is Redo (although not repeat); not in cmdline though
noremap <C-Y> <C-R>
inoremap <C-Y> <C-O><C-R>

" CTRL-A is Select all
noremap <C-A> gggH<C-O>G
inoremap <C-A> <C-O>gg<C-O>gH<C-O>G
cnoremap <C-A> <C-C>gggH<C-O>G
onoremap <C-A> <C-C>gggH<C-O>G
snoremap <C-A> <C-C>gggH<C-O>G
xnoremap <C-A> <C-C>ggVG

```
