
# java  삭제 및 재설치 

> https://www.imymac.com/ko/powermymac/uninstall-adoptopenjdk-mac.html
> https://androidmillions.codejava.net/java-se/uninstall-jdk-on-macos


1. terminal창에 다음 명령을 복하여 붙여넣습니다.
    1. sudo rm -fr /Library/Internet\ Plug-Ins/JavaAppletPlugin.plugin
    2. sudo rm -fr /Library/PreferencesPanes/JavaControlPanel.prefPane
    3. sudo rm -fr ~/Library/Application\ Support/Oracle/Java
2. 두번째로는 /Library/Java/JavaVirtualMachines/ 에 있는 jdk<본인버전> 디렉토리를 통째로 삭제합니다.

3. openjdk 위치 검색
```
which java

// 해당 경로 이동 후 삭제
rm -rf 경로/대상/OpenJDK
// 예시
rm -rf /opt/homebrew/opt/openjdk@17
```

4. oracle-jdk 설치 
```
brew install --cask oracle-jdk
```

# 1. frida
1. python version check
	- 만약 파이썬 3만 설치되어있거나 파이썬3가 설치되어있는데 파이썬2로만 인식된다면
		2번으로 가서 alias 설정을 합니다.
```
$ python --version 
```

2. python3 to python
```
$ vim ~/.zshrc

//맨 하단에 아래 구문 추가
alias python="python3"

//저장 후 나와서 다음 명령어 실행
$ source .zshrc

//이후 버전확인 
$ python --version
```

3. pip 
```
// pip 또는 pip3 설치여부 확인
$ pip
$ pip3 

// 둘다없을 경우 pip 설치
$ python3 -m pip install --upgrade pip

// pip3 명령어만 인식할 경우 alias 추가
위 python3 참고 
```

4. frida 
```
$ pip install frida-tools
```



6. adb
```
$ brew install --cask android-platform-tools

// 안드로이드 usb 연결 후 adb 실행
$ adb shell 
```

7. frida server download 

> https://github.com/frida/frida/releases 

```
// 기기 CPU ABI 확인 
$ adb shell getprop ro.product.cpu.abi 

// 압축 파일명 변경 방법
$ unxz frida-server-16.1.4-android-x86.xz
$ mv frida-server-16.1.4-android-x86 frida-server

// 디바이스에 넣기
$ adb root
$ adb push frida-server /data/local/tmp/
$ adb shell "chmod 755 /data/local/tmp/frida-server
```

8. android 디바이스 frida server 실행
```
// 안드로이드 디바이스에 usb 연결 후 실행
$ adb shell 

// 접속 후
$ cd /data/local/tmp 
$ ls
> frida-server-16.1.10-android-arm64

// 현재 실행중인 frida 서버 확인 
$ ps -ef | grep fri 

// 없을 경우 실행 &는 백그라운드에서 실행 되게 한다는 의미
$ ./frida-server-16.1.10-android-arm64 & 
```

9. frida 테스트
```
$ frida-ps -Uai

// 오류 발생
> Failed to enumerate applications: unable to find process with name 'system_server' 

// 해결 
로컬 버전과 안드로이드 기기 버전 일치 
```


# 2. fridump3

1. 파일 다운로드  및 압축해제
	https://github.com/rootbsd/fridump3 

```
// 압축해제
tar -zxvf fridump3-master.zip
```

2. 테스트
```
python fridump3.py -u -r [pid] -s 
```


# 3. jadx
```
$ brew install jadx

// jadx 실행
$ jadx-gui [apk파일명]
```
# 4. apk tool for mac

> apk easy tool 을 mac bash 스크립트로 변환 

- apk easy tool 도 안드로이드 apk tool 사용
- 안드로이드 스튜디오가 설치되어 있어야 함

- apk split 파일의 경우 sap 프로그램 또는 apktool m 어플을 사용하여 
	분리된 파일을 하나로 합쳐 줘야한다. 
	https://secuworm.tistory.com/7
	[apktoolm]https://maximoff.su/apktool/?lang=en

1. apk 추출
```
cd /상위경로/Apktool for Mac/In
adb pull /sdcard/apks/예스24\ 티켓.apk
```

2. 디컴파일 옵션 (apk easy tool)
```
--only-main-classes
```

3. recompile 옵션 (apk easy tool)
```
--use-aapt2 
```

4. signing 옵션
```
--v4-signing-enabled false 
```

5. apk push
```
adb push 예스24\ 티켓_zipa.apk /sdcard/apks/
```


> reference 
> https://apktool.org/docs/cli-parameters


# 5. android-file-transfer 


1. adb pull 사용
```
adb pull /sdcard/apks/예스24\ 티켓.apk
```

2. android-file-transfer (설치는 안해봄)
```
brew install --cask android-file-transfer
```
