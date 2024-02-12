
1 호스트네임
xx@aaa
aaa가 호스트 네임 

2 명령창에서 입력한대로 출력
echo "" 

3 현재 위치 
pwd 

4 파일 내용 보기 
cat 

5 파일 내용 검색
find . -name "flag.txt"

find . -type f -print | xargs grep -i "user" /dev/null
닷 . 은 현재 디렉토리 의미  

grep -rinoE '<플래그'

## 1. 열린포트 확인 

* netstat -tnlp

## 2. vmware 네트워크 연결이 안될 때 
* dhclient


**dhclient 란 ?**
dhcp 서버에서 ip를 할당 받게 해주는 명령어 이다. 
보안은 취약해 지지만 일일이 ip주소, 넷마스크, 게이트웨이를 입력하는 것 보다 훨씬 쉽고 간편한 방법이다. 

"<플래그-파일>.txt"