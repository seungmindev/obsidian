
# 1. frida-ios-dump 다운

```
git clone https://github.com/AloneMonkey/frida-ios-dump.git
```

- pip 패키지 업데이트
```
pip3 install -r requirements.txt --upgrade
```

- 오류 1 - pip패키지 업데이트 시 
```
WARNING: The scripts pip, pip3, pip3.11 and pip3.9 are installed in '/Users/mac/Library/Python/3.9/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.

#경로 설정 추가 
export PATH="$PATH:/Users/mac/Library/Python/3.9/bin"
```

- 오류 2 - pip패키지 업데이트 시 
```
WARNING: You are using pip version 21.2.4; however, version 23.3.1 is available.
You should consider upgrading via the '/Library/Developer/CommandLineTools/usr/bin/python3 -m pip install --upgrade pip' command.

# 요청대로 명령어 입력
python3 -m pip install --upgrade pip
```

- dump.py 스크립트 수정
```
ip iphone
port 22 
```

- ipa 압축 풀기
```
tar -xvzf 예스24\ 티켓.ipa
```
