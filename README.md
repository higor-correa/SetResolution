# Set Windows Display Resolution from Command Line

This small command line utility allows you to quickly set Windows Display Resolutions to any of the available display modes for your video driver on the default Windows Screen device.

* Set explicit Display Resolution (has to match a valid display mode)
* List all available Display Modes
* Create and use multiple Display Mode Profiles for quick access


> **Warning:** Use at your own risk. Setting an invalid display mode can [leave your screen inaccessible](#fark-i-set-a-resolution-that-doesnt-work-now-what). Use only with supported display modes. We check your settings against available modes and only allow those that match a driver display mode, but there may still be some modes that don't work.

## Download
This tool is a small, self-contained Console EXE application and you can download the `SetResolution.exe` (or `sr.exe` file directly from here):

[Download SetResolution.exe](https://github.com/RickStrahl/SetResolution/raw/master/Binaries/SetResolution.exe)

I recommend you copy to a folder location that is in your Windows path or add it to your path, so you can run `SetResoltion` from any location.

Most common usage is with a pre-define profile name:

```ps
SetResolution 1080

# or shortcut version (sr.exe)
sr 1080
```

## Syntax
To show available syntax, run `SetResolution.exe` or `sr.exe` without any parameters or `/?` or `HELP`. 
The help information is as follows:

```txt
Syntax:
-------
SetResolution  [<ProfileName>|SET|LIST|PROFILES|CREATEPROFILE]
               -w 1920 -h 1080 -f 60 -b 32 -o 0 -la -p ProfileName

Commands:
---------
HELP || /?          This help display
<ProfileName>       Run with only a Profile Name sets that display profile
SET                 Sets Display Settings -
                    provide either a profile (-p) or display options -w/-h/-f/-b/-o
LIST                Lists all available display modes
PROFILES            Lists all saved profiles (stored in SetResolution.xml)
CREATEPROFILE       Creates a new profile by specifying name and display options

Display Settings:
-----------------
-w                  Display Width
-h                  Display Height
-f                  Display Frequency in Hertz (60*)
-o                  Orientation - 0 (default*), 1 (90deg), 2 (180deg), 3 (270deg)
-p                  Profile name
-la                 List all Display modes (LIST). Default only shows current matches

Examples:
---------
SetResolution MyProfile
SetResolution SET -p MyProfile
SetResolution SET -w 1920 -h 1080 -f 60
SetResolution LIST
SetResolution PROFILES
SetResolution CREATEPROFILE -p "My Profile" -w 1920 -h 1080 -f 60
```

### Add to the Windows Path
We recommend that you add the `SetResolution.exe` folder to your Windows path so that you can always and quickly access the application to switch resolution from anywhere.

### Profiles
Profiles are 'shortcuts' to a specific set of Display Settings with a name and you can quickly access a profile with:

```ps
SetResolution SET -p <profileName>
```

You can create a profile with:

```ps
SetResolution CREATEPROFILE -p <profileName> -w 1280 -h 768 -f 59
```

Profiles are stored in `SetResolution.xml` in the same folder as the .exe. To remove profiles you can edit the `SetResolution.xml` file.

#### Default Profiles
A number of default profiles are added for common 16:9 resolutions @ 60hz:

```text
Available Profiles
------------------
1080:  1920 x 1080, 32, 60
4k:  3840 x 2160, 32, 60
1440:  2560 x 1440, 32, 60
720:  1280 x 720, 32, 60
```

These are stored in `SetResolution.xml` and you can add and remove additional profiles there or add via.

```ps
SetResolution CREATEPROFILE -p 1600 -w 1600 -h 1200  
```

## Fark: I Set a Resolution that doesn't work. Now what?
If you accidentally set your monitor into a display mode that isn't supported or just doesn't work, it's possible that the your screen becomes inaccessible. Because this tool switches the default display settings, once a wrong setting is made the screen simply will be blank and it's not just a simple matter of rebooting as the setting is applied to the Windows settings and persists on a reboot.

To reset an invalid setting you have to **boot into Windows Safe Mode** and select another display adapter, then reboot.

> Moral of the Story: Pick a display mode that you know works!

> SetResolution doesn't make this easy as we match your input Display Mode to the available display modes.

Note it's not easy to do this - as we set the display mode only to modes that have been retrieved just before - so realistically display modes should never be mismatched to what the monitor supports. Still it's possible of the hundreds of display modes available for many adapters that some may not work.

## Credits
The hard work of this tool is in the Win32 interfaces to retrieve and set display settings. All of that code is based on this article on C# Corner by [Mohammad Elseheimy](https://www.c-sharpcorner.com/members/mohammad-elsheimy):

* [Changing Display Settings Programmatically
](https://www.c-sharpcorner.com/uploadfile/GemingLeader/changing-display-settings-programmatically/)


