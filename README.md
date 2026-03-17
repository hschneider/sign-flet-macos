# sign-flet-macos
**Codesign Flet Desktop-Apps easily under macOS.**


This script signs the output of `flet build` and automates the codesign process for desktop-apps under macOS.

Replace the `DEV_ID` with yours and call:

```
flet build
./sign-flet-macos.sh build/macos/YOUR_APP.app
```

To automate **Notarization**, check out:

https://github.com/hschneider/macos-sign-notarize

Drop me a star, if you like it.

