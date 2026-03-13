# The Blender Artist Revenge Prank

A persistent Mac prank for a friend who won't stop making dicks in Blender and taking screenshots on your computer.

## What It Does

- Every day at 18:00, opens xvideos.com 10 times (3 seconds apart)
- First time only: shows 3 dialog popups before opening tabs
- Survives reboots and terminal closing
- Cannot be stopped by simply killing the process

## Install

Open Terminal on their Mac and paste:

```bash
cat > ~/Library/LaunchAgents/com.blender.artist.plist << 'EOF'
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.blender.artist</string>
    <key>ProgramArguments</key>
    <array>
        <string>/bin/bash</string>
        <string>-c</string>
        <string>FLAG="$HOME/.blender_artist_flag"; if [ ! -f "$FLAG" ]; then osascript -e 'display dialog "Stop making dicks in Blender on my computer." buttons {"No"} default button 1 with title "Hey"' &amp;&amp; osascript -e 'display dialog "Stop taking 500 screenshots every time I leave the room." buttons {"Fair enough"} default button 1 with title "Also"' &amp;&amp; osascript -e 'display dialog "This is what you get." buttons {"Oh no"} default button 1 with title "Too Late"' &amp;&amp; touch "$FLAG"; fi; for i in $(seq 1 10); do open -a Safari https://www.xvideos.com; sleep 3; done</string>
    </array>
    <key>StartCalendarInterval</key>
    <dict>
        <key>Hour</key>
        <integer>18</integer>
        <key>Minute</key>
        <integer>0</integer>
    </dict>
    <key>KeepAlive</key>
    <false/>
</dict>
</plist>
EOF
launchctl load ~/Library/LaunchAgents/com.blender.artist.plist
```

Press Enter. Done.

## Uninstall

```bash
launchctl unload ~/Library/LaunchAgents/com.blender.artist.plist
rm ~/Library/LaunchAgents/com.blender.artist.plist
rm ~/.blender_artist_flag
```
