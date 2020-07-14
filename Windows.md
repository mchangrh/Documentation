# Determine version of Windows ISO
`dism /Get-WimInfo /WimFile:E:\source\install.esd /index:1`

source: [SuperUser](https://superuser.com/questions/443357/version-number-of-windows-7-from-its-image-iso)

# Shrink VHDX
```PowerShell
$FilePath = "D:\Hyper-V\Virtual Hard Disks\Server01.vhdx"

Mount-VHD -Path $FilePath -ReadOnly
Optimize-VHD -Path $FilePath -Mode Full # or Quick
Dismount-VHD -Path $FilePath
```
