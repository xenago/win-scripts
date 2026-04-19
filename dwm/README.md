# dwm

Desktop Window Manager.

## Restart when broken

Sometimes the DWM process needs to be restarted.

For example, when performing a drag-and-drop a floating icon can get stuck on top.

Windows will restart it when shut down:
```bat
taskkill /f /im dwm.exe
```
