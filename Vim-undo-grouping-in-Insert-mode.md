Reverse-engineered rules for Vim undo grouping in Insert mode, written for [Issue #1096](https://github.com/jaredpar/VsVim/issues/1096):

I’ve come up with a simple set of rules that, as far as I can tell, correctly and completely predicts how Vim will group undos. I reverse-engineered these rules through experimentation and reading `undo.txt` in Vim’s help. I experimented by typing in Insert mode and then undoing that typing step by step. If you find that some behavior is missing, feel free to add it to this page.

These actions continue a group:
- just typing a character, like ‘a’ or ‘%’
- Enter
- Backspace
- Delete (forward delete)

These actions start a new group:
- moving the cursor somewhere else and typing
	- moving, for instance, to a different line, to the beginning of the line, or one character back
	- using e.g. the cursor keys, Home, End, `<C-O>` followed by a motion, etc.
- `<C-G>u`
	- see `:help :undojoin`
- setting the value of `undolevels`
	- see `:help :undojoin`

These actions start and end their own group:
- deletion over a motion with `<C-O>d`
- changing case over a motion with `<C-O>g~`
- `<C-O><C-E>` to scroll
- probably a bunch of other `<C-O>` commands - but not, at least, the motion-only ones

### Example

<dl>
<dt>what you type in Insert mode (with special keys Vim-escaped)</dt>
<dd><code>one &lt;Home&gt;two &lt;Home&gt;trh&lt;BS&gt;&lt;BS&gt;hree&lt;CR&gt;&lt;C-O&gt;$four</code></dd>
<dt>the result</dt>
<dd><pre>three
two one four</pre></dd>
<dt>the groups (represented as the strings they type; location not encoded)</dt>
<dd><code>["one ", "two ", "three\n", " four"]</code><dd>
</dl>