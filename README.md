# sign-flet-macos
### Codesign Flet Desktop-Apps easily under macOS


This Bash-Script signs the output of `flet build macos`.

Edit the script and replace the `DEV_ID` with yours, then call:

```
flet build macos
sign-flet-macos build/macos/YOUR_APP.app
```

To automate **Notarization**, have a look at:

https://github.com/hschneider/macos-sign-notarize

Drop me a star, if you like it.

---
This script is obsolete since Flet 1.0.

Use it, if you are on Flet < 1.0 or as a fallback if you run into problems with builtin sign & notarize.

Details here:
- https://flet.dev/docs/publish/macos#code-signing
- https://github.com/flet-dev/flet/pull/6702
