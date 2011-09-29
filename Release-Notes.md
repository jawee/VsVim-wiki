# Release Notes

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

