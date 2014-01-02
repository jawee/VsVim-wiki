This is a snapshot of the list of supported settings that can be issued as commands or included in the rc file.

Authoritative information can found in the source code for [setting names](https://github.com/jaredpar/VsVim/blob/master/Src/VimCore/VimSettingsInterface.fs) and [their defaults](https://github.com/jaredpar/VsVim/blob/master/Src/VimCore/VimSettings.fs).

For compatibility reasons, if you do not have any rc file, VsVim will uses prefer settings configured by Visual Studio such as tab and space settings.  However, if you do have an rc file, VsVim will prefer the settings configured in that file or its own vim-compatible defaults (such as tab stops of 8).  To have both an rc file and yet continue to let Visual Studio settings override VsVim settings, use `vsvim_useeditordefaults` (see [Defaults for Settings](Defaults-for-Settings) for more details).

## RC File
Like Vim, VsVim uses an rc file its settings.  VsVim will check the following candidate rc folders:
* `%HOME%`
* `%HOMEDRIVE%%HOMEPATH%`
* `c:\`

Once it finds a folder, it will check for the following candidate rc files:
* `.vsvimrc`
* `_vsvimrc`
* `.vimrc`
* `_vimrc`

## Settings
If the setting is a toggle, you can use either `set <setting>` or `set no<setting>`, e.g. `set hlsearch` or `set nohlsearch`.  If the setting is a number or a string you can use `set <setting>=<value>`, e.g. `set shiftwidth=4`.  Unless otherwise documented, settings are intended to be compatible with `vim`.


### Global Settings
* `vsvim_autocmd` - toggle - enable running auto commands (also requires `novsvim_useeditordefaults`), see [AutoCmd Support](AutoCmd-support)
* `backspace` - string
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
* `mousemodel` - string
* `paragraphs` - string
* `path` - string
* `scrolloff` - number
* `sections` - string
* `selection` - string
* `selectmode` - string
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
* `visualbell` - toggle
* `virtualedit` - string
* `vimrc` - string
* `vimrcpaths` - string
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
* `cursorline` - toggle
* `scroll` - number
