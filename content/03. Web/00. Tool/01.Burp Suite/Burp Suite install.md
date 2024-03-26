
# 주의 

>[!warning] 필독!
>- 새로운 피씨를 셋팅 하더라도 인증서를 공유하기위해 Export를 잘 해 놓는다.
>- 갑자기 버프가 안 잡힐 경우 프로젝트 save한 걸 사용 하지 않는다.


# 1. 인증서 재 설치 및 신규 설치 

- 기존인증서 삭제 
  실행 - certmgr.msc - 신뢰할 수 있는 루트 인증 기관 - PortSwigger 인증서 삭제
- Regenerate CA certificate 선택 (import한 인증서 초기화)

- proxy - options - import/export ca 선택 - Certificate in DER format 선택 - 
   폴더선택후 다운 
- 다운 받은 인증서 더블 클릭 후 설치 - 로컬컴퓨터 - 모든인증서를 다음 저장소에 저장 찾아보기 - 신뢰할 수 있는 루트 인증기관 - 다음 - 마침 

# 2. 안드로이드 Nox 인증서 작업 

## 01. 깃 설치 후 깃허브를 통해 Open ssl 다운 받기 

- 참고
> https://fascination-euna.tistory.com/224
## 02. OpenSSL Pem 변환 작업 

- 리눅스에서 해당 내용 작업 
```
openssl x509 -inform DER -in [인증서파일명].der -out [인증서파일명].pem

openssl x509 -inform PEM -subject_hash_old -in [인증서파일명].pem

mv [인증서파일명].pem 9a5ba575.0


ex)
openssl x509 -inform DER -in burp.der -out burp.pem  
openssl x509 -inform PEM -subject_hash_old -in burp.pem
mv burp.pem 9a5ba575.0

```

## 03. adb를 통해 변환한 파일 nox플레이어에 설치 

- 변환한 인증서를 C:/Program files/Nox/bin/ 아래로 이동 

- adb를 사용하여 생성한 인증서 파일을 nox 플레이어로 옮긴다음 권한변경

```
adb remount // 권한 부여 
> remount succeeded

adb push 9a5ba575.0 /system/etc/security/cacerts/
> [100%] /system/etc/security/cacerts/9a5ba575.0

adb shell // 이동 후 

cd /system/etc/security/cacerts/

chmod 644 9a5ba575.0 // 권한부여 
```


## 04. nox 재부팅 

- 설정 - 보안 - 암호화 및 사용자 인증정보 - 신뢰할 수 있는 자격증명 - 시스템 에서 들어갔는지 확인 

완료! 



# 3. 안드로이드 KernelSu 인증서 작업 

-  nox에서 만든 인증서 폴더로 이동 
-  설정 - 보안 - 보안설정더보기 - 암호화 및 사용자 인증정보 - 인증서설치 
    인증서 옮긴 폴더로 이동하여 설치 
-  설정 - 보안 - 보안설정더보기 - 신뢰할 수 있는 사용자 인증정보 에서 사용자에
    인증서 올라가있는지 확인 
-  KernelSu 모듈에서 Move User Certs KernelSU off 후 재시작 - on 후 재시작 
-  신뢰할 수 있는 사용자 인증정보 - 시스템 에서 해당 인증서 올라가 있는지 확인 
    올라가있으면 완료 

**인증서 사라질 경우**
-  모듈과의 충돌? 같은 이유로 인증서가 시스템에서 사라지는 경우가 있다. 
-  모든 모듈을 종료하고 재시작
-  Move User Certs KernelSU - on 후 재시작 
-  신뢰할 수 있는 사용자 인증정보에서 시스템에 인증서 올라가있음을 확인할 수 있다. 
-  이후 필요한 모듈을 하나씩 on 하면서 재시작하며 시스템인증서가 사라지는 여 부를 확인 한다. 
-  만약 이래도 안될경우 kernel su 초기화를 재작업한다.  직접 인증서를 밀어넣는 방법은 'KSU' read only라는 무서운 녀석으로 인해 적용이 안된다.

# 4. IOS 버프 인증서 작업

- 기존 인증서 제거  설정 - 일반 - VPN 및 기기 관리 - 구성 프로파일에 인증서 선택후  인증서 제거 (구성프로파일이 안보이면 인증서가 없는 것)
- 프록시 설정 후 http://burp 접속하여 인증서 다운 
- 설정 - 프로파일이 다운로드됨 클릭 - 인증서 설치 
- 일반 - 정보 - 하단 인증서 신뢰설정 - on 
- google 들어가보면 잘 잡히는 것을 확인 할 수 있다. 
   처음에 바로 안잡히면 조금 기다리거나 , 인증서 신뢰설정을 다시 off - on 시도 



# 5. kali linux 

## 1. foxproxy 없이

* apt-get update
* burpsuite 입력 및 설치 
* 최신버전 설치 하라고 하면 그대로 설치 
* fire fox  에서 설정 에서 proxy로 검색 
* manual proxy configuration  에서 127.0.0.1  8080입력 하단 also 체크 
* naver 들어가면 인증서 설치 표시 
* 버프스위트 열어서 proxy > options > proxylistener 하단 import/export CA 클릭
* Export - Certificate in DER format 선택  
* 저장 위치 바탕화면
* bs.der로 설치 
* 다시 firefox - 설정 - Privacy&Security - Cerificates - View Certificates - import - 앞서 설치한 bs.der폴더 선택 후 열기 
* trust this CA to identify websites 체크 > ok
* 다시 네이버 열면 잘됨 

## 2. foxproxy 사용
* firefox 에서 add ons 클릭 
* 검색 창에서 fox proxy 검색 > 첫번째 Foxproxy standard 클릭
* add to firefox 선택
* 브라우저 상단에 모듈 버튼에서 foxproxy 선택 > options 선택
* add  > title: burpsuite , proxytype: http , ip: 127.0.0.1, port:8080  > save
* 브라우저 settings > proxy > Use system proxy settings 클릭 
* 상단 브라우저 foxproxy >  turnoff 아래, 등록한 burpsuite 선택 
* 이후 버프스위트 동작시 패킷 캡쳐 가능 



reference 
https://programforlife.tistory.com/45


# Mac

## 1. 인증서 설치 

1. burp - open browser - http://burp 접속 - CA 다운 
2. 실행 - 키체인 설정 - 시스템 키체인 - PortSwigger CA 파일 신뢰 옵션 - 항상신뢰로 변경 
3. google 접속 시 https 빨간줄 사라짐 

