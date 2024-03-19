# CLEAN REPORTING WORKSTATION #
Best to start a new CMD with elevated privileges for

## NVIDIA DRIVERS ##
Older versions of NVIDIA drivers does not work. Can test this by going to Youtube and try to play a video.
`31.0.15.2727` `23/11/2022` is known to **not** work - which is in the IT Clean image

## CHROME & SHORTCUTS ##
[https://google.com/chrome](https://google.com/chrome)



## KARISMA ##
```
::make a new folder
MD C:\Karisma
::copy the necessary files over 
COPY "\\mhkarisma\LIVE\KarismaConsole.exe" "C:\Karisma\KarismaConsole.exe" /Y
COPY "\\mhkarisma\LIVE\KarismaConsole.map" "C:\Karisma\KarismaConsole.map" /Y
::grant group 'Users' full access to Karisma folder so can write logs
icacls "C:\Karisma" /grant:r "Users:(OI)(CI)(F)"
::create shortcut in Public Desktop to Karisma
powershell "$s=(New-Object -COM WScript.Shell).CreateShortcut('C:\Users\Public\Desktop\Karisma - Synapse v5.lnk');$s.TargetPath='C:\Karisma\KarismaConsole.exe';$s.Arguments='/server:mhkarisma /port:40100 /pacsclient:synapse5';$s.Save()"
```

## SYNAPSE DESKTOP AGENT ##
currently waiting for Fuji to confirm best practice deployment
MSI can manually be downloaded from (must use Edge in IE mode):
	[http://rmh-synapse/ex](http://rmh-synapse/ex)
```
start "" SynapseWorkstationEx.msi
```

## NINJAPACS ##
```
COPY "\\mhkarisma\Startup Scripts\NinjaPacs v0.997_x64.exe" "C:\Users\Public\Desktop\NinjaPacs v0.997_x64.exe" /Y
::make startup shortcut to 
powershell "$s=(New-Object -COM WScript.Shell).CreateShortcut('C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp\NinjaPacs.lnk');$s.TargetPath='C:\Users\Public\Desktop\NinjaPacs v0.997_x64.exe';$s.Save()"
```

## SYNGO VIA ##
```
::start the client installer first
start "" "\\mhkarisma\Startup Scripts\SyngoVia\syngo.via.Client.Setup@172.28.42.103.exe"
::install the Enterprise Browser
start "" "\\mhkarisma\Startup Scripts\SyngoVia\rmhradentcon.ssg.org.au.msi"
::cleanup the icons on the desktop
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
start "" "\\mhkarisma\Startup Scripts\DotNet\windowsdesktop-runtime-6.0.28-win-x64.exe" /install /quiet /norestart
```

## PACSMENU ##
```
::copy files over
XCOPY "\\mhkarisma\Startup Scripts\PACSMenu" "C:\PACSMenu" /Y /E /I /Q
::grant group 'Users' full access to PACSMenu folder so can write settings
icacls "C:\PACSMenu" /grant:r "Users:(OI)(CI)(F)"
```
