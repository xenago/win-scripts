# ps

PowerShell commands and utilities.

# Repeatedly run command

Every 2 seconds, this will print the date and then run a command, similar in effect to `watch -n 2 'echo test'`:

    while (1) {date -format s; echo test; sleep 2}

# Stop-Parsing token

Add `--%` if passing in inputs which will cause reinterpretation errors, like square brackets, without escaping.

For example:

```powershell
.\adb.exe shell mv "Dragonfly Squadron [Remastered] (1954) [3D MVC, BayView]" "/storage/EC69-5D42/Media/Video/Movies/3D"
```

This will cause the `/system/bin/sh: syntax error: unexpected '('` error.

Solution:

```powershell
.\adb.exe --% shell mv (...)
```
