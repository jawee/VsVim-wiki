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

# WPF

Although the F# core of VsVim doesn't use WPF directly, many peripheral areas use it extensively. For example, the `CommandMargin` could almost be a standalone WPF project. If you intend to work in one of these areas, you need to familiarize yourself with WPF.
