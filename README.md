# Begone-OneDrive

Hay! Ally, ive wrote down the PowerShell program that should stop the evil OneDrive script malware from halting any core processes, and overall PC gaming performance,
This is a looped program and will stay dormant in your background until it detects OneDrive again.

well, this script permanently changes the Windows system configuration so that it completely forgets about the old OneDrive path and strictly uses your local drive.

The reason it kept coming back when you right-clicked and refreshed is that Windows keeps its folder paths loaded in its live memory. The script forcefully overwrites those paths and restarts the Windows desktop interface (explorer.exe) to lock the changes in place immediately.

Once that script finishes running, the program will go into sleep mode until it detects OneDrive again. After the job is done, you can safely close the blue window, and you won't see that error pop up ever again.

```
$paths = @("HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders", "HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders")
foreach ($path in $paths) {
    if (Test-Path $path) {
        Set-ItemProperty -Path $path -Name "Desktop" -Value "$env:USERPROFILE\Desktop" -Force
        Set-ItemProperty -Path $path -Name "{754AC886-D69C-4754-88F1-4B3CD0A31367}" -Value "$env:USERPROFILE\Desktop" -Force
    }
}
if (!(Test-Path "$env:USERPROFILE\Desktop")) { New-Item -ItemType Directory -Path "$env:USERPROFILE\Desktop" -Force }
Stop-Process -Name explorer -Force
```
