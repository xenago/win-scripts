# 3D Media Playback on Windows

Play back 3D media, such as MVC-encoded 3D Blu-ray movies, on Windows with bitstreamed HDMI audio and frame-packed video output via 3D Vision.

## General Info

Last [official driver releases](https://nvidia.custhelp.com/app/answers/detail/a_id/4781/~/support-plan-for-3dvision-products) that support 3D Vision include 3DTV Play; Windows 10 1809-based builds are the last officially supported.

It seems possible to [get it working with newer GPUs using the studio driver](https://www.mtbs3d.com/phpbb/viewtopic.php?p=188137&sid=dfed06fd1d35acaa5a8479995016452f#p188137) or with [Intel NUCs via Kodi](https://forum.kodi.tv/showthread.php?tid=365120) but I have not tested these methods since Windows 10 LTSC 2019 is based on 1809 and that is relatively [recent and supported](https://learn.microsoft.com/en-us/lifecycle/products/windows-10-enterprise-ltsc-2019) so it works fine for my HTPC needs using a paltry GTX 1650.

Using software like Cyberlink or [Stereoscopic Player](https://www.3dtv.at/Index_en.aspx) may also be helpful but that is not freeware.

## HTPC Setup

1. OS install

    * Windows 10 ISO: `en_windows_10_enterprise_ltsc_2019_x64_dvd_5795bb03.iso`
    * SHA1: `615A77ECD40E82D5D69DC9DA5C6A6E1265F88E28`
    * Generic KMS key [from Microsoft](https://learn.microsoft.com/en-us/windows-server/get-started/kms-client-activation-keys?tabs=server2022%2Cwindows10ltsc%2Cversion1803%2Cwindows81#windows-enterprise-ltsc-and-ltsb), may be useful: `M7XTQ-FN8P6-TTKYV-9D4CC-J462D`
    * Download ISO and activate using usual methods

2. OS Configuration

    * Disable windows update from downloading drivers (to avoid nvidia driver being overwritten in the future)
    * Recommended:
      * Install clients for Plex, Jellyfin, VLC, etc.
      * Disable automatic windows updates
      * Disable unnecessary startup tasks
      * Configure mounted network drives/storage with read-only accounts for HTPC use

3. Install Nvidia driver using [3D Fix Manager](https://helixmod.blogspot.com/2017/05/3d-fix-manager.html)

    * Purge old driver with [DDU](https://www.guru3d.com/download/display-driver-uninstaller-download/) if needed
    * [3D Fix Manager 1.87 is mirrored here](https://github.com/xenago/win-scripts/raw/main/3d/fix_manager_1.87.7z) as the download seems spotty (the whole thing is somewhat janky but it provides a convenient GUI and tray icon for toggling frame-packed 3D output)
    * Set up 3D resolutions and configuration as desired for your setup
      * The only ones I have used are 1080p24 and 720p60 as those are the only ones relevant for my display, but supposedly [720p50 is supported by the 3D Blu-ray standard as well](https://www.videohelp.com/hd)

4. Install [PotPlayer](https://www.videohelp.com/software/PotPlayer/old-versions), performing the full codec install (including Intel MVC, this works on AMD and Nvidia as well)

5. Configure PotPlayer to decode 3D MVC and output with Nvidia 3D Vision

    * Generally, it is enough to enable the Intel MVC decoder and automatic 3D detection and set output to Nvidia 3D Vision
    * It may be necessary to use the [Nvidia Profile Inspector](https://github.com/Orbmu2k/nvidiaProfileInspector/releases) to set Stereo to Yes for the Daum potplayer profile (and add the potplayer mini64 exe from Program Files to that profile)

6. Enable 3D in the Fix Manager (may be necessary to restart potplayer) and when potplayer restarts it should support 3D output with MVC-encoded content in ISO and MKV form. It will also support playing SBS/OU format content output in frame-packed format.

## PotPlayer HDMI Audio Passthrough

This is useful to bitstream Dolby and DTS audio formats out to the TV/AVR/Projector etc., preserving object-based surround data like Atmos & DTS:X.

1. Ensure that Exclusive mode is enabled in Windows for your HDMI audio device (this will lock the dedicated application to the audio device for bitstreaming audio and prevent regular PCM output from the Windows mixer)
    1. Open `Control Panel`
    2. Open the `Sound` menu
    3. In `Playback`, open the device connected for HDMI audio
    4. In the `Advanced` tab, enable the `Exclusive Mode` options (`Allow applications to take exclusive control` and `Give exclusive mode applications priority`)
2. Open PotPlayer settings (right click playing area > `Preferences`)
3. Open the `Audio` section
    1. Set the `Audio Renderer` to `Built in WASAPI Audio Renderer`
    2. Set the `Speakers` accordingly for your setup (used only when not bitstreaming audio, i.e. any content that is not in DTS or Dolby codecs)
4. Click the `...` button to configure the `Built in WASAPI Audio Renderer`
    1. Set the HDMI audio device as the output
    2. Enable the option to `Use exclusive mode` (`Switch to bitexact` may be needed but didn't seem to be in my testing)
5. Click `Set Built-in Audio Decoder`
    1. Activate `Enable (Pass-through/Bitstreaming)`
    2. On the right, select `Default Pass-through Muxer` for each option supported by the output HDMI chain: `AC3`, `EAC3`, `TrueHD`, `DTS`, and `DTS-HD`
    3. If specific formats do not work, a different Muxer can be selected instead for that format
    4. In my case, DTS/DTS-HD only worked with the `Alternative Pass-through Muxer`
6. Restart PotPlayer
