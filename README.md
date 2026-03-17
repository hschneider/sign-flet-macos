# sign-flet-macos
**Codesign Flet Desktop-Apps easily under macOS.**


This script signs the output of `flet build macos`.

Replace the `DEV_ID` with yours and call:

```
flet build macos
sign-flet-macos build/macos/YOUR_APP.app
```

To automate **Notarization**, check out:

https://github.com/hschneider/macos-sign-notarize

Drop me a star, if you like it.

