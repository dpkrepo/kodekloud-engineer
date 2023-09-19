# Task
The backup server in the Stratos DC contains several template XML files used by the Nautilus application. However, these template XML files must be populated with valid data before they can be used. One of the daily tasks of a system admin working in the xFusionCorp industries is to apply string and file manipulation commands!

Replace all occurances of the string Sample to Submarine on the XML file /root/nautilus.xml located in the backup server.
## Solution

Connect to the Backup Server.

```sh
thor@jump_host ~$ ssh clint@stbkp01
```

Run sed command to replace string Sample to Submarine in the `/root/nautilus.xml` file.
```sh
[clint@stbkp01 ~]$ sudo sed -i 's/Sample/Submarine/g' /root/nautilus.xml
```

## References

[Use sed to Find and Repalce Text in Files](https://www.cyberciti.biz/faq/how-to-use-sed-to-find-and-replace-text-in-files-in-linux-unix-shell/)
