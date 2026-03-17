#!/bin/bash
#
# sign-flet-macos 1.0.1
#
# Signs Flet macOS desktop-app packages the right way :)
#
# (c)2026 Harald Schneider - marketmix.com
#

DEV_ID="Harald Schneider"   # <-- Your ID here.
TARGET="${1:-.}"
APP=$(basename "$TARGET" .app)

if [ ! -e "$TARGET" ]; then
    echo "Error: Target '$TARGET' not found"
    exit 1
fi

ENTITLEMENTS="/tmp/codesign.entitlements"
cat > "$ENTITLEMENTS" << 'EOF'
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>com.apple.security.cs.allow-jit</key>
    <true/>
    <key>com.apple.security.cs.allow-unsigned-executable-memory</key>
    <true/>
</dict>
</plist>
EOF

echo "----------------------------------------------"
echo "Starting & closing app to catch bundle writes."
echo "Please wait ..."
echo "----------------------------------------------"
open "${TARGET}"
sleep 5
osascript -e "quit app \"${APP}\""

echo "---------------------------------"
echo "Signing Framework libs ..."
echo "---------------------------------"
find "$TARGET" -type f -path "*Frameworks*" \( -iname '*.so' -o -iname '*.dylib' \) | while read f; do
    echo "Signing dylib: $f"
    codesign -f -s "$DEV_ID" --entitlements "$ENTITLEMENTS" --options runtime "$f" 2>/dev/null || true
done

echo "---------------------------------"
echo "Signing Python-Framework ..."
echo "---------------------------------"
find "$TARGET" -type f -path "*Python.framework*" -name "Python" | while read f; do
    echo "Signing Python: $f"
    codesign -f -s "$DEV_ID" --entitlements "$ENTITLEMENTS" --options runtime "$f" 2>/dev/null || true
done

echo "---------------------------------"
echo "Signing other Frameworks ..."
echo "---------------------------------"
find "$TARGET" -type d -name "*.framework" | while read f; do
    echo "Signing framework bundle: $f"
    codesign -f -s "$DEV_ID" --entitlements "$ENTITLEMENTS" --options runtime "$f" 2>/dev/null || true
done

echo "---------------------------------"
echo "Signing main executable ..."
echo "---------------------------------"
codesign -f -s "$DEV_ID" --entitlements "$ENTITLEMENTS" --options runtime "$TARGET"

echo "---------------------------------"
echo "Verifying signature ..."
echo "---------------------------------"
codesign -v "$TARGET"

echo "DONE - Code signing completed!"
rm -f "$ENTITLEMENTS"
