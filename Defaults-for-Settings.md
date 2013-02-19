VsVim 1.3.3 introduced a breaking change in how it chooses the values for settings shared between Vim and Visual Studio (`expandtab`, `tabstop`, `shiftwidth`, `cursorline` and `number`).  

> If VsVim detects a _vimrc file it will default to settings defined by vim, else it will default to Visual Studio settings

For users who want to define different defaults for VsVim than normal vim you can create a _vsvimrc file in the same directory as _vimrc.  VsVim will prefer _vsvimrc over _vimrc. 

I know this broke a few peoples expectations and I apologize for that.  I strive to avoid any breaking changes in updates and I'm not above implementing dirty hacks to do so.  But in this case I really had no choice.  

## Why did I make this change? 
Vim and Visual Studio have a common subset of settings and VsVim must pick a winner between settings that differ.  The solution up until this point was organic and incredibly inconsistent.  It goes back to the days where VsVim was a private toy of mine and my support for settings was so basic that I just hard coded a winner.  

As VsVim advanced so did my handling of settings.  I made patches where necessary to deal with the load ordering and users were mostly happy.  Then came Visual Studio 2012 and it changed things in a bad way

1. Vs 2010 and Vs 2012 have different defaults for specific settings
2. Vs 2012 changed the order in which settings loaded during document ope in a way that fundamentally broke me [1]

As I sat down to fix Vs 2012 and studied the changes they made I realized there was no way for me to keep the previous evolved behavior.  Also because of the default changes it would be hard to provide any consistency between how VsVim loaded in 2010 and 2012.  

Something simply had to give.  I decided that if I had to make a break it would be best to do it only once.  So I designed a predictable solution that I feel will be maintainable in the face of future Visual Studio changes.  

## Why didn't not only use settings which were only explicit set in the vimrc? 
I definitely considered the idea of looking at individual settings but eventually backed away from it. There are a good portion of vim users who prefer the vim default for a setting but never specified the default in the vimrc file (it would be redundant). 

For instance some users don't want a cursor line. This is the default behavior though so they never say `:set nocursorline`, they just expect it to not be there. I didn't want them contorting their standard vimrc for VsVim.

Additionally it gets even more complex because vim and Visual Studio have different defaults for a portion of the shared settings.  Also Visual Studio has different defaults for different versions of Visual Studio and different languages (so much fun)

- `tabstop`: vim = 8, vs = 4
- `shiftwidth`: vim = 8, vs = 4
- `cursorline`: vim = false, vs 2010 = false, vs 2012 = true
- `expandtab`: vim = false, vs = (C# false) (C++ true)
- `number`: vim = false, vs = false

After looking at all of this I decided the only predictable way to approach the problem was to have one win entirely over the other.  

## What if I have a _vimrc and I want VsVim to use Visual Studio settings?
Add the following line to your _vimrc file 

    set vsvim_useeditordefaults

VsVim will see this and let Visual Studio settings win at start up time 

[1] There are 2 events which generally fire during document load.  In 2010 the settings pretty much all loaded after the 2nd event.  In Vs 2012 they now load in all 3 places (before first, between and after second).  It's an implementation detail I shouldn't have depended on but as I said before, this code wasn't ever designed, it evolved.  


