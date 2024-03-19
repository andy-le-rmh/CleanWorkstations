# CLEAN REPORTING WORKSTATION #
> [!TIP]
> Below are commands when in **Command Prompt**
> 
> You should start an elevated Prompt using a local admin account.
> 
> You may start long processes in a different thread so you can continue without needing to wait for that process to finish by using `start ""` before your commands.
> 
> Example: `start "" "\\mhkarisma\Startup Scripts\SyngoVia\syngo.via.Client.Setup@172.28.42.103.exe"`

## NVIDIA DRIVERS ##
> [!WARNING]
> Older versions of NVIDIA drivers does not work for browser hardware accelleration. Can test this by going to Youtube and try to play a video.
> 
> `31.0.15.2727` `23/11/2022` is known to **not** work - which is the version supplied in the IT Clean image.
>
> The version below is known to work:
```
"\\mhkarisma\Startup Scripts\NVIDIA Drivers\551.61-quadro-rtx-desktop-notebook-win10-win11-64bit-international-dch-whql.exe"
```



## CHROME & SHORTCUTS ##
> Download

[https://google.com/chrome](https://google.com/chrome)

> Install
```
ChromeSetup.exe
```

> Shortcut to Radiology Intranet site in Chrome
```
powershell "$s=(New-Object -COM WScript.Shell).CreateShortcut('C:\Users\Public\Desktop\Radiology Intranet - Chrome.lnk');$s.WorkingDirectory='C:\Program Files\Google\Chrome\Application';$s.TargetPath='C:\Program Files\Google\Chrome\Application\chrome.exe';$s.Arguments='http://172.28.40.180';$s.Save()"
```
> Shortcut to Protocol App in Chrome
```
powershell "$s=(New-Object -COM WScript.Shell).CreateShortcut('C:\Users\Public\Desktop\Protocol App - Chrome.lnk');$s.WorkingDirectory='C:\Program Files\Google\Chrome\Application';$s.TargetPath='C:\Program Files\Google\Chrome\Application\chrome.exe';$s.Arguments='http://radorder:8080/protapp/prot.html';$s.Save()"
```
> Shortcut to Synapse 5 in Chrome (interuption workflow)
```
powershell "$s=(New-Object -COM WScript.Shell).CreateShortcut('C:\Users\Public\Desktop\Synapse5 - Chrome.lnk');$s.WorkingDirectory='C:\Program Files\Google\Chrome\Application';$s.TargetPath='C:\Program Files\Google\Chrome\Application\chrome.exe';$s.Arguments='http://rmh-synapse/synapse';$s.Save()"
```

## KARISMA ##
> Make a new folder for Karisma

```
MD C:\Karisma
```
> Copy the app files over
```
COPY "\\mhkarisma\LIVE\KarismaConsole.exe" "C:\Karisma\KarismaConsole.exe" /Y
COPY "\\mhkarisma\LIVE\KarismaConsole.map" "C:\Karisma\KarismaConsole.map" /Y
```
> Grant group 'Users' full access to Karisma folder so can write logs

```
icacls "C:\Karisma" /grant:r "Users:(OI)(CI)(F)"
```

> Create shortcut in Public Desktop to Karisma
```
powershell "$s=(New-Object -COM WScript.Shell).CreateShortcut('C:\Users\Public\Desktop\Karisma - Synapse v5.lnk');$s.WorkingDirectory='C:\Karisma';$s.TargetPath='C:\Karisma\KarismaConsole.exe';$s.Arguments='/server:mhkarisma /port:40100 /pacsclient:synapse5';$s.Save()"
```
After installing you should log into Karisma to (1) **assign workstation license**, (2) download other files and (3) install **SpeechMagic**.

## SYNAPSE DESKTOP AGENT ##
Currently waiting for Fuji to confirm best practice deployment.

MSI can manually be downloaded from (must use Edge in IE mode):
	[http://rmh-synapse/ex](http://rmh-synapse/ex)
``` 
start "" SynapseWorkstationEx.msi
```


## NINJAPACS ##
```
COPY "\\mhkarisma\Startup Scripts\NinjaPacs v0.997_x64.exe" "C:\Users\Public\Desktop\NinjaPacs v0.997_x64.exe" /Y
```
> Create shortcut to auto startup
```
powershell "$s=(New-Object -COM WScript.Shell).CreateShortcut('C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp\NinjaPacs.lnk');$s.TargetPath='C:\Users\Public\Desktop\NinjaPacs v0.997_x64.exe';$s.Save()"
```

## SYNGO VIA ##
> Must start the client installer first
```
"\\mhkarisma\Startup Scripts\SyngoVia\syngo.via.Client.Setup@172.28.42.103.exe"
```
> Then install the Enterprise Browser
```
"\\mhkarisma\Startup Scripts\SyngoVia\rmhradentcon.ssg.org.au.msi"
```
> Clean up the icons on the desktop (delete unused ones leaving only Enterprise Browser)
```
DEL "C:\Users\Public\Desktop\syngo.via - Server Selection.lnk"
DEL "C:\Users\Public\Desktop\syngo.via - Single Sign On.lnk"
DEL "C:\Users\Public\Desktop\syngo.via Client.lnk"
DEL "C:\Users\Public\Desktop\syngo.via Quick Guide.lnk"
DEL "C:\Users\Public\Desktop\syngo Flight Recorder.lnk"
COPY "\\mhkarisma\Startup Scripts\SyngoVia\syngo.via Enterprise Browser.lnk" "C:\Users\Public\Desktop\syngo.via Enterprise Browser.lnk" /Y
```

## DOTNET RUNTIME ##
This is required for certain tools to work such as PACSMenu and the popup for unreported studies
```
"\\mhkarisma\Startup Scripts\DotNet\windowsdesktop-runtime-6.0.28-win-x64.exe" /install /quiet /norestart
```

## PACSMENU ##
> Copy app files over
```
XCOPY "\\mhkarisma\Startup Scripts\PACSMenu" "C:\PACSMenu" /Y /E /I /Q
```
> Grant group 'Users' full access to PACSMenu folder so can write settings
```
icacls "C:\PACSMenu" /grant:r "Users:(OI)(CI)(F)"
```

## DRAGON ##
> Run the installer remotely
```
"\\mhkarisma\Startup Scripts\Dragon\setup.exe"
```
> License key
```
more "\\mhkarisma\Startup Scripts\Dragon\Serial Number.txt"
```
## TEAMS ##
> The bootstrapper will download the latest version for all users
```
"\\mhkarisma\Startup Scripts\Teams\teamsbootstrapper.exe" -p
```
> A successful install will show this message:

![successful install screenshot](https://learn.microsoft.com/en-us/microsoftteams/media/new-teams-direct-deploy-cmd-feedback.png)
