---
layout: subdoc
title: Proprietary Escape Codes - Documentation - iTerm2 - Mac OS Terminal Replacement
active-state: documentation
subhead: Proprietary Escape Codes
---
iTerm2 supports several non-standard escape codes. These may not work properly in tmux or screen, and may have unknown effects on other terminal emulators. Proceed with caution.
<h6 class="question">Set cursor shape</h6>
    ^[]50;CursorShape=N^G
where N=0, 1, or 2.
<ul>
        <li>0: Block</li>
        <li>1: Vertical bar</li>
        <li>2: Underline</li>
</ul>
Add this to your .vimrc to change cursor shape in insert mode:
    let &t_SI = "\<Esc>]50;CursorShape=1\x7" 
    let &t_EI = "\<Esc>]50;CursorShape=0\x7"
This is derived from <a href="http://vim.wikia.com/wiki/Change_cursor_shape_in_different_modes">Konsole</a>.
<h6 class="question">Set Mark</h6>
The "Set Mark" (cmd-shift-M) command allows you to record a location and then jump back to it later (with cmd-shift-J). The following escape code has the same effect as that command:

    ^[]50;SetMark^G

<h6 class="question">Steal Focus</h6>
To bring iTerm2 to the foreground:

    ^[]50;StealFocus^G

<h6 class="question">Clear Scrollback History</h6>
To erase the scrollback history:

    ^[]50;ClearScrollback^G

<h6 class="question">Set curent directory</h6>
To inform iTerm2 of the current directory to help semantic history:

    ^[]50;CurrentDir=/the/current/directory^G

<h6 class="question">Change profile</h6>
To change the session's profile on the fly:

    ^[]50;SetProfile=NewProfileName^G

<h6 class="question">Copy to clipboard</h6>
To place text in the pasteboard:

    ^[]50;CopyToClipboard=name^G

Where name is one of "rule", "find", "font", or empty to mean the general pasteboard (which is what you normally want). After this is sent, all text received is placed in the pasteboard until this code comes in:

    ^[]50;EndCopy^G

<h6 class="question">Set window title and tab chrome background color</h6>
To set the window title and tab color use this escape sequence:

    ^[]6;1;bg;red;brightness;N^G 
    ^[]6;1;bg;green;brightness;N^G 
    ^[]6;1;bg;blue;brightness;N^G

Replace N with a decimal value in 0 to 255.

Example in bash that turns the background purple:

    echo -e "\033]6;1;bg;red;brightness;255\a" 
    echo -e "\033]6;1;bg;green;brightness;0\a" 
    echo -e "\033]6;1;bg;blue;brightness;255\a"

<h6 class="question">Change the color palette</h6>
    ^[]Pnrrggbb^[\
Replace "n" with:
<ul>
        <li>0-f (hex) = ansi color</li>
        <li>g = foreground</li>
        <li>h = background</li>
        <li>i = bold color</li>
        <li>j = selection color</li>
        <li>k = selected text color</li>
        <li>l = cursor</li>
        <li>m = cursor text</li>
</ul>
rr, gg, bb are 2-digit hex value (for example, "ff").
Example in bash that changes the foreground color blue:

    echo -e "\033]Pg4040ff\033\\"