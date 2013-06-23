ASCII control characters are chars with the numeric value of [0-31].  They are meant for control operations such as back space, bell, escape, etc ...  They are not textual operations and have no character associated with them.  In a normal Visual Studio editor they are invisible and lead to confusing error messages.  

VsVim will display ASCII control characters in the same way as gVim does.  By using the `^B` notation where `^` indicates a control character followed by the control code letter 

This behavior can be disabled by toggling the `vsvim_controlchars` setting

    :set novsvim_controlchars