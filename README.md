# launchpad-db
Sometimes, you just need to brute force a fix for your macOS launchpad...

Saving this here for future reference (and in case anyone else needs this).

### Fixing LaunchPad DB Preferences

The `*.db` file was missing from com.apple.dock in `~/Library/Application\ Support/Dock`. Resetting LaunchPad, killing the dock, and all the other recommended solutions did not fix the issue, so I first copied the missing LaunchPad DB file from another user on the same computer. This did not immediately fix anything, so I started to search through the Preferences and `.plist` files in the `~/Library` directory to see if the options for *ResetLaunchPad* were changed. I discovered that there weren’t any keys for *ResetLaunchPad or *LaunchPadDBName* in my `com.apple.dock.plist` file at all.

So I found a unique `com.apple.dock.$HOST.plist` file with the original LaunchPadDBName in `~/Library/Preferences/ByHost`. I took that string and edited the current `com.apple.dock.plist` by adding two additional rows: 
```
ResetLaunchPad | boolean | NO
LaunchPadDBName | String | <value>
```

Additionally, I changed the copied `.db` filename to `<value>.db` so that the .plist key was pointing to the correct file.

I then modified the LaunchPad configuration, restarted my computer, and voila! LaunchPad configuration was preserved once more!
