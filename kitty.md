# Mappable Actions

The actions described below can be mapped to any key press or mouse action using the `map` and `mouse_map` directives in `kitty.conf`. For configuration examples, see the default shortcut links for each action. To read about keyboard mapping in more detail, see [Making your keyboard dance](https://www.google.com/search?q=kitty+Making+your+keyboard+dance).

---

## Copy/Paste

* **clear\_selection**: Clear the current selection.
* **copy\_and\_clear\_or\_interrupt**: Copy the selected text from the active window to the clipboard and clear selection; if no selection, send SIGINT (aka `ctrl+c`).
* **copy\_ansi\_to\_clipboard**: Copy the selected text from the active window to the clipboard with ANSI formatting codes.
* **copy\_or\_interrupt**: Copy the selected text from the active window to the clipboard; if no selection, send SIGINT (aka `ctrl+c`).
* **copy\_to\_clipboard**: Copy the selected text from the active window to the clipboard.
    * Default shortcuts using this action: `ctrl+shift+c`
* **pass\_selection\_to\_program**: Pass the selected text from the active window to the specified program.
    * Default shortcuts using this action: `ctrl+shift+o`
* **paste**: Paste the specified text into the current window. ANSI C escapes are decoded.
* **show\_first\_command\_output\_on\_screen**: Show output from the first shell command on screen in a pager like `less`.
    * Requires **Shell integration** to work.
* **show\_last\_command\_output**: Show output from the last shell command in a pager like `less`.
    * Requires **Shell integration** to work.
    * Default shortcuts using this action: `ctrl+shift+g`
* **show\_last\_non\_empty\_command\_output**: Show the last non-empty output from a shell command in a pager like `less`.
    * Requires **Shell integration** to work.
* **show\_last\_visited\_command\_output**: Show the first command output below the last scrolled position via `scroll_to_prompt` or the last mouse clicked command output in a pager like `less`.
    * Requires **Shell integration** to work.
* **show\_scrollback**: Show scrollback in a pager like `less`.
    * Default shortcuts using this action: `ctrl+shift+h`
* **copy\_to\_buffer**: Copy the selection from the active window to the specified buffer.
    * See **Multiple copy/paste buffers** for details.
* **paste\_from\_buffer**: Paste from the specified buffer to the active window.
    * See **Multiple copy/paste buffers** for details.
* **paste\_from\_clipboard**: Paste from the clipboard to the active window.
    * Default shortcuts using this action: `ctrl+shift+v`
* **paste\_from\_selection**: Paste from the primary selection, if present, otherwise the clipboard to the active window.
    * Default shortcuts using this action: `ctrl+shift+s`

---

## Debugging

* **dump\_lines\_with\_attrs**: Show a dump of the current lines in the scrollback + screen with their line attributes.
* **close\_shared\_ssh\_connections**: Close all shared SSH connections.
    * See **share\_connections** for details.
* **debug\_config**: Show the effective configuration kitty is running with.
    * Default shortcuts using this action: `ctrl+shift+f6`
* **show\_kitty\_env\_vars**: Show the environment variables that the kitty process sees.
* **simulate\_color\_scheme\_preference\_change**: Simulate a change in OS color scheme preference.

---

## Layouts

* **goto\_layout**: Switch to the named layout.
    In case there are multiple layouts with the same name and different options, specify the full layout definition or a unique prefix of the full definition.
    For example:
    ```
    map f1 goto_layout tall
    map f2 goto_layout fat:bias=20
    ```
* **last\_used\_layout**: Go to the previously used layout.
* **layout\_action**: Perform a layout specific action. See **Arrange windows** for details.
* **next\_layout**: Go to the next enabled layout. Can optionally supply an integer to jump by the specified number.
    * Default shortcuts using this action: `ctrl+shift+l`
* **toggle\_layout**: Toggle the named layout.
    Switches to the named layout if another layout is current, otherwise switches to the last used layout. Useful to "zoom" a window temporarily by switching to the stack layout. For example:
    ```
    map f1 toggle_layout stack
    ```

---

## Marks

* **remove\_marker**: Remove a previously created marker.
* **scroll\_to\_mark**: Scroll to the next or previous mark of the specified type.
* **toggle\_marker**: Toggle the current marker on/off.
* **create\_marker**: Create a new marker.

---

## Miscellaneous

* **send\_key**: Send the specified keys to the active window.
    Note that the key will be sent only if the current keyboard mode of the program running in the terminal supports it. Both key press and key release are sent. First presses for all specified keys and then releases in reverse order. To send a pattern of press and release for multiple keys use the `combine` action. For example:
    ```
    map f1 send_key ctrl+x alt+y
    map f1 combine : send_key ctrl+x : send_key alt+y
    ```
* **send\_text**: Send the specified text to the active window.
    * See **send\_text** for details.
    * Default shortcuts using this action: `ctrl+shift+alt+h`
* **show\_kitty\_doc**: Display the specified kitty documentation, preferring a local copy, if found.
    For example:
    ```
    # show the config docs
    map f1 show_kitty_doc conf
    # show the ssh kitten docs
    map f1 show_kitty_doc kittens/ssh
    ```
    * Default shortcuts using this action: `ctrl+shift+f1`
* **signal\_child**: Send the specified SIGNAL to the foreground process in the active window.
    For example:
    ```
    map f1 signal_child SIGTERM
    ```
* **clear\_terminal**: Clear the terminal.
    See **reset\_terminal** for details. For example:
    ```
    # Reset the terminal
    map f1 clear_terminal reset active
    # Clear the terminal screen by erasing all contents
    map f1 clear_terminal clear active
    # Clear the terminal scrollback by erasing it
    map f1 clear_terminal scrollback active
    # Scroll the contents of the screen into the scrollback
    map f1 clear_terminal scroll active
    # Clear everything on screen up to the line with the cursor or the start of the current prompt (needs shell integration)
    # Useful for clearing the screen up to the shell prompt and moving the shell prompt to the top of the screen.
    map f1 clear_terminal to_cursor active
    # Same as above except cleared lines are moved into scrollback
    map f1 clear_terminal to_cursor_scroll active
    ```
    * Default shortcuts using this action: `cmd+ctrl+l`, `option+cmd+k`, `cmd+k`, `ctrl+shift+delete`
* **combine**: Combine multiple actions and map to a single keypress.
    The syntax is:
    `map key combine <separator> action1 <separator> action2 <separator> action3 ...`
    For example:
    ```
    map kitty_mod+e combine : new_window : next_layout
    map kitty_mod+e combine | new_tab | goto_tab -1
    ```
* **disable\_ligatures\_in**: Turn on/off ligatures in the specified window.
    * See **disable\_ligatures** for details.
* **discard\_event**: Discard this event completely ignoring it.
* **edit\_config\_file**: Edit the `kitty.conf` config file in your favorite text editor.
    * Default shortcuts using this action: `ctrl+shift+f2`
* **hide\_macos\_app**: Hide macOS kitty application.
    * Default shortcuts using this action: `cmd+h`
* **hide\_macos\_other\_apps**: Hide macOS other applications.
    * Default shortcuts using this action: `opt+cmd+h`
* **input\_unicode\_character**: Input an arbitrary unicode character. See **Unicode input** for details.
* **kitten**: Run the specified kitten. See **Custom kittens** for details.
    * Default shortcuts using this action:
        * Hints - `ctrl+shift+p>h` Insert selected hash
        * Hints - `ctrl+shift+p>l` Insert selected line
        * Hints - `ctrl+shift+p>f` Insert selected path
        * Hints - `ctrl+shift+p>w` Insert selected word
        * Hints - `ctrl+shift+p>shift+f` Open selected path
        * Hints - `ctrl+shift+p>n` Open the selected file at the selected line
        * Hints - `ctrl+shift+p>y` Open the selected hyperlink
        * Unicode input - `ctrl+shift+u` Unicode input
* **kitty\_shell**: Run the kitty shell to control kitty with commands.
    * Default shortcuts using this action: `ctrl+shift+escape`
* **launch**: Launch the specified program in a new window/tab/etc.
    * See **The launch command** for details.
* **load\_config\_file**: Reload the config file.
    If mapped without arguments reloads the default config file, otherwise loads the specified config files, in order. Loading a config file **replaces** all config options. For example:
    ```
    map f5 load_config_file /path/to/some/kitty.conf
    ```
    * Default shortcuts using this action: `ctrl+shift+f5`
* **minimize\_macos\_window**: Minimize macOS window.
    * Default shortcuts using this action: `cmd+m`
* **open\_url**: Open the specified URL.
    * Default shortcuts using this action: `shift+cmd+/`
* **open\_url\_with\_hints**: Click a URL using the keyboard.
    * Default shortcuts using this action: `ctrl+shift+e`
* **pop\_keyboard\_mode**: End the current keyboard mode switching to the previous mode.
* **push\_keyboard\_mode**: Switch to the specified keyboard mode, pushing it onto the stack of keyboard modes.
* **remote\_control**: Run a remote control command without needing to allow remote control.
    For example:
    ```
    map f1 remote_control set-spacing margin=30
    ```
    * See **Mapping key presses to remote control commands** for details.
* **remote\_control\_script**: Run a remote control script without needing to allow remote control.
    For example:
    ```
    map f1 remote_control_script /path/to/script arg1 arg2 ...
    ```
    * See **Mapping key presses to remote control commands** for details.
* **set\_colors**: Change colors in the specified windows.
    For details, see **kitten @ set-colors**. For example:
    ```
    map f5 set_colors --configured /path/to/some/config/file/colors.conf
    ```
* **show\_error**: Show an error message with the specified title and text.
* **sleep**: Sleep for the specified time period. Suffix can be `s` for seconds, `m` for minutes, `h` for hours and `d` for days. The time can be fractional.
* **toggle\_macos\_secure\_keyboard\_entry**: Toggle macOS secure keyboard entry.
    * Default shortcuts using this action: `opt+cmd+s`
* **no\_op**: Unbind a shortcut.
    Mapping a shortcut to `no_op` causes kitty to not intercept the key stroke anymore, instead passing it to the program running inside it.

---

## Mouse Actions

* **mouse\_click\_url**: Click the URL under the mouse.
* **mouse\_click\_url\_or\_select**: Click the URL under the mouse only if the screen has no selection.
* **mouse\_handle\_click**: Handle a mouse click.
    Try to perform the specified actions one after the other till one of them is successful. Supported actions are:
    * `selection` - check for a selection and if one exists abort processing
    * `link` - if a link exists under the mouse, click it
    * `prompt` - if the mouse click happens at a shell prompt move the cursor to the mouse location
    For examples, see **Mouse actions**.
* **mouse\_select\_command\_output**: Select clicked command output.
    * Requires **Shell integration** to work.
* **mouse\_selection**: Manipulate the selection based on the current mouse position.
    For examples, see **Mouse actions**.
* **mouse\_show\_command\_output**: Show clicked command output in a pager like `less`.
    * Requires **Shell integration** to work.
* **paste\_selection**: Paste the current primary selection.
* **paste\_selection\_or\_clipboard**: Paste the current primary selection or the clipboard if no selection is present.

---

## Scrolling

* **scroll\_end**: Scroll to the bottom of the scrollback buffer when in main screen.
    * Default shortcuts using this action: `ctrl+shift+end`
* **scroll\_home**: Scroll to the top of the scrollback buffer when in main screen.
    * Default shortcuts using this action: `ctrl+shift+home`
* **scroll\_line\_down**: Scroll down by one line when in main screen. To scroll by different amounts, you can map the `remote_control scroll-window` action.
    * Default shortcuts using this action: `ctrl+shift+down`
* **scroll\_line\_up**: Scroll up by one line when in main screen. To scroll by different amounts, you can map the `remote_control scroll-window` action.
    * Default shortcuts using this action: `ctrl+shift+up`
* **scroll\_page\_down**: Scroll down by one page when in main screen. To scroll by different amounts, you can map the `remote_control scroll-window` action.
    * Default shortcuts using this action: `ctrl+shift+page_down`
* **scroll\_page\_up**: Scroll up by one page when in main screen. To scroll by different amounts, you can map the `remote_control scroll-window` action.
    * Default shortcuts using this action: `ctrl+shift+page_up`
* **scroll\_prompt\_to\_bottom**: Scroll prompt to the bottom of the screen, filling in extra lines from the scrollback buffer, when in main screen.
* **scroll\_prompt\_to\_top**: Scroll prompt to the top of the screen, filling screen with empty lines, when in main screen. To avoid putting the lines above the prompt into the scrollback use `scroll_prompt_to_top y`.
* **scroll\_to\_prompt**: Scroll to the previous/next shell command prompt.
    Allows easy jumping from one command to the next. Requires working **Shell integration**. Takes a single, optional, number as argument which is the number of prompts to jump, negative values jump up and positive values jump down. A value of zero will jump to the last prompt visited by this action. For example:
    ```
    map ctrl+p scroll_to_prompt -1  # jump to previous
    map ctrl+n scroll_to_prompt 1   # jump to next
    map ctrl+o scroll_to_prompt 0   # jump to last visited
    ```
    * Default shortcuts using this action: `ctrl+shift+x`, `ctrl+shift+z`

---

## Tab Management

* **close\_other\_tabs\_in\_os\_window**: Close all the tabs in the current OS window other than the currently active tab.
* **close\_tab**: Close the current tab.
    * Default shortcuts using this action: `ctrl+shift+q`
* **detach\_tab**: Detach a tab, moving it to another OS Window.
    * See **detaching windows** for details.
* **goto\_tab**: Go to the specified tab, by number, starting with 1.
    Zero and negative numbers go to previously active tabs. Use the `select_tab` action to interactively select a tab to go to.
* **move\_tab\_backward**: Move the active tab backward.
    * Default shortcuts using this action: `ctrl+shift+,`
* **move\_tab\_forward**: Move the active tab forward.
    * Default shortcuts using this action: `ctrl+shift+.`
* **new\_tab**: Create a new tab.
    * Default shortcuts using this action: `ctrl+shift+t`
* **new\_tab\_with\_cwd**: Create a new tab with working directory for the window in it set to the same as the active window.
* **next\_tab**: Make the next tab active.
    * Default shortcuts using this action: `ctrl+shift+right`
* **previous\_tab**: Make the previous tab active.
    * Default shortcuts using this action: `ctrl+shift+left`
* **select\_tab**: Interactively select a tab to switch to.
* **set\_tab\_title**: Change the title of the active tab interactively, by typing in the new title.
    If you specify an argument to this action then that is used as the title instead of asking for it. Use the empty string (`""`) to reset the title to default. Use a space (`" "`) to indicate that the prompt should not be pre-filled. For example:
    ```
    # interactive usage
    map f1 set_tab_title
    # set a specific title
    map f2 set_tab_title some title
    # reset to default
    map f3 set_tab_title ""
    # interactive usage without prefilled prompt
    map f3 set_tab_title " "
    ```
    * Default shortcuts using this action: `ctrl+shift+alt+t`

---

## Window Management

* **set\_window\_title**: Change the title of the active window interactively, by typing in the new title.
    If you specify an argument to this action then that is used as the title instead of asking for it. Use the empty string (`""`) to reset the title to default. Use a space (`" "`) to indicate that the prompt should not be pre-filled. For example:
    ```
    # interactive usage
    map f1 set_window_title
    # set a specific title
    map f2 set_window_title some title
    # reset to default
    map f3 set_window_title ""
    # interactive usage without prefilled prompt
    map f3 set_window_title " "
    ```
* **close\_other\_windows\_in\_tab**: Close all windows in the tab other than the currently active window.
* **eighth\_window**: Focus the eighth window.
    * Default shortcuts using this action: `ctrl+shift+8`
* **fifth\_window**: Focus the fifth window.
    * Default shortcuts using this action: `ctrl+shift+5`
* **first\_window**: Focus the first window.
    * Default shortcuts using this action: `ctrl+shift+1`
* **focus\_visible\_window**: Focus a visible window by pressing the number of the window. Window numbers are displayed over the windows for easy selection in this mode. See **visual\_window\_select\_characters**.
    * Default shortcuts using this action: `ctrl+shift+f7`
* **fourth\_window**: Focus the fourth window.
    * Default shortcuts using this action: `ctrl+shift+4`
* **move\_window**: Move the window in the specified direction.
    For example:
    ```
    map ctrl+left move_window left
    map ctrl+down move_window bottom
    ```
* **move\_window\_backward**: Move active window backward (swap it with the previous window).
    * Default shortcuts using this action: `ctrl+shift+b`
* **move\_window\_forward**: Move active window forward (swap it with the next window).
    * Default shortcuts using this action: `ctrl+shift+f`
* **move\_window\_to\_top**: Move active window to the top (make it the first window).
    * Default shortcuts using this action: `ctrl+shift+\``
* **neighboring\_window**: Focus the neighboring window in the current tab.
    For example:
    ```
    map ctrl+left neighboring_window left
    map ctrl+down neighboring_window bottom
    ```
* **next\_window**: Focus the next window in the current tab.
    * Default shortcuts using this action: `ctrl+shift+]`
* **ninth\_window**: Focus the ninth window.
    * Default shortcuts using this action: `ctrl+shift+9`
* **nth\_window**: Focus the nth window if positive or the previously active windows if negative. When the number is larger than the number of windows focus the last window. For example:
    ```
    # focus the previously active window
    map ctrl+p nth_window -1
    # focus the first window
    map ctrl+1 nth_window 0
    ```
* **previous\_window**: Focus the previous window in the current tab.
    * Default shortcuts using this action: `ctrl+shift+[`
* **reset\_window\_sizes**: Reset window sizes undoing any dynamic resizing of windows.
* **resize\_window**: Resize the active window by the specified amount.
    * See **Resizing windows** for details.
* **second\_window**: Focus the second window.
    * Default shortcuts using this action: `ctrl+shift+2`
* **seventh\_window**: Focus the seventh window.
    * Default shortcuts using this action: `ctrl+shift+7`
* **sixth\_window**: Focus the sixth window.
    * Default shortcuts using this action: `ctrl+shift+6`
* **swap\_with\_window**: Swap the current window with another window in the current tab, selected visually. See **visual\_window\_select\_characters**.
    * Default shortcuts using this action: `ctrl+shift+f8`
* **tenth\_window**: Focus the tenth window.
    * Default shortcuts using this action: `ctrl+shift+0`
* **third\_window**: Focus the third window.
    * Default shortcuts using this action: `ctrl+shift+3`
* **change\_font\_size**: Change the font size for the current or all OS Windows.
    * See **Font sizes** for details.
    * Default shortcuts using this action: `ctrl+shift+minus`, `ctrl+shift+equal`, `ctrl+shift+backspace`
* **close\_os\_window**: Close the currently active OS Window.
    * Default shortcuts using this action: `shift+cmd+w`
* **close\_other\_os\_windows**: Close all other OS Windows other than the OS Window containing the currently active window.
* **close\_window**: Close the currently active window.
    * Default shortcuts using this action: `ctrl+shift+w`
* **close\_window\_with\_confirmation**: Close window with confirmation.
    Asks for confirmation before closing the window. If you don't want the confirmation when the window is sitting at a shell prompt (requires **Shell integration**), use:
    ```
    map f1 close_window_with_confirmation ignore-shell
    ```
* **detach\_window**: Detach a window, moving it to another tab or OS Window.
    * See **detaching windows** for details.
* **new\_os\_window**: New OS Window.
    * Default shortcuts using this action: `ctrl+shift+n`
* **new\_os\_window\_with\_cwd**: New OS Window with the same working directory as the currently active window.
* **new\_window**: Create a new window.
    * Default shortcuts using this action: `ctrl+shift+enter`
* **new\_window\_with\_cwd**: Create a new window with working directory same as that of the active window.
* **nth\_os\_window**: Focus the nth OS window if positive or the previously active OS windows if negative. When the number is larger than the number of OS windows focus the last OS window. A value of zero will refocus the currently focused OS window, this is useful if focus is not on any kitty OS window at all, however, it will only work if the window manager allows applications to grab focus. For example:
    ```
    # focus the previously active kitty OS window
    map ctrl+p nth_os_window -1
    # focus the current kitty OS window (grab focus)
    map ctrl+0 nth_os_window 0
    # focus the first kitty OS window
    map ctrl+1 nth_os_window 1
    # focus the last kitty OS window
    map ctrl+1 nth_os_window 999
    ```
* **quit**: Quit, closing all windows.
    * Default shortcuts using this action: `cmd+q`
* **set\_background\_opacity**: Set the background opacity for the active OS Window.
    For example:
    ```
    map f1 set_background_opacity +0.1
    map f2 set_background_opacity -0.1
    map f3 set_background_opacity 0.5
    ```
    * Default shortcuts using this action: `ctrl+shift+a>l`, `ctrl+shift+a>1`, `ctrl+shift+a>m`, `ctrl+shift+a>d`
* **start\_resizing\_window**: Resize the active window interactively.
    * See **Resizing windows** for details.
    * Default shortcuts using this action: `ctrl+shift+r`
* **toggle\_fullscreen**: Toggle the fullscreen status of the active OS Window.
    * Default shortcuts using this action: `ctrl+shift+f11`
* **toggle\_maximized**: Toggle the maximized status of the active OS Window.
    * Default shortcuts using this action: `ctrl+shift+f10`
* **toggle\_tab**: Toggle to the tab matching the specified expression.
    Switches to the matching tab if another tab is current, otherwise switches to the last used tab. Useful to easily switch to and back from a tab using a single shortcut. Note that toggling works only between tabs in the same OS window. See **Matching windows and tabs** for details on the match expression. For example:
    ```
    map f1 toggle_tab title:mytab
    ```
