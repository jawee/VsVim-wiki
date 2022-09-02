### Acquisition
#### VS Mac 8.10
Download the extension via the VSMac extension gallery (Visual Studio -> Extensions -> Gallery) and search for VSVim.

#### VS Mac Preview (Cocoa 17.0+)
VSMac 17.0 does not yet have an extension gallery. However, it is still possible to install VsVim by downloading the latest mpack (currently [2.8.0.14](https://github.com/VsVim/VsVim/releases/download/v2.8.0.14-vsm8.9/Vim.Mac.VsVim_2.8.0.14.mpack)) file from the [Releases](https://github.com/VsVim/VsVim/releases) page and then running the following command inside a terminal.

```sh
/Applications/Visual\ Studio\ \(Preview\).app/Contents/MacOS/vstool setup install /FULL/PATH/TO/Vim.Mac.VsVim_2.8.0.14.mpack
```

Restart VSMac if it was already running.

### Build instructions


If you want to build from source code instead, then use one of the following two methods.

```sh
git clone https://github.com/VsVim/VsVim.git
cd VsVim
msbuild /p:Configuration=DebugMac /p:Platform="Any CPU" /t:Restore
cd Src/VimMac
msbuild /p:InstallAddin=True
```

or

```sh
git clone --branch vsmac https://github.com/VsVim/VsVim.git && cd VsVim && msbuild /p:Configuration=DebugMac /p:Platform="Any CPU" /t:Restore && cd Src/VimMac && msbuild /p:InstallAddin=True
```

This will build the VsVim extension against the current installation of VSMac.

After running those commands, ensure that the Addin has been loaded into VSMac and is enabled.

<img width="815" alt="image" src="https://user-images.githubusercontent.com/667194/66313771-d42a5680-e90a-11e9-9d00-cb3563ef4a9e.png">

Some control keys used by VsVim conflict with default VSMac keys (`<C-d>` etc). If you want VsVim to use these keys then please select the `Visual Studio + VsVim` keybinding scheme.

<img width="664" alt="image" src="https://user-images.githubusercontent.com/667194/70971779-9cbdf000-2099-11ea-999e-c528f9c026a3.png">


That's it! A restart of VSMac may be needed.

If you like, you may use a `~/.vsvimrc` file to customize the behavior of VsVim. This is mine.

#### Example Vim configuration

```vim
set incsearch
set hlsearch
let mapleader=" "
set cursorline
set clipboard=unnamed " <-- Use the system clipboard when yanking and putting
set expandtab
set ignorecase
set smartcase
set autoindent
set backspace=indent,eol,start " <-- Needed if you want the backspace key to work like you would expect!
set tabstop=4
set shiftwidth=4
nnoremap <C-p> :vsc MonoDevelop.Ide.Commands.SearchCommands.GotoFile <CR>
nnoremap gu :vsc MonoDevelop.Refactoring.RefactoryCommands.FindReferences <CR>
nnoremap gh :vsc MonoDevelop.Ide.Commands.TextEditorCommands.ShowQuickInfo <CR> " <-- Show tooltip without mouse
nnoremap gb :vsc MonoDevelop.RefactoryCommands.NavigationCommands.FindBaseSymbols <CR>
nnoremap <C-w>o :vsc MonoDevelop.Ide.Commands.FileTabCommands.CloseAllButThis <CR>

" I prefer default VSMac behaviour of navigating between buffers
" when navigating backwards and forwards
nnoremap <C-o> :vsc MonoDevelop.Ide.Commands.NavigationCommands.NavigateBack <CR>
nnoremap <C-i> :vsc MonoDevelop.Ide.Commands.NavigationCommands.NavigateForward <CR>

" Keys copied from SpaceMacs
nnoremap <Space>p :vsc MonoDevelop.Ide.Commands.SearchCommands.GotoFile <CR>
nnoremap <Space>fs :vsc MonoDevelop.Ide.Commands.FileCommands.Save <CR>

nmap gs :vsc VsVim.ShowPadByTitle Solution<CR>

" Emacs keys when in insert mode
inoremap <C-d> MonoDevelop.Ide.Commands.EditCommands.Delete
inoremap <C-a> MonoDevelop.Ide.Commands.TextEditorCommands.LineStart
```


#### Development guide
 If you want to help develop the code, then you will also need to install the AddinMaker extension

<img width="828" alt="image" src="https://user-images.githubusercontent.com/667194/66313143-c45e4280-e909-11e9-8356-91ff8e068e62.png">

This extension adds some IDE support. It takes care of locating VSMac references that are located under `/Applications/Visual Studio.app` and also makes it easy to run any changes (Start Debugging on the VimMac project should launch a new instance of VSMac with any changes to the Extension applied.

<img width="423" alt="image" src="https://user-images.githubusercontent.com/667194/66313484-5bc39580-e90a-11e9-8091-bb75e00f94ae.png">

Please refer to the AddinMaker documentation if you want to target a different version of VSMac than the one that you are currently running.

#### Commands to be used in .vsvimrc

- MonoDevelop.Ide.Commands.TextEditorCommands.LineUp
- MonoDevelop.Ide.Commands.TextEditorCommands.LineDown
- MonoDevelop.Ide.Commands.TextEditorCommands.InsertNewLinePreserveCaretPosition
- MonoDevelop.Ide.CodeFormatting.CodeFormattingCommands.FormatBuffer
- MonoDevelop.Ide.Commands.TextEditorCommands.LineStart
- MonoDevelop.Ide.Commands.TextEditorCommands.DeleteRightChar
- MonoDevelop.Ide.Commands.TextEditorCommands.CharRight
- MonoDevelop.Ide.Commands.TextEditorCommands.CharLeft
- MonoDevelop.Ide.Commands.EditCommands.Copy
- MonoDevelop.Ide.Commands.EditCommands.Cut
- MonoDevelop.Ide.Commands.EditCommands.Paste
- MonoDevelop.Ide.Commands.EditCommands.Delete
- MonoDevelop.Ide.Commands.EditCommands.Rename
- MonoDevelop.Ide.Commands.EditCommands.Undo
- MonoDevelop.Ide.Commands.EditCommands.Redo
- MonoDevelop.Ide.Commands.EditCommands.SelectAll
- MonoDevelop.Ide.Commands.EditCommands.ToggleCodeComment
- MonoDevelop.Ide.Commands.EditCommands.AddCodeComment
- MonoDevelop.Ide.Commands.EditCommands.RemoveCodeComment
- MonoDevelop.Ide.Commands.EditCommands.IndentSelection
- MonoDevelop.Ide.Commands.EditCommands.UnIndentSelection
- MonoDevelop.Ide.Commands.EditCommands.UppercaseSelection
- MonoDevelop.Ide.Commands.EditCommands.LowercaseSelection
- MonoDevelop.Ide.Commands.EditCommands.RemoveTrailingWhiteSpaces
- MonoDevelop.Ide.Commands.EditCommands.JoinWithNextLine
- MonoDevelop.Ide.Commands.EditCommands.SortSelectedLines
- MonoDevelop.Ide.Commands.EditCommands.InsertGuid
- MonoDevelop.Ide.Commands.EditCommands.CopyValue
- MonoDevelop.Ide.Commands.EditCommands.MonodevelopPreferences
- MonoDevelop.Ide.Commands.EditCommands.InsertStandardHeader
- MonoDevelop.Ide.Commands.EditCommands.EnableDisableFolding
- MonoDevelop.Ide.Commands.EditCommands.ToggleFolding
- MonoDevelop.Ide.Commands.EditCommands.ToggleAllFoldings
- MonoDevelop.Ide.Commands.EditCommands.FoldDefinitions
- MonoDevelop.Ide.Commands.ProjectCommands.AddNewProject
- MonoDevelop.Ide.Commands.ProjectCommands.AddNewWorkspace
- MonoDevelop.Ide.Commands.ProjectCommands.AddNewSolution
- MonoDevelop.Ide.Commands.ProjectCommands.AddSolutionFolder
- MonoDevelop.Ide.Commands.ProjectCommands.AddProject
- MonoDevelop.Ide.Commands.ProjectCommands.AddItem
- MonoDevelop.Ide.Commands.ProjectCommands.RemoveFromProject
- MonoDevelop.Ide.Commands.ProjectCommands.Options
- MonoDevelop.Ide.Commands.ProjectCommands.SetStartupProjects
- MonoDevelop.Ide.Commands.ProjectCommands.SolutionOptions
- MonoDevelop.Ide.Commands.ProjectCommands.ProjectOptions
- MonoDevelop.Ide.Commands.ProjectCommands.ExcludeFromProject
- MonoDevelop.Ide.Commands.ProjectCommands.AddReference
- MonoDevelop.Ide.Commands.ProjectCommands.AddNewFiles
- MonoDevelop.Ide.Commands.ProjectCommands.AddEmptyClass
- MonoDevelop.Ide.Commands.ProjectCommands.AddFiles
- MonoDevelop.Ide.Commands.ProjectCommands.AddFilesFromFolder
- MonoDevelop.Ide.Commands.ProjectCommands.AddExistingFolder
- MonoDevelop.Ide.Commands.ProjectCommands.NewFolder
- MonoDevelop.Ide.Commands.ProjectCommands.IncludeToProject
- MonoDevelop.Ide.Commands.ProjectCommands.BuildSolution
- MonoDevelop.Ide.Commands.ProjectCommands.Build
- MonoDevelop.Ide.Commands.ProjectCommands.RebuildSolution
- MonoDevelop.Ide.Commands.ProjectCommands.Rebuild
- MonoDevelop.Ide.Commands.ProjectCommands.SetAsStartupProject
- MonoDevelop.Ide.Commands.ProjectCommands.Run
- MonoDevelop.Ide.Commands.ProjectCommands.RunEntry
- MonoDevelop.Ide.Commands.ProjectCommands.Clean
- MonoDevelop.Ide.Commands.ProjectCommands.CleanSolution
- MonoDevelop.Ide.Commands.ProjectCommands.LocalCopyReference
- MonoDevelop.Ide.Commands.ProjectCommands.Stop
- MonoDevelop.Ide.Commands.ProjectCommands.Reload
- MonoDevelop.Ide.Commands.ProjectCommands.Unload
- MonoDevelop.Ide.Commands.ProjectCommands.EditSolutionItem
- MonoDevelop.Ide.Commands.ProjectCommands.ExportSolution
- MonoDevelop.Ide.Commands.ProjectCommands.ApplyPolicy
- MonoDevelop.Ide.Commands.ProjectCommands.ExportPolicy
- MonoDevelop.Ide.Commands.ProjectCommands.RunCodeAnalysisSolution
- MonoDevelop.Ide.Commands.ProjectCommands.RunCodeAnalysisProject
- MonoDevelop.Ide.Commands.ProjectCommands.ToggleFileNesting
- MonoDevelop.Debugger.DebugCommands.Debug
- MonoDevelop.Debugger.DebugCommands.DebugEntry
- MonoDevelop.ConnectedServices.Commands.OpenServicesGallery
- MonoDevelop.DotNetCore.Commands.Pack
- MonoDevelop.DotNetCore.Commands.InstallWorkloads
- MonoDevelop.DotNetCore.Commands.ManageUserSecrets
- Xamarin.Ide.ArchiveCommands.Archive
- Xamarin.Ide.ArchiveCommands.ArchiveAll
- MonoDevelop.MacDev.Commands.SyncWithXcode
- MonoDevelop.MonoMac.MonoMacCommands.Profile
- MonoDevelop.MonoMac.MonoMacCommands.ProfileItem
- MonoDevelop.MonoDroid.GooglePlayServices.Commands.AddGooglePlayServiceNuget
- Xamarin.Ide.AndroidXMigration.Migrate
- MonoDevelop.AspNetCore.Commands.PublishToFolder
- MonoDevelop.AspNetCore.Commands.AspNetCoreCommands.Scaffold
- Xamarin.AzureSupport.Publishing.Commands.PublishToAzure
- Xamarin.Android.Deploy.MonoDevelop.Commands.DeployCommands.ApplyChanges
- MonoDevelop.Ide.Commands.FileCommands.OpenFile
- MonoDevelop.Ide.Commands.FileCommands.NewFile
- MonoDevelop.Ide.Commands.FileCommands.Save
- MonoDevelop.Ide.Commands.FileCommands.SaveAll
- MonoDevelop.Ide.Commands.FileCommands.NewProject
- MonoDevelop.Ide.Commands.FileCommands.NewWorkspace
- MonoDevelop.Ide.Commands.FileCommands.CloseFile
- MonoDevelop.Ide.Commands.FileCommands.CloseAllFiles
- MonoDevelop.Ide.Commands.FileCommands.CloseWorkspace
- MonoDevelop.Ide.Commands.FileCommands.CloseWorkspaceItem
- MonoDevelop.Ide.Commands.FileCommands.ReloadFile
- MonoDevelop.Ide.Commands.FileCommands.SaveAs
- MonoDevelop.Ide.Commands.FileCommands.ClearRecentFiles
- MonoDevelop.Ide.Commands.FileCommands.ClearRecentProjects
- MonoDevelop.Ide.Commands.FileCommands.Exit
- MonoDevelop.Ide.Commands.FileCommands.OpenInTerminal
- MonoDevelop.Ide.Commands.FileCommands.OpenFolder
- MonoDevelop.Ide.Commands.FileCommands.OpenContainingFolder
- MonoDevelop.Ide.Commands.FileCommands.ShowProperties
- MonoDevelop.Ide.Commands.FileCommands.CopyToOutputDirectory
- MonoDevelop.Ide.Commands.ProjectCommands.SpecificAssemblyVersion
- MonoDevelop.Ide.Commands.FileTabCommands.CloseAll
- MonoDevelop.Ide.Commands.FileTabCommands.CloseAllButThis
- MonoDevelop.Ide.Commands.FileTabCommands.CloseAllToTheRight
- MonoDevelop.Ide.Commands.FileTabCommands.CopyPathName
- MonoDevelop.Ide.Commands.FileTabCommands.CopyRelativePathName
- MonoDevelop.Ide.Commands.FileTabCommands.ReopenClosedTab
- MonoDevelop.Ide.Commands.FileTabCommands.CloseAllExceptPinned
- MonoDevelop.Ide.Commands.FileTabCommands.PinTab
- MonoDevelop.Ide.Commands.ViewCommands.NewLayout
- MonoDevelop.Ide.Commands.ViewCommands.DeleteCurrentLayout
- MonoDevelop.Ide.Commands.FileTabCommands.ToggleMaximize
- MonoDevelop.Ide.Commands.ViewCommands.FullScreen
- MonoDevelop.Ide.Commands.ViewCommands.Open
- MonoDevelop.Ide.Commands.ViewCommands.ResetTreeDisplayOptions
- MonoDevelop.Ide.Commands.ViewCommands.RefreshTree
- MonoDevelop.Ide.Commands.ViewCommands.CollapseAllTreeNodes
- MonoDevelop.Ide.Commands.ViewCommands.ShowNext
- MonoDevelop.Ide.Commands.ViewCommands.ShowPrevious
- MonoDevelop.Ide.Commands.NavigationCommands.NavigateBack
- MonoDevelop.Ide.Commands.NavigationCommands.NavigateForward
- MonoDevelop.Ide.Commands.NavigationCommands.ClearNavigationHistory
- MonoDevelop.Ide.Commands.ViewCommands.ZoomIn
- MonoDevelop.Ide.Commands.ViewCommands.ZoomOut
- MonoDevelop.Ide.Commands.ViewCommands.ZoomReset
- MonoDevelop.Ide.Commands.ViewCommands.SideBySideMode
- MonoDevelop.Ide.Commands.ViewCommands.SingleMode
- MonoDevelop.Ide.Commands.ViewCommands.NextNotebook
- MonoDevelop.Ide.Commands.ViewCommands.PreviousNotebook
- MonoDevelop.Ide.Commands.ViewCommands.FocusCurrentDocument
- MonoDevelop.Ide.Commands.ViewCommands.CenterAndFocusCurrentDocument
- MonoDevelop.Ide.Commands.ViewCommands.ShowWelcomePage
- Xamarin.Ide.ArchiveCommands.ViewArchives
- MonoDevelop.Ide.Commands.ToolCommands.AddinManager
- MonoDevelop.Ide.Commands.ToolCommands.EditCustomTools
- MonoDevelop.Ide.Commands.ToolCommands.InstrumentationViewer
- MonoDevelop.Ide.Commands.ToolCommands.ToggleSessionRecorder
- MonoDevelop.Ide.Commands.ToolCommands.ReplaySession
- MonoDevelop.RegexToolkit.Commands.ShowRegexToolkit
- MonoDevelop.MacDev.Commands.LaunchInstruments
- MonoDevelop.MonoDroid.EmulatorSupport.XamarinEmulatorManager.Commands.OpenXamarinEmulatorManager
- MonoDevelop.AssemblyBrowser.ShowAssemblyBrowser
- MonoDevelop.Ide.Commands.WindowCommands.NextDocument
- MonoDevelop.Ide.Commands.WindowCommands.PrevDocument
- MonoDevelop.Ide.Commands.WindowCommands.OpenDocument1
- MonoDevelop.Ide.Commands.WindowCommands.OpenDocument2
- MonoDevelop.Ide.Commands.WindowCommands.OpenDocument3
- MonoDevelop.Ide.Commands.WindowCommands.OpenDocument4
- MonoDevelop.Ide.Commands.WindowCommands.OpenDocument5
- MonoDevelop.Ide.Commands.WindowCommands.OpenDocument6
- MonoDevelop.Ide.Commands.WindowCommands.OpenDocument7
- MonoDevelop.Ide.Commands.WindowCommands.OpenDocument8
- MonoDevelop.Ide.Commands.WindowCommands.OpenDocument9
- MonoDevelop.Ide.Commands.WindowCommands.SwitchNextDocument
- MonoDevelop.Ide.Commands.WindowCommands.SwitchPreviousDocument
- MonoDevelop.Ide.Commands.WindowCommands.SwitchNextPad
- MonoDevelop.Ide.Commands.WindowCommands.SwitchPreviousPad
- VisualStudioMac.MacIntegration.MacIntegrationCommands.MinimizeWindow
- VisualStudioMac.MacIntegration.MacIntegrationCommands.HideWindow
- VisualStudioMac.MacIntegration.MacIntegrationCommands.ZoomWindow
- VisualStudioMac.MacIntegration.MacIntegrationCommands.HideOthers
- VisualStudioMac.MacIntegration.MacIntegrationCommands.ShowOthers
- VisualStudioMac.UI.Docking.ResetLayout
- MonoDevelop.Ide.Commands.HelpCommands.OpenLogDirectory
- MonoDevelop.Ide.Commands.HelpCommands.OpenLogFile
- MonoDevelop.Ide.Commands.HelpCommands.About
- MonoDevelop.Ide.Updater.UpdateCommands.CheckForUpdates
- MonoDevelop.Ide.Commands.HelpCommands.MarkLog
- MonoDevelop.Ide.Commands.HelpCommands.DumpWorkspace
- Xamarin.Ide.FeedbackCommands.ReportProblem
- Xamarin.Ide.FeedbackCommands.ProvideSuggestion
- MonoDevelop.Unity.Documentation.UnityDocumentation
- MonoDevelop.Ide.Commands.SearchCommands.Find
- MonoDevelop.Ide.Commands.SearchCommands.Replace
- MonoDevelop.Ide.Commands.SearchCommands.FindNext
- MonoDevelop.Ide.Commands.SearchCommands.FindPrevious
- MonoDevelop.Ide.Commands.SearchCommands.EmacsFindNext
- MonoDevelop.Ide.Commands.SearchCommands.EmacsFindPrevious
- MonoDevelop.Ide.Commands.SearchCommands.FindNextSelection
- MonoDevelop.Ide.Commands.SearchCommands.FindPreviousSelection
- MonoDevelop.Ide.Commands.SearchCommands.FindInFiles
- MonoDevelop.Ide.Commands.SearchCommands.ReplaceInFiles
- MonoDevelop.Ide.Commands.SearchCommands.RunCommand
- MonoDevelop.Ide.Commands.SearchCommands.GotoType
- MonoDevelop.Ide.Commands.SearchCommands.GotoFile
- MonoDevelop.Components.MainToolbar.Commands.NavigateTo
- MonoDevelop.Ide.Commands.SearchCommands.ToggleBookmark
- MonoDevelop.Ide.Commands.SearchCommands.PrevBookmark
- MonoDevelop.Ide.Commands.SearchCommands.NextBookmark
- MonoDevelop.Ide.Commands.SearchCommands.ClearBookmarks
- MonoDevelop.Ide.Commands.SearchCommands.GotoLineNumber
- MonoDevelop.Ide.Commands.SearchCommands.UseSelectionForFind
- MonoDevelop.Ide.Commands.SearchCommands.UseSelectionForReplace
- MonoDevelop.Ide.Commands.TextEditorCommands.ShowCompletionWindow
- MonoDevelop.Ide.Commands.TextEditorCommands.ShowCodeTemplateWindow
- MonoDevelop.Ide.Commands.TextEditorCommands.ShowCodeSurroundingsWindow
- MonoDevelop.Ide.Commands.TextEditorCommands.LineEnd
- MonoDevelop.Ide.Commands.TextEditorCommands.DeleteLeftChar
- MonoDevelop.Ide.Commands.TextEditorCommands.DocumentStart
- MonoDevelop.Ide.Commands.TextEditorCommands.DocumentEnd
- MonoDevelop.Ide.Commands.TextEditorCommands.PageUp
- MonoDevelop.Ide.Commands.TextEditorCommands.PageDown
- MonoDevelop.Ide.Commands.TextEditorCommands.ScrollLineUp
- MonoDevelop.Ide.Commands.TextEditorCommands.ScrollLineDown
- MonoDevelop.Ide.Commands.TextEditorCommands.ScrollPageUp
- MonoDevelop.Ide.Commands.TextEditorCommands.ScrollPageDown
- MonoDevelop.Ide.Commands.TextEditorCommands.ScrollTop
- MonoDevelop.Ide.Commands.TextEditorCommands.ScrollBottom
- MonoDevelop.Ide.Commands.TextEditorCommands.DeleteLine
- MonoDevelop.Ide.Commands.TextEditorCommands.DeleteToLineStart
- MonoDevelop.Ide.Commands.TextEditorCommands.DeleteToLineEnd
- MonoDevelop.Ide.Commands.TextEditorCommands.MoveBlockUp
- MonoDevelop.Ide.Commands.TextEditorCommands.MoveBlockDown
- MonoDevelop.Ide.Commands.TextEditorCommands.ShowParameterCompletionWindow
- MonoDevelop.Ide.Commands.TextEditorCommands.GotoMatchingBrace
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectionMoveRight
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectionMoveLeft
- MonoDevelop.Ide.Commands.TextEditorCommands.MovePrevWord
- MonoDevelop.Ide.Commands.TextEditorCommands.MoveNextWord
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectionMovePrevWord
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectionMoveNextWord
- MonoDevelop.Ide.Commands.TextEditorCommands.MovePrevSubword
- MonoDevelop.Ide.Commands.TextEditorCommands.MoveNextSubword
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectionMovePrevSubword
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectionMoveNextSubword
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectionMoveUp
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectionMoveDown
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectionMoveHome
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectionMoveEnd
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectionMoveToDocumentStart
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectionMoveToDocumentEnd
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectCurrentWord
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectCurrentSubword
- MonoDevelop.Ide.Commands.TextEditorCommands.SubwordExpandSelection
- MonoDevelop.Ide.Commands.TextEditorCommands.ExpandSelectionToLine
- MonoDevelop.Ide.Commands.TextEditorCommands.ExpandSelection
- MonoDevelop.Ide.Commands.TextEditorCommands.ShrinkSelection
- MonoDevelop.Ide.Commands.TextEditorCommands.SubwordShrinkSelection
- MonoDevelop.Ide.Commands.TextEditorCommands.SwitchCaretMode
- MonoDevelop.Ide.Commands.TextEditorCommands.InsertTab
- MonoDevelop.Ide.Commands.TextEditorCommands.RemoveTab
- MonoDevelop.Ide.Commands.TextEditorCommands.InsertNewLine
- MonoDevelop.Ide.Commands.TextEditorCommands.InsertNewLineAtEnd
- MonoDevelop.Ide.Commands.TextEditorCommands.CompleteStatement
- MonoDevelop.Ide.Commands.TextEditorCommands.DeletePrevWord
- MonoDevelop.Ide.Commands.TextEditorCommands.DeleteNextWord
- MonoDevelop.Ide.Commands.TextEditorCommands.DeletePrevSubword
- MonoDevelop.Ide.Commands.TextEditorCommands.DeleteNextSubword
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectionPageDownAction
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectionPageUpAction
- MonoDevelop.Ide.Commands.TextEditorCommands.TransposeCharacters
- MonoDevelop.Ide.Commands.TextEditorCommands.TransposeWords
- MonoDevelop.Ide.Commands.TextEditorCommands.TransposeSubwords
- MonoDevelop.Ide.Commands.TextEditorCommands.TransposeLines
- MonoDevelop.Ide.Commands.TextEditorCommands.InsertNextMatchingCaret
- MonoDevelop.Ide.Commands.TextEditorCommands.InsertAllMatchingCarets
- MonoDevelop.Ide.Commands.TextEditorCommands.RemoveLastSecondaryCaret
- MonoDevelop.Ide.Commands.TextEditorCommands.MoveLastCaretDown
- MonoDevelop.Ide.Commands.TextEditorCommands.RotatePrimaryCaretNext
- MonoDevelop.Ide.Commands.TextEditorCommands.RotatePrimaryCaretPrevious
- MonoDevelop.Ide.Commands.TextEditorCommands.GoToContainingDeclaration
- MonoDevelop.Ide.Commands.TextEditorCommands.SelectContainingDeclaration
- MonoDevelop.Ide.Commands.TextEditorCommands.ToggleBlockSelectionMode
- MonoDevelop.Ide.Commands.TextEditorCommands.DuplicateLine
- MonoDevelop.Ide.Commands.TextEditorCommands.DynamicAbbrev
- MonoDevelop.Ide.Commands.TextEditorCommands.PulseCaret
- MonoDevelop.Ide.Commands.TextEditorCommands.ShowQuickInfo
- MonoDevelop.Ide.Commands.TextEditorCommands.ShowTextMateScopesHandler
- MonoDevelop.SourceEditor.QuickTasks.ScrollbarCommand.ShowMinimap
- MonoDevelop.CSharp.Highlighting.MoveToUsagesCommand.PrevUsage
- MonoDevelop.CSharp.Highlighting.MoveToUsagesCommand.NextUsage
- MonoDevelop.DesignerSupport.Commands.SwitchBetweenRelatedFiles
- MonoDevelop.Debugger.DebugCommands.DebugApplication
- MonoDevelop.Debugger.DebugCommands.AttachToProcess
- MonoDevelop.Debugger.DebugCommands.Detach
- MonoDevelop.Debugger.DebugCommands.Pause
- MonoDevelop.Debugger.DebugCommands.Continue
- MonoDevelop.Debugger.DebugCommands.HotReload
- MonoDevelop.Debugger.DebugCommands.StepOver
- MonoDevelop.Debugger.DebugCommands.StepInto
- MonoDevelop.Debugger.DebugCommands.StepOut
- MonoDevelop.Debugger.DebugCommands.NewBreakpoint
- MonoDevelop.Debugger.DebugCommands.NewFunctionBreakpoint
- MonoDevelop.Debugger.DebugCommands.NewCatchpoint
- MonoDevelop.Debugger.DebugCommands.ShowBreakpoints
- MonoDevelop.Debugger.DebugCommands.RemoveBreakpoint
- MonoDevelop.Debugger.DebugCommands.ShowBreakpointProperties
- MonoDevelop.Debugger.DebugCommands.ToggleBreakpoint
- MonoDevelop.Debugger.DebugCommands.EnableDisableBreakpoint
- MonoDevelop.Debugger.DebugCommands.DisableAllBreakpoints
- MonoDevelop.Debugger.DebugCommands.ClearAllBreakpoints
- MonoDevelop.Debugger.DebugCommands.ShowDisassembly
- MonoDevelop.Debugger.DebugCommands.ExpressionEvaluator
- MonoDevelop.Debugger.DebugCommands.ShowCurrentExecutionLine
- MonoDevelop.Debugger.DebugCommands.AddWatch
- MonoDevelop.Debugger.DebugCommands.StopEvaluation
- MonoDevelop.Debugger.DebugCommands.RunToCursor
- MonoDevelop.Debugger.DebugCommands.SetNextStatement
- MonoDevelop.Debugger.DebugCommands.ShowNextStatement
- MonoDevelop.SourceEditor.SourceEditorCommands.NextIssue
- MonoDevelop.SourceEditor.SourceEditorCommands.PrevIssue
- MonoDevelop.SourceEditor.SourceEditorCommands.NextIssueError
- MonoDevelop.SourceEditor.SourceEditorCommands.PrevIssueError
- MonoDevelop.Refactoring.RefactoryCommands.GotoDeclaration
- MonoDevelop.Refactoring.RefactoryCommands.GotoImplementation
- MonoDevelop.Refactoring.Navigate.GotoBaseMember
- MonoDevelop.Refactoring.RefactoryCommands.FindReferences
- MonoDevelop.Refactoring.RefactoryCommands.FindAllReferences
- MonoDevelop.CSharp.Refactoring.FindProjectReferenceUsages
- MonoDevelop.CSharp.Navigation.FindExtensionMethods
- MonoDevelop.Refactoring.Navigation.FindBaseSymbols
- MonoDevelop.Refactoring.Navigation.FindDerivedSymbols
- MonoDevelop.CSharp.Navigation.FindMemberOverloads
- MonoDevelop.CSharp.Navigation.FindImplementingMembers
- MonoDevelop.VersionControl.Commands.Add
- MonoDevelop.VersionControl.Commands.Remove
- MonoDevelop.VersionControl.Commands.Diff
- MonoDevelop.VersionControl.Commands.Revert
- MonoDevelop.VersionControl.Commands.Log
- MonoDevelop.VersionControl.Commands.Status
- MonoDevelop.VersionControl.Commands.SolutionStatus
- MonoDevelop.VersionControl.Commands.Update
- MonoDevelop.VersionControl.Commands.UpdateSolution
- MonoDevelop.VersionControl.Commands.Checkout
- MonoDevelop.VersionControl.Commands.Lock
- MonoDevelop.VersionControl.Commands.Unlock
- MonoDevelop.VersionControl.Commands.Annotate
- MonoDevelop.VersionControl.Commands.Ignore
- MonoDevelop.VersionControl.Commands.CreatePatch
- MonoDevelop.VersionControl.Commands.Unignore
- MonoDevelop.VersionControl.Commands.ResolveConflicts
- MonoDevelop.VersionControl.Commands.RepositoryHistory
- MonoDevelop.VersionControl.Git.Commands.Push
- MonoDevelop.VersionControl.Git.Commands.ManageBranches
- MonoDevelop.VersionControl.Git.Commands.Merge
- MonoDevelop.VersionControl.Git.Commands.Rebase
- MonoDevelop.VersionControl.Git.Commands.Stash
- MonoDevelop.VersionControl.Git.Commands.StashPop
- MonoDevelop.VersionControl.Git.Commands.ManageStashes
- MonoDevelop.VersionControl.Git.Commands.InitializeRepository
- MonoDevelop.TextTemplating.Commands.Generate
- PerformanceDiagnosticsAddIn.StartStopListeningUIThreadMonitorHandler
- PerformanceDiagnosticsAddIn.ProfileFor5SecondsHandler
- PerformanceDiagnosticsAddIn.DumpLiveWidgetsHandler
- PerformanceDiagnosticsAddIn.ToggleProfileHandler
- PerformanceDiagnosticsAddIn.EnhanceSampleFile
- PerformanceDiagnosticsAddIn.EnhanceInstrumentsDeepCopy
- PerformanceDiagnosticsAddIn.DumpMemoryProbes
- PerformanceDiagnosticsAddIn.InduceUIThreadManagedException
- PerformanceDiagnosticsAddIn.InduceBGThreadManagedException
- PerformanceDiagnosticsAddIn.InduceUIThreadObjCException
- PerformanceDiagnosticsAddIn.InduceBGThreadObjCException
- PerformanceDiagnosticsAddIn.InduceHang
- PerformanceDiagnosticsAddIn.InduceNativePInvokeCrash
- PerformanceDiagnosticsAddIn.InduceStackOverflow
- PerformanceDiagnosticsAddIn.InduceUIDelay
- PerformanceDiagnosticsAddIn.InduceSigAbort
- PerformanceDiagnosticsAddIn.InduceSigSegv
- PerformanceDiagnosticsAddIn.NSViewException
- WebEditors.Languages.Html.WrapWithDiv
- MonoDevelop.Unity.Project.NodeBuilders.UnityFolderNodeCommands.AddNewMonoBehaviour
- MonoDevelop.Unity.Project.NodeBuilders.UnityFolderNodeCommands.AddNewEditorScript
- MonoDevelop.Unity.Project.NodeBuilders.UnityFolderNodeCommands.AddNewShader
- MonoDevelop.Unity.Project.NodeBuilders.UnityFolderNodeCommands.AddNewEnum
- MonoDevelop.Unity.Project.NodeBuilders.UnityFolderNodeCommands.AddNewClass
- MonoDevelop.Unity.Project.NodeBuilders.UnityFolderNodeCommands.AddNewFile
- MonoDevelop.Unity.Project.NodeBuilders.UnityFolderNodeCommands.AddNewInterface
- MonoDevelop.Unity.Project.NodeBuilders.UnityFolderNodeCommands.AddNewStruct
- MonoDevelop.Unity.Project.NodeBuilders.UnityFolderNodeCommands.AddNewFolder
- MonoDevelop.Unity.UI.UnityMessaging.UnityMessage
- MonoDevelop.Debugger.BreakpointPadCommands.GoToFile
- MonoDevelop.Debugger.ThreadsPadCommands.Pause
- MonoDevelop.Debugger.ThreadsPadCommands.Resume
- MonoDevelop.Debugger.StackTracePadCommands.ShowNameColumn
- MonoDevelop.Debugger.StackTracePadCommands.ShowFileColumn
- MonoDevelop.Debugger.StackTracePadCommands.ShowLanguageColumn
- MonoDevelop.Debugger.StackTracePadCommands.ShowAddressColumn
- MonoDevelop.Debugger.StackTracePadCommands.ShowExternalCode
- MonoDevelop.Debugger.StackTracePadCommands.ShowModuleNames
- MonoDevelop.Debugger.StackTracePadCommands.ShowParameterTypes
- MonoDevelop.Debugger.StackTracePadCommands.ShowParameterNames
- MonoDevelop.Debugger.StackTracePadCommands.ShowParameterValues
- MonoDevelop.Debugger.StackTracePadCommands.ShowLineNumbers
- MonoDevelop.Refactoring.RefactoryCommands.QuickFix
- MonoDevelop.Refactoring.RefactoryCommands.ImportSymbol
- MonoDevelop.AnalysisCore.AnalysisCommands.ExportRules
- MonoDevelop.Refactoring.AnalyzeWholeSolution
- MonoDevelop.Refactoring.AnalyzeSource
- MonoDevelop.Refactoring.AnalyzeCurrentProject
- MonoDevelop.CSharp.Refactoring.Commands.SortAndRemoveImports
- MonoDevelop.PackageManagement.Commands.AddPackages
- MonoDevelop.PackageManagement.Commands.ManageNuGetPackages
- MonoDevelop.PackageManagement.Commands.ManageNuGetPackagesInProject
- MonoDevelop.PackageManagement.Commands.RestorePackages
- MonoDevelop.PackageManagement.Commands.Restore
- MonoDevelop.PackageManagement.Commands.PackageReferenceNodeCommands.ReinstallPackage
- MonoDevelop.PackageManagement.Commands.PackageReferenceNodeCommands.UpdatePackage
- MonoDevelop.PackageManagement.Commands.UpdateAllPackagesInProject
- MonoDevelop.PackageManagement.Commands.UpdateAllPackagesInSolution
- MonoDevelop.PackageManagement.Commands.PackagesFolderNodeCommands.ReinstallAllPackagesInProject
- MonoDevelop.UnitTesting.Commands.TestCommands.DebugAllTests
- MonoDevelop.UnitTesting.Commands.TestCommands.RunAllTests
- MonoDevelop.UnitTesting.Commands.TestCommands.RunTest
- MonoDevelop.UnitTesting.Commands.TestCommands.ShowTestCode
- MonoDevelop.UnitTesting.Commands.TestCommands.GoToFailure
- MonoDevelop.UnitTesting.Commands.TestCommands.SelectTestInTree
- MonoDevelop.UnitTesting.Commands.TestCommands.ShowTestDetails
- MonoDevelop.UnitTesting.Commands.TestCommands.RerunTest
- MonoDevelop.UnitTesting.Commands.TestChartCommands.UseTimeScale
- MonoDevelop.UnitTesting.Commands.TestChartCommands.SingleDayResult
- MonoDevelop.UnitTesting.Commands.TestChartCommands.ShowResults
- MonoDevelop.UnitTesting.Commands.TestChartCommands.ShowTime
- MonoDevelop.UnitTesting.Commands.TestChartCommands.ShowSuccessfulTests
- MonoDevelop.UnitTesting.Commands.TestChartCommands.ShowFailedTests
- MonoDevelop.UnitTesting.Commands.TestChartCommands.ShowIgnoredTests
- MonoDevelop.UnitTesting.Commands.TextEditorCommands.RunTestAtCaret
- MonoDevelop.UnitTesting.Commands.TextEditorCommands.DebugTestAtCaret
- MonoDevelop.UnitTesting.Commands.TextEditorCommands.SelectTestAtCaret
- MonoDevelop.UnitTesting.Commands.TestCommands.RunTestsInFile
- MonoDevelop.UnitTesting.Commands.TestCommands.DebugTestsInFile
- Xamarin.Ide.Accounts.AccountCommands.MicrosoftIdentities
- MonoDevelop.MacDev.AssetEditor.AssetFolderCommands.OpenAssetFolder
- MonoDevelop.MacDev.NativeReferences.NativeReferenceCommands.Add
- MonoDevelop.AspNet.Commands.AspNetCommands.AddController
- MonoDevelop.AspNet.Commands.AspNetCommands.AddView
- MonoDevelop.AspNet.Commands.AspNetCommands.GoToView
- MonoDevelop.AspNet.Commands.AspNetCommands.AddViewFromController
- MonoDevelop.AspNet.Commands.AspNetCommands.GoToController
- MonoDevelop.Xml.Editor.XmlCommands.CreateSchema
- MonoDevelop.Xml.Editor.XmlCommands.Validate
- MonoDevelop.Xml.Editor.XmlCommands.AssignStylesheet
- MonoDevelop.Xml.Editor.XmlCommands.OpenStylesheet
- MonoDevelop.Xml.Editor.XmlCommands.RunXslTransform
- MonoDevelop.Xml.Editor.XmlCommands.GoToSchemaDefinition
- MonoDevelop.Docker.Commands.AddDockerSupport
- Xamarin.AndroidDesigner.AndroidPlatformCommands.HighlightContainers
- Xamarin.AndroidDesigner.AndroidPlatformCommands.ZoomInDesigner
- Xamarin.AndroidDesigner.AndroidPlatformCommands.ZoomOutDesigner
- Xamarin.AndroidDesigner.AndroidPlatformCommands.ZoomFitDesigner
- Xamarin.AndroidDesigner.AndroidPlatformCommands.ZoomFullDesigner
- Xamarin.AndroidDesigner.AndroidPlatformCommands.ShowGrid
- Xamarin.AndroidDesigner.AndroidPlatformCommands.SetFocusToToolbar
- Xamarin.AndroidDesigner.AndroidPlatformCommands.SetFocusToZoomBar
- Xamarin.AndroidDesigner.AndroidPlatformCommands.SetFocusToSideBar
- Microsoft.VisualStudio.FSharp.Editor.FSharpCommands.SendFile
- Microsoft.VisualStudio.FSharp.Editor.FSharpCommands.SendSelection
- Microsoft.VisualStudio.FSharp.Editor.FSharpCommands.SendLine
- Microsoft.VisualStudio.FSharp.Editor.FSharpCommands.SendReferences
- Microsoft.VisualStudio.FSharp.Editor.FSharpCommands.RestartFsi
- Microsoft.VisualStudio.FSharp.Editor.FSharpCommands.ClearFsi
- Microsoft.VisualStudioMac.AddinMaker.AddinCommands.AddAddinReference
- MonoDevelop.AzureFunctions.Commands.AddFunction
- Xamarin.Terminal.TerminalCommands.OpenInTerminalPad
- Xamarin.Terminal.TerminalCommands.CreateNewTerminalPad
- Xamarin.Terminal.TerminalCommands.ToggleTerminalPad
- VsVim.ShowPadById
- VsVim.ShowPadByTitle
- Pad|MonoDevelop.Ide.Gui.Pads.ErrorListPad
- Pad|MonoDevelop.Ide.Gui.Pads.BuildOutputPad
- Pad|MonoDevelop.Ide.Gui.Pads.TaskListPad
- Pad|ProjectPad
- Pad|MonoDevelop.DesignerSupport.ToolboxPad
- Pad|MonoDevelop.DesignerSupport.PropertyPad
- Pad|MonoDevelop.DesignerSupport.DocumentOutlinePad
- Pad|MonoDevelop.Debugger.BreakpointPad
- Pad|MonoDevelop.Debugger.LocalsPad
- Pad|MonoDevelop.Debugger.WatchPad
- Pad|MonoDevelop.Debugger.ImmediatePad
- Pad|MonoDevelop.Debugger.StackTracePad
- Pad|MonoDevelop.Debugger.ThreadsPad
- Pad|Xamarin.HotReload.LiveVisualTreePad
- Pad|MonoDevelop.UnitTesting.TestPad
- Pad|MonoDevelop.UnitTesting.TestResultsPad
- Pad|Xamarin.Ide.DeviceLogging.DeviceLogPad
- Pad|GitStatusView
- Pad|FSharp.Editor.FSharpInteractivePad
- Pad|Xamarin.Terminal.TerminalPad
- Pad|OutputPad-Vim Output-0
- Pad|OutputPad-PackageConsole-0
- Pad|SearchPad - Search Results - 0