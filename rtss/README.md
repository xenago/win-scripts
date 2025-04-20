# rtss

Configure [Rivatuner Statistics Server](https://www.guru3d.com/download/rtss-rivatuner-statistics-server-download/) (installed with [MSI Afterburner](https://www.guru3d.com/download/msi-afterburner-beta-download/)).

# Stop annoying update warnings

1. Run RTSS
2. Click `Setup`
3. Change `Check for available product updates` to `Never`

# Stop error message at boot

Frequently, RTSS will display a nonsensical `Direct3D9 components cannot be hooked` warning at boot. This error is utterly irrelevant and can be silenced.

1. Run `notepad.exe` as Admin
2. Open `C:\Program Files (x86)\RivaTuner Statistics Server\ProfileTemplates\Config`
3. Edit `Silent = 0` and change to `Silent = 1`
