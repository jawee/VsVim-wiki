VsVim tries to let you use almost all of vim's standard key bindings.  However, when VsVim is hosted by Visual Studio the keyboard is complicated and things can go awry.

## How It's Supposed to Work

* VsVim detects any key bindings that would conflict with it being able to use it in the editor
* The options dialog displays keys that have conflicts
* For each key, you choose which is less worse: Let Visual Studio handle the key or let VsVim handle the key
* When you let VsVim handle the key, VsVim **unbinds all the conflicting keys** in Visual Studio
