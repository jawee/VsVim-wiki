There is a configuration issue in the stand alone install of Python Tools for Visual Studio which makes it impossible for VsVim to run out of the box.  The devenv.exe.config file has a binding redirect to a DLL which does not exist and causes VsVim to silently fail on startup.  This should only be a problem for installs of the PTVS stand alone shell.  Full versions of Visual Studio should not have this problem.  

To work around this problem do the following.  

1. Close Visual Studio
2. Comment out the following lines in `C:\Program Files\Microsoft Visual Studio 12.0\Common7\IDE\devenv.exe.config`

`            <dependentAssembly>`
`              <assemblyIdentity name="FSharp.Core" publicKeyToken="b03f5f7f11d50a3a" culture="neutral"/>`
`              <bindingRedirect oldVersion="2.0.0.0-4.3.0.0" newVersion="4.3.1.0"/>`
`            </dependentAssembly>`

3. Delete this directory `%LOCALAPPDATA%\Microsoft\VisualStudio\12.0\ComponentModelCache`
4. Restart Visual Studio 

**WARNING:** direct edits to devenv.exe.config are potentially dangerous. I tested out my changes locally and I'm confident this won't have any unforseen issues. This is not a guarantee though.  I'm working on a less hacky solution for this problem.  


Tracking bug is in PTVS right now.  

https://pytools.codeplex.com/workitem/1464
