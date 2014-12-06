#Staging branch remarks

This branch includes a solution so the mapping of alt+shift+arrows will work also in Chromium, Firefox and LibreOffice.

Notice that this solution is a little bit buggy, when holding the alt+shift+arrows hotkeys for a long period of time the system will stop responding to the hotkey and it will take a few seconds for any key press to register.

Auto repeating is also broken so you will need to set it manually by adding the following to your `.xinitrc` (or other autostart method) to get back repeats of arrows keys
```
xset r 111
xset r 113
xset r 114
xset r 116
```

This solution is only for an Xorg session, it won't work in a Wayland session because [libxkcommon](https://github.com/xkbcommon/libxkbcommon) doesn't support it, I opened a [feature request for adding the RedirectKey action](https://github.com/xkbcommon/libxkbcommon/issues/18), please show your support by posting there.


ATM I decided to keep this solution in a separated branch as I've got no idea if these issues will ever be fixed in xorg-server and because that RedirectKey doesn't work in a Wayland session.

#xkeyboard-config-chromebook

xkeyboard-config with custom mapping for Chromebooks.

###Chromebook tweaks
* F1-F3,F6-F10 keys mapped to the same keysyms as in ChromeOS.
* F5 mapped to Print keysym (PrintScreen key).
* `English(US, Chromebook)` layout was added as a replacement of `English(US)` layout with Alt_R mapped to AltGR.
* Alt+Shift+Arrows (Up, Down, Left, Right) mapped to [the same keysyms as Alt[+Ctrl]+Arrows in ChromeOS](https://support.google.com/chromebook/answer/1047364?hl=en) (PgUp, PgDown, Home, End).
* AltGR+Backspace mapped to Delete.

###Benefits
* F1-F10 keysyms with modifiers are the same (e.g. ALT+F4 still close a window).
* Get the keysyms of F1-F10 with AltGR (e.g. AltGR+F2 for rename in Nautilus).
* Suitable when multiple layouts are used (superior to xmodmap as its settings purged when changing layout/language).
* Works with GTK3 apps like Epiphany and Nautilus (xbindkeys+xvkbd doesn't).
* Gnome's [drop-down-terminal extension](https://extensions.gnome.org/extension/442/drop-down-terminal): get the backtick/grave character with AltGR+` on the English (US, Chromebook) layout.
* Works well in a Gnome Wayland session.

###Known limitations
* Chromium, Firefox and LibreOffice aren't respecting Alt+Shift mapping. Alt+Shift+Arrows (PgUp, PgDown, Home, End) not working properly for navigation in Chromium and Firefox but do work when writing in a text box with these applications, it also works in any other application (perfect in Epiphany).
* Alt+Shift+Down hotkey (set as `PgDown`) conflicts with Nautilus hotkey mapping to the action `OpenCloseParent`. It's recommended to clear the hotkey mapping by adding the following line to `~/.config/nautilus/accels`.
```
(gtk_accel_path "<Actions>/DirViewActions/OpenCloseParent" "")
```
* Firefox doesn't respect XF86Reload (F3 key set as Reload). If Firefox is your default browser then you can comment out the patch that set F3 as XF86Reload and use another method to set it as 'Ctrl+R', see example in [xbindkeys_sample](xbindkeys_sample).  

###Other recommended hotkeys tweaks 
*  Nautilus: set Alt+Backspace as send-to-trash action and Shift+Backspace as delete by adding the following lines to `~/.config/nautilus/accels`.
```
(gtk_accel_path "<Actions>/DirViewActions/Trash" "<Alt>BackSpace")
(gtk_accel_path "<Actions>/DirViewActions/Delete" "<Shift>BackSpace")
```
* Chromium:  
With the extension [Hotkeys](https://chrome.google.com/webstore/detail/mmbiohbmijkiimgcgijfomelgpmdiigb) map Alt+Shift+Arrows to [the same actions as the Alt[+Ctrl]+Arrows in ChromeOS](https://support.google.com/chromebook/answer/1047364?hl=en) (preferable as Alt+Left/Right already used for Back/Forward).
* Firefox:
    1. Install the extension [Key Config](https://addons.mozilla.org/en-us/firefox/addon/key-config).
    2. Extract the file keyconfig.js from the xpi package (it's just a zip) and open it, replace the two occurence of the function of scrollByLine to scrollByPages and limit the argument to 1.
    3. Update the xpi with our keyconfig.js.
    4. Start Firefox and map Alt+Shift+Arrows to [the same actions as the Alt[+Ctrl]+Arrows in ChromeOS](https://support.google.com/chromebook/answer/1047364?hl=en) (preferable as Alt+Left/Right already used for Back/Forward).
* Xbindkeys:  
Sample configuration file is supplied ([xbindkeys_sample](xbindkeys_sample)) as users might like having extra hotkeys (I don't).  
The main difference between the sample config to ChromeOS is the use of Ctrl+Arrows instead of Alt+Arrows.  
