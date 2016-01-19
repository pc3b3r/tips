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
