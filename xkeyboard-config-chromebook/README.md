#xkeyboard-config-chromebook

xkeyboard-config with custom mapping for Chromebooks.

### Changes:
* F1-F10 keys mapped to the same keysyms as ChromeOS.
* F5 mapped to Print keysym (PrintScreen key).
* English US layout: Alt_R mapped to AltGR.
* AltGR+Arrows (Up, Down, Left, Right) mapped to the same keysyms as Ctrl+Arrows in ChromeOS (PgUp, PgDown, Home, End).
* AltGR+Backspace mapped to Delete.

###Benefits:
* F1-F10 keysyms with modifiers were not changed (e.g. ALT+F4 still close a window).
* Suitable when multiple layouts are used, superior to xmodmap as its settings purged when changing layout/language.
* Works with GTK3 apps like Epiphany and Nautilus (xbindkeys+xvkbd doesn't).
* Gnome's drop-down-terminal extension: get the backtick/grave character with AltGR+` on the English US layout
* Might also work in a Wayland desktop (Gnome 3.14) as Wayland supports XKB (though Weston 1.5.0 seems to fallback to the kbd layouts and not xkeyboard-config).

###Issues
* AltGR+Arrows (PgUp, PgDown, Home, End) doesn't works for navigation in Chromium and Firefox but does work when writing in a text box in these applications, it also works in any other application (perfect in Epiphany).

###Other Recommended Settings
*  Nautilus: set Alt+Backspace as send-to-trash action. 
* Chromium: with the extension Hotkeys map Ctrl+Arrows to the same actions as in ChromeOS.