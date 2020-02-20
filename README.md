# Get-DriverNtOsKrnlImports
Use dumpbin to find driver imports of ntoskrnl.exe.

# Usage
Relies on VS Build Tools installs and dumpbin in the hardcoded path. Doesn't need to be this way, you can easily switch this to whatever you'd like. Ultimately it should be parameterized but that's on my to-do list. Dot source the function and use like so:
```powershell
. .\Get-DriverNtOsKrnlImports.ps1
Get-DriverNtOsKrnlImports -DriverListFile C:\Path\To\List\Of\Drivers.txt -SaveToOneFile
```

This will write a file to `.\driver_ntoskrnl_imports.txt` with dumpbin output for each run.
# To-Do
- Write up 'suspicious calls' logic to trip on `ZwAllocateVirtualMemory` and `KeInsertQueueApc` calls, a la [vulnerable Huawei driver style](https://www.microsoft.com/security/blog/2019/03/25/from-alert-to-driver-vulnerability-microsoft-defender-atp-investigation-unearths-privilege-escalation-flaw/).
- Dynamic dumpbin.exe finding or parameterized input.
