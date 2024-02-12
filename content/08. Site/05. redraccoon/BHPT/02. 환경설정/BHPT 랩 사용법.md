
# 1. mac 에서 설정

1. open vpn 설치 (인터넷에서 dmg 또는 터미널에서 brew로 설치)
2. 랩에서 준 .ovpn 파일 을 실행
3. 터미널에서 ifconfig 명령어 입력 시 맨 마지막에 아래처럼 보이면 동작 중
```
utun0: flags=8051<UP,POINTOPOINT,RUNNING,MULTICAST> mtu 1500
	inet 10.8.0.15 --> 10.8.0.1 netmask 0xffffff00
```

4. brew 로 nmap 설치 
5. nmap 실행
```
namp -p 172.31.133.228

Starting Nmap 7.94 ( https://nmap.org ) at 2023-12-29 22:28 KST
Nmap scan report for 172.31.133.228
Host is up (0.014s latency).

PORT   STATE SERVICE
22/tcp open  ssh

Nmap done: 1 IP address (1 host up) scanned in 0.16 seconds
```


[🔓 머신 실행 완료 - 0xm1n1🔓]

▓▒░--------------------------------------------░▒▓

🛡️ 박스 이름:            testo
🔐 인스턴스 해시:        1100610612922425374-testo-jjbVxXuAtjfY
🌐 VPN IP:              172.31.133.228
🆔 인스턴스 ID:          i-09e3c6edc76e0e08d
🕔 예정 종료 시각 (KST): 2023-12-29 22:52:26

▓▒░--------------------------------------------░▒▓

👨‍💻 Happy Hacking 👩‍💻