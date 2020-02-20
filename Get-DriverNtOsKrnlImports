Function Get-DriverNtOsKrnlImports {
    [CmdletBinding()]
    param (
        [Parameter(Mandatory = $true)]
        [String]
        $DriverListFile,
        [Parameter(ParameterSetName = 'OutputOptions')]
        [Switch]
        $SaveToIndividualFiles,
        [Parameter(ParameterSetName = 'OutputOptions')]
        [Switch]
        $OutputToConsole,
        [Parameter(ParameterSetName = 'OutputOptions')]
        [Switch]
        $SaveToOneFile,
        [Parameter(ParameterSetName = 'AlertingOptions')]
        [Switch]
        $AlertOnSuspiciousCalls
    )
    process {
        $driverlist = Get-Content -Path $DriverListFile
        foreach ($driver in $driverlist) {
            Write-Host -ForegroundColor Green "[*] Getting exports from driver: [$driver]`r`n"

            $queryInfo = New-Object System.Diagnostics.ProcessStartInfo
            $queryInfo.FileName = 'C:\Program Files (x86)\Microsoft Visual Studio\2019\BuildTools\VC\Tools\MSVC\14.24.28314\bin\Hostx64\x64\dumpbin.exe'
            $queryInfo.RedirectStandardOutput = $true
            $queryInfo.UseShellExecute = $false
            $queryInfo.Arguments = "/imports:ntoskrnl.exe `"$driver`""
            $queryProcess = New-Object System.Diagnostics.Process
            $queryProcess.StartInfo = $queryInfo
            $queryProcess.Start() | Out-Null
            $out = $queryProcess.StandardOutput.ReadToEnd()

            # send output to file with driver name
            if ($SaveToIndividualFiles) {
                if ($AlertOnSuspiciousCalls) {
                    # todo
                }
                else {
                    # Get driver file name
                    $driverName = $driver.Split('\') | Select-Object -Last 1

                    # Silently continue on errors incase of overwrites
                    $out | Out-File -FilePath ".\$driverName`_ntoskrnl_imports.txt" -Force -ErrorAction SilentlyContinue
                }
            }
            if ($OutputToConsole) {
                if ($AlertOnSuspiciousCalls) {
                    # todo
                }
                else {
                    $out
                }
            }
            if ($SaveToOneFile) {
                if ($AlertOnSuspiciousCalls) {
                    # todo
                }
                else {
                    $out | Out-File -FilePath ".\driver_ntoskrnl_imports.txt" -Append -Force -ErrorAction SilentlyContinue
                }
            }
        }
    }
}
