### Building

1. Install the Visual SDK for your Visual Studio Version:
    * [Visual Studio 2010 SDK](http://www.microsoft.com/en-us/download/details.aspx?id=2680)
    * [Visual Studio 2012 SDK](http://www.microsoft.com/en-us/download/details.aspx?id=30668)
    * [Visual Studio 2013 SDK](http://www.microsoft.com/en-us/download/details.aspx?id=40758)
2. Open the Solution `VsVim.sln`
3. Build

### Solutions

* `VimCore.sln` - the part of VsVim that doesn't depend on the full Visual Studio environment
* `VsVim.sln` - builds the VsVim Visual Studio extension
* `VimAll.sln` - like `VsVim.sln` but includes VimApp which isolates VsVim into a standalone application

### Debugging

The extension solutions are set up to debug the VsVim that is built inside an experimental instance of Visual Studio.  The experimental instance can (and should) have different extensions installed that your primary Visual Studio instance.  The fewer the better!

Core editor feature development and testing is made faster and easier by using the VimApp standalone application.  The whole of Visual Studio doesn't have to fire up, breakpoints are reached sooner, etc.

### Installing

To install the version you built into your "normal" instance of Visual Studio:

* remove any previous version of VsVim using Tools -> Extensions and Updates...
* close Visual Studio
* double-click, e.g., the file `Src\VsVim\bin\Release\VsVim.vsix`

Installation of vsix files can also be done manually (assuming the extension is not already installed in a different folder) by simply unzipping the vsix file into any folder under, e.g., `%LOCALAPPDATA%\Microsoft\VisualStudio\11.0\Extensions` and deleting the corresponding cache file, e.g., `%LOCALAPPDATA%\Microsoft\VisualStudio\11.0\Extensions\extensions.en-US.cache`.  If this approach is used, the first time it is installed this way it will be disabled but can be enabled using the extension manager.

### Branching Structure

* master: Stable branch 
* staging: Used for releasing new versions
* fixes*: Both short and long term fixes
* dead*: Branches which will never integrate with master again.  
