## Porting VsVim to other applications

I am occasionally asked how difficult it would be to port VsVim to other applications.  Or more specifically how much of a dependency does VsVim have on Visual Studio.  To answer this I need to first explain the Visual Studio architecture a bit

## Visual Studio Architecture

Visual Studio itself is layered into 2 important parts

1. The WPF editor
2. The Visual Studio Shell

The WPF editor was introduced in Visual Studio 2010 and is a completely independent component.  It includes a very advanced text data modeling, view and extension layer.  It's easiest to think of this as a simple WPF editting control that knows nothing of Visual Studio.

The Visual Studio Shell is what most people think of when they think of Visual Studio.  The menus, solution explorer, tool windows, etc ...  

The WPF editor is actually the core of several other products.  Powershell ISE and Web Matrix both use the WPF editor as their core editting experience. 

## VsVim Architecture 

VsVim is intentionally layered in the same way as Visual Studio.  The core parts of VsVim (VimCore and VimWpf) depend only on the WPF editor.  These projects represent all of the Vim specific logic.  The rest of VsVim (VsVimShared + VsVim) are depnedent on the shell and mainly deal with hosting issues in Visual Studio.  

## Porting VsVim 

Porting VsVim to an application which uses the WPF editor is very straight forward.  VimWpf defines an abstract class named VimHost than needs to be implemented.  The number of methods that must be implemented are small and an example implementation exists in the VimTestApp project.  

The implementation of VimHost along with the binaries from VimCore and VimWpf need to be included in the MEF container of the application.  Once that is done VsVim will light up in the application.  

Porting VsVim to an application which doesn't use the WPF editor would be a large under taking.  VsVim takes advantage of a large portion of the text model in the editor (in particular it's ability to get snapshots and track points across edits).  The port would have to include a large subset of the WPF editor or rewrite significant portions of VsVim.  It's not a task that I think could easily be done.  
