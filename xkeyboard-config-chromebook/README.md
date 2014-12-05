#xkeyboard-config-chromebook

xkeyboard-config with custom mapping for Chromebooks.

###Chromebook tweaks
* F1-F3,F6-F10 keys mapped to the same keysyms as in ChromeOS.
* F5 mapped to Print keysym (PrintScreen key).
* `English(US, Chromebook)` layout was added as a replacement of `English(US)` layout with Alt_R mapped to AltGR.
* Alt+Shift+Arrows (Up, Down, Left, Right) mapped to [the same keysyms as Alt[+Ctrl]+Arrows in ChromeOS](https://support.google.com/chromebook/answer/1047364?hl=en) (PgUp, PgDown, Home, End).
* AltGR+Arrows (Up, Down, Left, Right) mapped to [the same keysyms as Alt[+Ctrl]+Arrows in ChromeOS](https://support.google.com/chromebook/answer/1047364?hl=en) (PgUp, PgDown, Home, End).
* AltGR+Backspace mapped to Delete.

###Benefits
* F1-F10 keysyms with modifiers are the same (e.g. ALT+F4 still close a window).
* Get the keysyms of F1-F10 with AltGR (e.g. AltGR+F2 for rename in Nautilus).
* Suitable when multiple layouts are used (superior to xmodmap as its settings purged when changing layout/language).
* Works with GTK3 apps like Epiphany and Nautilus (xbindkeys+xvkbd doesn't).
* Gnome's [drop-down-terminal extension](https://extensions.gnome.org/extension/442/drop-down-terminal): get the backtick/grave character with AltGR+` on the English (US, Chromebook) layout.
* Works well in Gnome Wayland session.

###Known limitations
* Chromium and Firefox aren't respecting AltGR and not Alt+Shift mapping. AltGR+Arrows and Alt+Shift+Arrows (PgUp, PgDown, Home, End) not working properly for navigation in Chromium and Firefox but do work when writing in a text box with these applications, it also works in any other application (perfect in Epiphany).
* Alt+Shift+Down hotkey (set as `PgUp`) conflicts with Nautilus hotkey mapping to the action `OpenCloseParent`. It's recommended to clear the hotkey mapping by adding the following line to `~/.config/nautilus/accels`.
```
(gtk_accel_path "<Actions>/DirViewActions/OpenCloseParent" "")
```
* Our AltGR+Right hotkey (set as `End`) conflicts with Gnome's Super+End hotkey (set as `Switch to last workspace`), when pressing Super+Right instead of attaching the focused application to the right of the screen (`Toggle tiled right`) it switch to the last workspace. for now please disable the hotkey via `Settings->Keyboard->Shortcuts->Navigation` (press Backspace to disable a hotkey).  
* Firefox doesn't respect XF86Reload (F3 key set as Reload). If Firefox is your default browser then you can comment out the patch that set F3 as XF86Reload and use another method to set it as 'Ctrl+R', see example in [xbindkeys_sample](xbindkeys_sample).  

###Other recommended hotkeys tweaks 
*  Nautilus: set Alt+Backspace as send-to-trash action and Shift+Backspace as delete by adding the following lines to `~/.config/nautilus/accels`.
```
(gtk_accel_path "<Actions>/DirViewActions/Trash" "<Alt>BackSpace")
(gtk_accel_path "<Actions>/DirViewActions/Delete" "<Shift>BackSpace")
```
* Chromium:  
With the extension [Hotkeys](https://chrome.google.com/webstore/detail/mmbiohbmijkiimgcgijfomelgpmdiigb) map Ctrl+Arrows to [the same actions as the Alt[+Ctrl]+Arrows in ChromeOS](https://support.google.com/chromebook/answer/1047364?hl=en) (preferable as Alt+Left/Right already used for Back/Forward).
* Firefox:
    1. Install the extension [Key Config](https://addons.mozilla.org/en-us/firefox/addon/key-config).
    2. Extract the file keyconfig.js from the xpi package (it's just a zip) and open it, replace the two occurence of the function of scrollByLine to scrollByPages and limit the argument to 1.
    3. Update the xpi with our keyconfig.js.
    4. Start Firefox and map Ctrl+Arrows to [the same actions as the Alt[+Ctrl]+Arrows in ChromeOS](https://support.google.com/chromebook/answer/1047364?hl=en) (preferable as Alt+Left/Right already used for Back/Forward).
* Xbindkeys:  
Sample configuration file is supplied ([xbindkeys_sample](xbindkeys_sample)) as users might like having extra hotkeys (I don't).  
The main difference between the sample config to ChromeOS is the use of Ctrl+Arrows instead of Alt+Arrows.  
