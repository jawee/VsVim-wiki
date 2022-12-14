This is a snapshot of the list of supported settings that can be issued as commands or included in the rc file.

Authoritative information can found in the source code for [setting names](https://github.com/jaredpar/VsVim/blob/master/Src/VimCore/VimSettingsInterface.fs) and [their defaults](https://github.com/jaredpar/VsVim/blob/master/Src/VimCore/VimSettings.fs).

For compatibility reasons, if you do not have any rc file, VsVim will prefer settings configured by Visual Studio such as tab and space settings.  However, if you do have an rc file, VsVim will prefer the settings configured in that file or its own vim-compatible defaults (such as tab stops of 8).  To have both an rc file and yet continue to let Visual Studio settings override VsVim settings, use `vsvim_useeditordefaults` (see [Defaults for Settings](Defaults-for-Settings) for more details).

## RC File
Like Vim, VsVim uses an rc file for its settings.  VsVim will check the following candidate rc folders:
* `%HOME%`
* `%HOMEDRIVE%%HOMEPATH%`
* `%VIM%`
* `%USERPROFILE%`

Once it finds a folder, it will check for the following candidate rc files:
* `.vsvimrc`
* `_vsvimrc`
* `.vimrc`
* `_vimrc`

You can use the `set` command (with no arguments) interactively to see what file VsVim found and loaded.

## Settings
If the setting is a toggle, you can use either `set <setting>` or `set no<setting>`, e.g. `set hlsearch` or `set nohlsearch`.  If the setting is a number or a string you can use `set <setting>=<value>`, e.g. `set shiftwidth=4`.  Unless otherwise documented, settings are intended to be compatible with `vim`.

### Global Settings
* `vsvim_autocmd` - toggle - enable running auto commands (also requires `novsvim_useeditordefaults`), see [AutoCmd Support](AutoCmd-support)
* `backspace` - string - [vim documentation](http://vimhelp.appspot.com/options.txt.html#%27backspace%27)
    * `indent` - supported
    * `start` - supported
    * `eol` - supported
* `vsvimcaret` - number - opacity of the caret block from `0` to `100` (higher is more opaque)
* `vsvim_controlchars` - toggle - see [Control Character Display](Control-Character-Display)
* `cdpath` - string
* `clipboard` - string
    * `unnamed`
    * `autoselect`
    * `autoselectml`
* `hlsearch` - toggle
* `history` - number
* `ignorecase` - toggle
* `incsearch` - toggle
* `joinspaces` - toggle
* `keymodel` - string
* `magic` - toggle
* `vsvim_maxmapcount` - number
* `maxmapdepth` - number
* `mousemodel` - string - [vim documentation](http://vimhelp.appspot.com/options.txt.html#%27mousemodel%27), see also [behave](http://vimhelp.appspot.com/gui.txt.html#%3Abehave)
    * `extend` - supported
    * `popup`
    * `popup_setpos`
* `paragraphs` - string
* `path` - string
* `scrolloff` - number
* `sections` - string
* `selection` - string - [vim documentation](http://vimhelp.appspot.com/options.txt.html#%27selection%27), see also [behave](http://vimhelp.appspot.com/gui.txt.html#%3Abehave)
    * `inclusive` - supported
    * `exclusive` - supported
* `selectmode` - string - [vim documentation](http://vimhelp.appspot.com/options.txt.html#%27selectmode%27), see also [behave](http://vimhelp.appspot.com/gui.txt.html#%3Abehave)
    * `mouse` - supported
    * `key` - supported
    * `cmd` - not supported
* `shell` - string
* `shellcmdflag` - string
* `smartcase` - toggle
* `startofline` - toggle
* `tildeop` - toggle
* `ttimeout` - toggle
* `timeout` - toggle
* `timeoutlen` - number
* `ttimeoutlen` - number
* `vsvim_useeditorindent` - toggle
* `vsvim_useeditordefaults` - toggle - prefer editor defaults for options such as `shiftwidth`
* `visualbell` - toggle - [vim documentation](http://vimhelp.appspot.com/options.txt.html#%27visualbell%27)
* `virtualedit` - string - [vim documentation](http://vimhelp.appspot.com/options.txt.html#%27virtualedit%27)
    * `onemore` - supported
* `vimrc` - string
* `vimrcpaths` - string
* `whichwrap` - string - [vim documentation](http://vimhelp.appspot.com/options.txt.html#%27whichwrap%27)
    * `b` - supported
    * `s` - supported
    * `h` - supported
    * `l` - supported
    * `<` - supported
    * `>` - supported
    * `~` - not supported yet
    * `[` - supported
    * `]` - supported
* `wrapscan` - toggle

### Local Settings
* `autoindent` - toggle
* `expandtab` - toggle
* `number` - toggle
* `nrformats` - string
* `shiftwidth` - number
* `tabstop` - number
* `quoteescape` - string

### Window Settings
* `cursorline` - toggle - [vim documentation](http://vimhelp.appspot.com/options.txt.html#%27cursorline%27)
* `scroll` - number
