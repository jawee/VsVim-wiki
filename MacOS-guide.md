### Acquisition

Download the extension via the VSMac extension gallery (Visual Studio -> Extensions -> Gallery) and search for VSVim.



### Build instructions


If you want to build from source code instead, then use one of the following two methods.

```sh
git clone https://github.com/VsVim/VsVim.git
cd VsVim
msbuild /p:Configuration=DebugMac /p:Platform="Any CPU" /t:Restore
cd Src/VimMac
msbuild /p:InstallAddin=True
```

or

```sh
git clone --branch vsmac https://github.com/VsVim/VsVim.git && cd VsVim && msbuild /p:Configuration=DebugMac /p:Platform="Any CPU" /t:Restore && cd Src/VimMac && msbuild /p:InstallAddin=True
```

This will build the VsVim extension against the current installation of VSMac.

After running those commands, ensure that the Addin has been loaded into VSMac and is enabled.

<img width="815" alt="image" src="https://user-images.githubusercontent.com/667194/66313771-d42a5680-e90a-11e9-9d00-cb3563ef4a9e.png">

Some control keys used by VsVim conflict with default VSMac keys (`<C-d>` etc). If you want VsVim to use these keys then please select the `Visual Studio + VsVim` keybinding scheme.

<img width="664" alt="image" src="https://user-images.githubusercontent.com/667194/70971779-9cbdf000-2099-11ea-999e-c528f9c026a3.png">


That's it! A restart of VSMac may be needed.

If you like, you may use a `~/.vsvimrc` file to customize the behavior of VsVim. This is mine.

#Example Vim configuration

```vim
set incsearch
set hlsearch
let mapleader=" "
set cursorline
set clipboard=unnamed
set expandtab
set ignorecase
set smartcase
set autoindent
set backspace=indent,eol,start " <-- Needed if you want the backspace key to work like you would expect!
set tabstop=4
set shiftwidth=4
nnoremap <C-p> :vsc MonoDevelop.Ide.Commands.SearchCommands.GotoFile <CR>
nnoremap gu :vsc MonoDevelop.Refactoring.RefactoryCommands.FindReferences <CR>
nnoremap gh :vsc MonoDevelop.Ide.Commands.TextEditorCommands.ShowQuickInfo <CR> " <-- Show tooltip without mouse
nnoremap gb :vsc MonoDevelop.RefactoryCommands.NavigationCommands.FindBaseSymbols <CR>
nnoremap <C-w>o :vsc MonoDevelop.Ide.Commands.FileTabCommands.CloseAllButThis <CR>

" I prefer default VSMac behaviour of navigating between buffers
" when navigating backwards and forwards
nnoremap <C-o> :vsc MonoDevelop.Ide.Commands.NavigationCommands.NavigateBack <CR>
nnoremap <C-i> :vsc MonoDevelop.Ide.Commands.NavigationCommands.NavigateForward <CR>

" Keys copied from SpaceMacs
nnoremap <Space>p :vsc MonoDevelop.Ide.Commands.SearchCommands.GotoFile <CR>
nnoremap <Space>fs :vsc MonoDevelop.Ide.Commands.FileCommands.Save <CR>

nmap gs :vsc VsVim.ShowPadByTitle Solution<CR>

" Emacs keys when in insert mode
inoremap <C-d> MonoDevelop.Ide.Commands.EditCommands.Delete
inoremap <C-a> MonoDevelop.Ide.Commands.TextEditorCommands.LineStart
```


#### Development guide
 If you want to help develop the code, then you will also need to install the AddinMaker extension

<img width="828" alt="image" src="https://user-images.githubusercontent.com/667194/66313143-c45e4280-e909-11e9-8356-91ff8e068e62.png">

This extension adds some IDE support. It takes care of locating VSMac references that are located under `/Applications/Visual Studio.app` and also makes it easy to run any changes (Start Debugging on the VimMac project should launch a new instance of VSMac with any changes to the Extension applied.

<img width="423" alt="image" src="https://user-images.githubusercontent.com/667194/66313484-5bc39580-e90a-11e9-8091-bb75e00f94ae.png">

Please refer to the AddinMaker documentation if you want to target a different version of VSMac than the one that you are currently running.