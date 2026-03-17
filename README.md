# sign-flet-macos
### Codesign Flet Desktop-Apps easily under macOS.


This script signs the output of `flet build macos`.

Edit the script and replace the `DEV_ID` with yours, then call:

```
flet build macos
sign-flet-macos build/macos/YOUR_APP.app
```

To automate **Notarization**, have a look at:

https://github.com/hschneider/macos-sign-notarize

Drop me a star, if you like it.

