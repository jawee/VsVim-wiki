# Release Notes

### Version 1.3.1
https://github.com/jaredpar/VsVim/issues?milestone=27&page=1&state=closed

Primary Issues Addressed
* Non-English keyboard handling 
* More key mapping fixes 
* VS 2012 fixes 

### Version 1.3.0
https://github.com/jaredpar/VsVim/issues?milestone=23&state=closed

Primary Issues Addressed
* Key Handling
  * Number pad keys now act as their equivalent 
  * Multiple key mapping fixes 
* Better Visual Assist Support
* Mindscape Support
* Bugs present in Dev11 only installations
* C# event handler pattern '+=' doesn't go to Visual Mode
* Select Mode 

Patched Issues (1.3.0.2)
* Select mode deletion added an unprintable character 
* Macro playback failed when SpecFlow was also installed
* The `gk` command caused a down movement when word wrap was disabled
* Exception on startup 
* Certain key mappings not working in insert mode

### Version 1.2.2
Milestone: https://github.com/jaredpar/VsVim/issues?milestone=25&state=closed

Primary Issues Addressed

* Substitute with quotes behaved incorrectly 
* Substitute at end of line behaved incorrectly
* Support for Mind Scape workbench files 

### Version 1.2.1
Milestone: https://github.com/jaredpar/VsVim/issues?milestone=24&state=closed

Primary Issues Addressed

* Support for the clipboard option 
* Could not 'j' over blank lines in Visual Character Mode
* Comments were breaking vimrc loading
* Repeating commands resulted in intellisense being displayed

### Version 1.2 
Milestone: https://github.com/jaredpar/VsVim/issues?milestone=20&state=closed

Primary Issues Addressed

* Support for block motions
* Support for `a{text-object}` and `i{text-object}` in Visual Mode (`aB`, `a<`, etc ...)
* Support for :global command
* Support for block insertion
* Support for 'viw'. 
* Support for exclusive selections in Visual Mode
* Many key mapping issues involving key modifiers and non-alpha keys
* Repeating of Enter now better handles indentation
* Continued performance tuning of :hlsearch

### Version 1.1.2
Milestone: https://github.com/jaredpar/VsVim/issues?sort=created&direction=desc&state=closed&page=1&milestone=22

Primary Issues Addressed

* Performance of :hlseach
* Maintaining vertical caret column
* Several tabs / spaces issues including cc, caret column and repeat of 'cw', 
* Tab on new line inserts tab on previous line 

### Version 1.1.1
Milestone: https://github.com/jaredpar/VsVim/issues?milestone=19&sort=created&direction=desc&state=closed

Primary Issues Addressed

* Exception thrown while using CTRL-N
* Upper case marks broken in 1.1
* Replace command not working for international characters
* Intellisense, quick info causing an exception in Visual Studio 11
* Crash when dragging the window splitter from visual mode 
* CTRL-O didn't support commands that switched to visual or command mode

**Patch 1**

* Vim undo command causing too many Visual Studio undos to occur.  
* VsVim not running on machines with only Visual Studio 11 installed 

### Version 1.1.0 
Milestone: https://github.com/jaredpar/VsVim/issues?sort=created&direction=desc&state=closed&page=1&milestone=10

Primary Issues Addressed

* Insert mode largely rewritten. Better support for repeat and commands like CTRL-I, CTRL-M, CTRL-H, etc ...
* CTRL-N and CTRL-P support added. 
* CTRL-A and CTRL-X support added.  Keys must be manually mapped to VsVim to avoid unexpected conflicts with select all and cut. 
* Added support for the gv command
* VsVim will now preserve non-CRLF line endings 
* Support added for Dev11 preview

### Version 1.0.3
Milestone: https://github.com/jaredpar/VsVim/issues?milestone=17&state=closed

Primary Issues Addressed

* Shift-C was placing the caret in the incorrect position.  
* End key was cancelling Visual Mode 
* Enter and Back were causing issues with R# in certain scenarios 

### Version 1.0.2
Milestone: https://github.com/jaredpar/VsVim/issues?milestone=16&state=closed

Primary Issues Addressed

* Crash which occurred after closing tabs.  Most often repro'd when combined with Pro Power Tools
* Key mappings which contained multiple inputs didn't behave properly in insert mode 