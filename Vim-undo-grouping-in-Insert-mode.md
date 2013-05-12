Reverse-engineered rules for Vim undo grouping in Insert mode, written for [Issue #1096](https://github.com/jaredpar/VsVim/issues/1096):

I’ve experimented by typing in Insert mode, and I’ve come up with a simple set of rules that, as far as I can tell, correctly and completely predicts how Vim will group undos.

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
- Setting the value of `undolevels`
	- see `:help :undojoin`

These actions start and end their own group:
- A deletion with `<C-O>d`

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