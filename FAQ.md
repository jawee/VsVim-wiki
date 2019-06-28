FAQ 

* [What features are supported?](#what-features-are-supported)
* [What settings are supported?](#what-settings-are-supported)
* [How can I get feature X implemented?](#how-can-i-get-feature-x-implemented)
* [Why don't the copy, paste and cut keystrokes work?](#why-dont-the-copy-paste-and-cut-keystrokes-work)
* [How can I disable autoload of my vimrc?](#how-can-i-disable-autoload-of-my-vimrc)
* [Why can't I backspace in insert mode?](#why-cant-i-backspace-in-insert-mode)
* [Why don't keys like Delete work after uninstall?](#why-dont-keys-like-delete-work-after-uninstall)
* [How can I verify my vimrc is loading?](#how-can-i-verify-my-vimrc-is-loading)
* [How can I temporarily disable VsVim?](#how-can-i-temporarily-disable-vsvim)
* [Where can I get older drops?](#where-can-i-get-older-drops)
* [How can I use Visual Assist and VsVim?](#how-can-i-use-visual-assist-and-vsvim)
* [How can I change the cursor blink rate?](#how-can-i-change-the-cursor-blink-rate)
* [How can I build VsVim myself?](#how-can-i-build-vsvim-myself)
* [How can I install a build with the latest sources?](#how-can-i-install-a-build-with-the-latest-sources)
* [How can I get a build that can run on .NET 4.0?](#how-can-i-get-a-build-that-can-run-on-net-40)
* [Why can't I install VsVim on VS 2010?](#why-cant-i-install-vsvim-on-vs2010)

### What features are supported?

Quite a few and more are being added all the time.  See [[Supported Features|Supported-Features]] for more details.

### What settings are supported?

Hopefully, your favorite vim settings are supported.  Check [[Settings Reference|Settings-Reference]] to find out.

### How can I get feature X implemented?

Please file an issue on GitHub requesting this feature.  Issues are the primary way I track both bugs and feature requests.  

### Why don't the copy, paste and cut keystrokes work?

All of these commands are implemented but are not enabled by default.  These are command keys which have very specific meaning in Windows and their usage is classified as advanced so VsVim won't unbind them by default.  To enable these commands manually switch them to VsVim in the conflicting key bindings dialog. 

If you'd like to have the VsVim handle Ctrl-V, Ctrl-C, etc and still get the typical Windows behavior, see [these instructions](https://github.com/jaredpar/VsVim/wiki/VsVim-Nonstandard-Behavior#wiki-clipboard) on the [VsVim Nonstandard Behavior](https://github.com/jaredpar/VsVim/wiki/VsVim-Nonstandard-Behavior) page.

Note: Ctrl-A and Ctrl-X aren't available until 1.1

### Why can't I backspace in insert mode?

VsVim implements the Vim `backspace` setting.  The default value for this setting doesn't allow backspace at the start of insert mode.  If you have a vimrc file VsVim will respect this setting and behave as Vim would.  To change this behavior add the following to your vimrc file 

```
set backspace=indent,eol,start
```

### How can I disable autoload of my vimrc?

Note: This entry won't be relevant until 1.7.0 is released

By default VsVim will load the same _vimrc file that gVim would load.  To disable this behavior do the following

- Tools -> Options 
- VsVim -> Defaults
- Change "VimRc File Loading" to "vsvimrc only" or "None"

### Why don't keys like Delete work after uninstall?

Visual Studio by default contains a lot of key bindings which interfere with VsVim's ability to be a proper emulation of Vim.  As such on start up it will detect any key bindings which conflict and prompt the user to remove them.  These are not reset when VsVim is uninstalled.

There are two options for restoring the settings.  The first is to use the Vim Options page (accessible via the Options button on the margin).  From here you can reset the key bindings back to their original state.  

The other method is to reset your current profile.  This is much more impactful though and will have the effect of resetting other settings.  

> Tools -> Options -> Import / Export Settings

### How can I verify my vimrc is loading?

There are 2 non-standard vim settings that can be used to diagnose potential .vimrc load issues

* vimrc - This setting will display the full path of the file which was loaded for the .vimrc
* vimrcpaths - This setting will display the files and paths searched for .vimrc 

By default VsVim will look for a file named .vsvimrc, _vsvimrc, .vimrc or _vimrc file in the paths %HOME%, %VIM% and %USERPROFILE%

As of now the commands supported in the .vimrc file are limited to those supported in command mode.  

### How can I temporarily disable VsVim?

VsVim can be temporary disabled by the key sequence <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>F12</kbd> and re-enabled later by the same key sequence.  While disabled VsVim will not interfere with any keyboard or selection allowing you to use Visual Studio as if VsVim wasn't installed.

If the shortcut is not working for you, it is possible the key combination is bound to another command. To see which command is conflicting so that you can reassign/remove the binding:

- Go to Tools -> Options -> Environment -> Keyboard.
- In the "Press shortcut keys" field, press <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>F12</kbd>
- Check the "Shortcut currently used by" field, copy the name.
- Paste the command name into the "Show commands containing" field to filter the list of commands.
- Remove or reassign the key binding from the command.

### Where can I get older drops?

Older versions of VsVim are available in the [VsVim Drops](https://www.dropbox.com/sh/pqxkvemji983alf/kZ3a2dUplB) folder on DropBox.

### How can I use Visual Assist and VsVim?

Recent versions of Visual Assist are compatible with VsVim.  If you are seeing any issues then make sure that the following registry value has a value of 1.  This is the default so not seeing the setting means that it's OK.

* VS2010: HKCU\Software\Whole Tomato\Visual Assist X\VANet10\TrackCaretVisibility
* VS2012: HKCU\Software\Whole Tomato\Visual Assist X\VANet11\TrackCaretVisibility

### How can I change the cursor blink rate?

VsVim obeys your operating system cursor blink rate preferences.  If you don't like it, set it to none in:

```
Control Panel -> Keyboard -> Cursor blink rate
```

### How can I build VsVim myself?

See [[Build Environment|Build-Environment]] for details.

### How can I install a build with the latest sources?

Every commit in VsVim will upload a new build to the [Open VSIX Gallery](http://vsixgallery.com) (search for [VsVim](http://vsixgallery.com/extension/VsVim.Microsoft.e214908b-0458-4ae2-a583-4310f29687c3/).  If there is a bug fix or patch which isn't on the official [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=JaredParMSFT.VsVim) yet, you can just install the latest VsVim build from here until it makes it into the official release. The instructions for using this as a VSIX source are [documented here](http://vsixgallery.com/guide/feed/)


### How can I get a build that can run on .NET 4.0?

Starting with version 2.2 VsVim will require .NET 4.5 to run.  This could negatively impact developers who are running on Visual Studio 2010 as it has a minimum runtime requirement of 4.0.  This version of the runtime is no longer supported but it's possible it is still used.  

If that is the case you can install the final 2.1 build which runs on 4.0:

> [VsVim 2.1.1.0](https://vsvim.blob.core.windows.net/drops/VsVim-2.1.1.0.vsix)

### Why can't I install VsVim on VS2010? 

Changes to the VSIX manifest format in VS 2017 make it impossible to have a single VSIX that supports VS 2010 - 2017.  Instead I can only support VS 2012 - 2017 in that manner.  As such I had to drop support for VS 2010 from the main project.  

VS 2010 developers can still use VsVim by installing the "VsVim 2010" extension.  This is VsVim as of 2.2.0 that specifically targets VS 2010.  



