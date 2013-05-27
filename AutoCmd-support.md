VsVim has limited support for `autocmd`.  Full support of `autocmd` is an explicit non-goal at this time.  Many of the events vim supports simply have no equivalent in Visual Studio and hence can't be accurately emulated.  However most uses of `autocmd` are on a small subset of commands for which there is a Visual Studio equivalent and we will work to support those.

### What is supported? 
At this time the following `autocmd` events are supported 

* BufEnter
* BufWinEnter
* BufWinLeave
* FileType

Other events can be added on request assuming there is an equivalent mapping in Visual Studio. 

### How can I disable this support? 
There are 2 ways to disable VsVim support for `autocmd`.  

    set novsvim_autocmd
    set vsvim_useeditordefaults

Either of these will disable VsVim support for `autocmd`.  




Supporting the full breadth of `autocmd` is difficult because of the lack of a clear mapping between Visual Studio and vim events.  However there is enough `autocmd` support to allow for the cus