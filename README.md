# Begone-OneDrive

Hay! Ally, ive wrote down the PowerShell program that should stop the evil OneDrive script malware from halting any core processes, and overall PC gaming performance,
This is a looped program and will stay dormant in your background until it detects OneDrive again.

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
