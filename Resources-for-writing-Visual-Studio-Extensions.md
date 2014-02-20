I've gotten a few requests about resources for learning Visual Studio extensions.  Here is a quick summary of the resources that I use when developing VsVim.  

While there is sparse documentation for the older IVs style interfaces, there is ample documentation for the WPF editor introduced in Visual Studio 2010.  Here is the main tutorial you should start with 

- http://msdn.microsoft.com/en-us/library/vstudio/dd885240.aspx

The best place to look is at existing Visual Studio Extensions that are open source.  Their sources already contain many of the solutions you are looking for.  Here are a few of note

- https://github.com/jaredpar/VsVim - taggers, adornments, key stroke handling, mouse handling, custom editting, undo integration
- https://nuget.codeplex.com - project system integration, custom tool windows, context menu, build integration
- https://github.com/ryanmolden - Ryan is a developer in Visual Studio and puts up great little samples on not so obvious patterns which are commonly requested by customers.  I **frequently** seek him out for help on problems I am having.  
- https://github.com/paulcbetts/SaveAllTheTime - reactive solution in VS, save integration, adornments
- https://github.com/dungpa/fantomas - undo integration, command handling
- https://github.com/madskristensen/WebEssentials2013 - these guys integrate into so many corners of Visual Studio
- https://pytools.codeplex.com/ - one of the few OSS projects which has a fully integrated language 

Another good resource is the MSDN forums.  A lot of the Visual Studio developers monitor that group, Ryan included, and give great answers to the hard questions there.  

- http://social.msdn.microsoft.com/Forums/vstudio/en-US/home?category=visualstudio