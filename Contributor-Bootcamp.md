# Introduction

If you want to contribute to VsVim, you will have the usual hurdles of git, GitHub, forking, etc. This is non-trivial exercise for many (even seasoned) developers.

# DotNet

VsVim is heavily dependent on the .Net ecosystem. Much of the infrastructure code is written in C#. If you are a C# programmer, you are well-prepared to contribute to VsVim. Things like `IDisposable`, `IEnumerable`, assemblies, etc. for a valuable foundation for much of VsVim.

# F#

Chances are that even if you are well equipped for most of VsVim, the biggest hurdle will be F#.

# Visual Studio Extensibility

A developer working on Visual Studio extensions needs to sift through a fairly complex set a material in order to write their first extension.

# MEF

VsVim relies on the MEF framework to instantiate components and locate services.

# Visual Studio Editor

Much of VsVim deals directly with text using the Visual Studio editor APIs. These APIs are essential for understanding what VsVim is trying to do and how it does it. It is helpful to read this overview so that you understand the key concepts and terms:

* [Inside the Editor](https://docs.microsoft.com/en-us/visualstudio/extensibility/inside-the-editor)

Additional information:

* [Language Service and Editor Extension Points](https://docs.microsoft.com/en-us/visualstudio/extensibility/language-service-and-editor-extension-points)

# WPF

Although the F# core of VsVim doesn't use WPF directly, many peripheral areas use it extensively. For example, the `CommandMargin` could almost be a standalone WPF project. If you intend to work in one of these areas, you need to familiarize yourself with WPF.

# International Keyboards

If you are US keyboard user, you may be unfamiliar with the complexities of international keyboards. For the most part WPF does a very good job of supporting international keyboards, but if you are working in an area that affects the keyboard, you may need to study up on topics that are foreign to a US keyboard user.

## AltGr, Dead Keys, etc.

Although the US keyboard does not make use of AltGr or dead keys, virtually all other languages including Western European languages do. Since US English has no need of accented characters, this makes US keyboard users fairly naive in an area that most of the world deals with on a daily basis. However, you are not out of luck. You can easily install the US International keyboard and test AltGr and dead keys.

## IME - The Input Method Editor

VsVim and vim have special support for the IME that a modeless editor doesn't necessarily need to have. Use of the IME is common in many non-Latin languages. If you are a US keyboard user, you may have no idea what an IME even is. To work on this area of the code, you can set up a JP keyboard and use it's IME while still retaining the US keyboard as your default.