```
C:\Windows\System32\winevt\Logs
```

There are three main ways of accessing these event logs within a Windows system:

1. **Event Viewer** (GUI-based application)
2. **Wevtutil.exe** (command-line tool)
3. **Get-WinEvent** (PowerShell cmdlet)

## Event Viewer

```
eventvwr.msc
```

## wevtutil.exe

enables you to retrieve information about  event logs and publishers. You can also use this command to install and  uninstall event manifests, to run queries, and to export, archive, and  clear logs.

Example:

el enum-logs  List log names.

wevtutil el

wevtu

til el | Measure

**wevtutil qe Application /c:3 /rd:true /f:text**

## Get-WinEvent

This is a PowerShell cmdlet called **Get-WinEvent**. Per Microsoft, the Get-WinEvent cmdlet "gets events from event logs and event tracing log files on local and remote computers." It provides  information on event logs and event log providers. Additionally, you can combine numerous events from multiple sources into a single command and filter using XPath queries, structured XML queries, and hash table queries.

https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/get-winevent?view=powershell-5.1

Get all logs from a computer

```shell-source
Get-WinEvent -ListLog *
```

Get event log providers and log names

```shell-source
Get-WinEvent -ListProvider *
```

Log filtering

```shell-source
Get-WinEvent -LogName Application | Where-Object { $_.ProviderName -Match 'WLMS' }
```



```shell-source
Get-WinEvent -FilterHashtable @{
  LogName='Application' 
  ProviderName='WLMS' 
}
```

https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/get-winevent?view=powershell-7.4&viewFallbackFrom=powershell-7.1

## XPath Queries

https://learn.microsoft.com/en-us/windows/win32/wes/consuming-events#xpath-10-limitations

filter event id

```
Get-WinEvent -LogName Application -FilterXPath '*/System/EventID=100'
```

filter by provider

```shell-session
Get-WinEvent -LogName Application -FilterXPath '*/System/Provider[@Name="WLMS"]'
```

filter Provider name WLMS and Event id 101

```
Get-WinEvent -LogName Application -FilterXPath '*/System/EventID=101 and */System/Provider[@Name="WLMS"]'
```

filter from Eventdata

```shell-session
Get-WinEvent -LogName Security -FilterXPath '*/EventData/Data[@Name="TargetUserName"]="System"' -MaxEvents 1
```

the query to find **WLMS** events with a System Time of **2020-12-15T01:09:08.940277500Z**?                            

Get-WinEvent -LogName Application -FilterXPath '*/System/Provider[@Name="WLMS"] and */System/TimeCreated[@SystemTime="2020-12-15T01:09:08.940277500Z"]'

**Get-WinEvent** and **XPath**, what is the query to find a user named Sam with an Logon Event ID of 4720?

Get-WinEvent -LogNameSecurity -FilterXPath '*/EventData/Data[@Name="TargetUserName"]=Sam" and *System/EventID=4720'

## Event ids

[The Windows Logging Cheat Sheet (Windows 7 - Windows 2012)](https://static1.squarespace.com/static/552092d5e4b0661088167e5c/t/580595db9f745688bc7477f6/1476761074992/Windows+Logging+Cheat+Sheet_ver_Oct_2016.pdf).

