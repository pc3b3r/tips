# Tips


* **BASH**

Bash date log output
```bash
___script___>>`date "+%Y-%m-%d"`.log 2>&1
```

Start .ovpn file

```bash
sudo openvpn --config ***.ovpn --verb 4
```

Network usage
```bash
sudo nethogs wlan0
```

Tunnel Port Forward
```bash
ssh -C2qTnN -D 8080 username@ip_host -p port_host
```

Permission code 
```bash
stat /home
```


Split a file in multiple files in the folder with the same file name

```bash
#!/bin/bash

texts=$(find . -size +500M -exec ls {} \+)

echo $texts

IFS=' ' read -a array <<<$texts

echo "starting import"

for currentFile in "${array[@]}"
do
        echo "$currentFile"
        dirName=$(dirname "$currentFile")
        baseName=$(basename $currentFile)
        echo $dirName
        echo $baseName
        rm -rf "${dirName}/${baseName//.}"
        mkdir "${dirName}/${baseName//.}"
        split -dl 70000 $currentFile "${dirName}/${baseName//.}/${baseName}."
        echo "${dirName}/${baseName//.}/${baseName}"
done
```

* **cUrl**

CURL with SSL Certificate: 

export all the certificates from green lock in the top left of the browser with signature "DER encoded binary". 
Name them cert1.cert - cert2.cert - cert3.cert

then convert ALL to PEM

```bash
openssl x509 -inform DES -in cert1.cert -out pem1.pem -text
openssl x509 -inform DES -in cert2.cert -out pem2.pem -text
openssl x509 -inform DES -in cert3.cert -out pem3.pem -text
```

merge all

```bash
cat pem*.pem > validCert.pem
```

run cUrl with PEM certificate
```
curl --cacert validCert.pem -X GET "https://www.google.it"
```


* **TOR**

Generate Password: 

```bash 
tor --hash-password YOURMAGICPASSWORD
```

copy the password generated, then

```bash
vim /etc/tor/torrc
```

Enable ControlPort 9051

paste the hash in HashedControlPassword

enable RunAsDaemon

* **SSHUTTLE**

Enable Wifi hotspot &
```bash
sudo sshuttle -vNHr user@server:port 0/0 -l 10.42.0.1
```
Using specific rsa
```bash
sshuttle -e 'ssh -i ~/.ssh/id_rsa' -r {___USER___}@{___IP___}:{___PORT___} 0/0 -vvv --exclude {___IP___}
```

* **LOGIN --> TELEGRAM   == > /etc/profile**

```bash
KEY="TOKEN FROM BOTFATHER"
#from https://api.telegram.org/bot{$KEY}/getUpdates
CHATID="CHAT_ID" 
TIME="10"
URL="https://api.telegram.org/bot$KEY/sendMessage"
TEXT="`whoami` Login on `hostname`"
curl -s --max-time $TIME -d "chat_id=$CHATID&disable_web_page_preview=1&text=$TEXT" $URL >/dev/null
```
