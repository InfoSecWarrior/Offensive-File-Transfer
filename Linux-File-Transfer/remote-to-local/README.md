Commands to start HTTP Server -
------------------------------------------------------------------------------------------------------------------

**Python HTTP Server**

    python2.7 -m SimpleHTTPServer 80
    python3 -m http.server 80

**PHP HTTP Server**

    php -S localhost:80

**Ruby HTTP Server**
    
    ruby -run -e httpd . -p 80
    
**BusyBox HTTP Server**

    busybox httpd -p 80
        
------------------------------------------------------------------------------------------------------------------

</br>
    
USING WGET -
------------------------------------------------------------------------------------------------------------------

**1. On the Lcoal PC, run the following command after launching a HTTP Server on Remote PC**
    
    wget http://{REMOTE-IP}/demo.txt

**2. Utilize the `-O` flag to specify a different destination for the downloaded file**
    
    wget http://{REMOTE-IP}/demo.txt -O /tmp/demo.txt


**3. Utilize the `-b` flag to execute the process in the background**
    
    wget -b http://{REMOTE-IP}/demo.txt -O /tmp/demo.txt

**4. For downloading files over HTTPS with certificate validation disabled, use the following command**
    
    wget http://{REMOTE-IP}/demo.txt -O /tmp/demo.txt --no-check-certificate

**5. Use the `-i` flag to fetch URLs from a file, where each URL is listed on a separate line**

    wget -i urls.txt

**6. Execute this command on remote PC, while HTTP server is running on local PC, it uses PUT method so run http server which supports PUT method, Here is my script for http server that supports PUT method  -**  https://github.com/sudovivek/Portable-Servers/blob/main/HTTP_Server/http-server.py

    wget -O- --method=PUT --body-file=demo.txt http://{LOCAL-IP}/demo.txt

------------------------------------------------------------------------------------------------------------------

</br>

USING CURL -
------------------------------------------------------------------------------------------------------------------

**1. To download a file and display its content on the screen**
    
    curl -v http://{REMOTE-IP}/demo.txt

**2. Utilize the `-o` flag, to save the output to a file and specify a location**
    
    curl -v http://{REMOTE-IP}/demo.txt -o demo.txt

**3. Utilize the `-O` flag to Write output to a file named as the remote file**

    curl -v -O http://{REMOTE-IP}/demo.txt

**4. Utilize the `-k` flag to download file over HTTPS with certificate validation disabled**
    
    curl -v https://{REMOTE-IP}/demo.txt -O demo.txt -k

**5. Execute this command on remote PC, while HTTP server is running on local PC, it uses PUT method so run http server which supports PUT method, Here is my script for http server that supports PUT method  -**  https://github.com/sudovivek/Portable-Servers/blob/main/HTTP_Server/http-server.py

    curl -v -X PUT --upload-file demo.txt http://{Local-IP}           
------------------------------------------------------------------------------------------------------------------

</br>

NC / Ncat -
------------------------------------------------------------------------------------------------------------------

**Run NC Server on Local PC**
    
    nc -nlvp 443 > demo.txt

**Run NC Client on Remote PC**
    
    nc -v {LOCAL-IP} 443 < demo.txt
                    OR
    cat demo.txt | nc.exe -v {LOCAL-IP} 443
------------------------------------------------------------------------------------------------------------------

</br>

SOCAT -
------------------------------------------------------------------------------------------------------------------

**Run Socat Server on Remote PC**
    
    socat TCP4-LISTEN:443,fork file:demo.txt

**Run Socat Client on Local PC**
    
    socat TCP4:{REMOTE-IP}:443 file:demo.txt,create
------------------------------------------------------------------------------------------------------------------

</br>

PHP -
------------------------------------------------------------------------------------------------------------------

**Run HTTP server on Remote PC**
    
    python -m http.server 80

    php -S 0.0.0.0:80

**Run PHP script on Local PC**

Download file.

    php -r '$file = file_get_contents("http://{REMOTE-IP}/demo.txt"); file_put_contents("demo.txt",$file);'

Output save in output.txt file.

    echo "<?php file_put_contents('output.txt', fopen('http://{REMOTE-IP}/demo.txt', 'r')); ?>" > demo.php && php demo.php
------------------------------------------------------------------------------------------------------------------

</br>

USING SSH - 
------------------------------------------------------------------------------------------------------------------

**SCP-**

**Copy a file from Remote PC to Local PC**
    
    scp user@{REMOTE-IP}:/tmp/demo.txt /tmp/

**Copy a directory from Remote PC to Local PC**

    scp -r user@{REMOTE-IP}:/tmp/demo/ /tmp/
    
**Copy a directory from Remote to Local with RSA key**

    scp -i id_rsa -r user@{REMOTE-IP}:/tmp/demo/ /tmp/
    
**RSYNC-**

**Copy a file from Remote PC to Local PC**
    
    rsync -av user@{REMOTE-IP}:/tmp/demo.txt /tmp/

**Copy a directory from Remote PC to Local PC**

    rsync -r user@{REMOTE-IP}:/tmp/demo/ /tmp/
    
**Copy a directory from Remote to Local with RSA key**

    rsync -av --port 22 -e 'ssh -i id_rsa' -r user@{REMOTE-IP}:/tmp/demo/ /tmp/
