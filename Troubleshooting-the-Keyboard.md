VsVim tries to let you use almost all of vim's standard key bindings.  However, when VsVim is hosted by Visual Studio the keyboard is complicated and things can go awry.

## How It's Supposed to Work

* VsVim detects any key bindings that would conflict with you using it in the editor
* The options dialog displays keys that have conflicts
* For each key, you choose which is less worse: Let Visual Studio handle the key or let VsVim handle the key
* When you let VsVim handle the key, VsVim **unbinds all the conflicting keys** in Visual Studio

## What If I Choose Handled by VsVsim but the key doesn't Work?

It may happen that you are willing to give up other uses of a key and so you choose "Handled by VsVim" but the key still doesn't work.  Let's say the `Ctrl+[` key to go to normal mode isn't working.

### Check VsVim Options

You should see this in VsVim options:

* `Ctrl+[`       Handled by `[VsVim]`

### Check the status bar in the lower left when you type Ctrl+[

If Visual Studio is hanging onto the key because it is the first key in a keyboard shortcut "chord" you will see the following message on the status bar when you type the `Ctrl+[` key:

* (Ctrl+[) was pressed.  Waiting for second key of chord...

If that happens, then for whatever reason Visual Studio still has a multi-key binding that starts with that keystroke even though VsVim tried to unbind it.

### Check Visual Studio Keyboard Bindings

* Tools -> Options
* Environment -> Keyboard
* Navigate to the "Press Shortcut Key" box and type in the `Ctrl+[` sequence

If it is bound to a command it will show up in the drop down just below that dialog.

### Manually Remove All Other Key Bindings for the Keystroke

You may have success with the key in VsVim by manually removing all other uses of that key that VsVim either didn't remove, failed to remove, or appeared with VsVim noticing

### Still Doesn't Work?

Create a [VsVim issue](https://github.com/jaredpar/VsVim/issues) describing your problem.