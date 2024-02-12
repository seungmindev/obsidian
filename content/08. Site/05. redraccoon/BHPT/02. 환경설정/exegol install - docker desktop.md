
# 1. docker desktop 설치

1. https://docs.docker.com/desktop/install/mac-install/
2. docker desktop 어플리케이션 실행
3. docker desktop 자체 동영상 학습 설명이 직관적이기 때문에 어렵지 않아 따라 해보시는걸 추천 드립니다.

# 2. X11 설치

> orbstack 에서 미지원 

1. xquartz 

> https://www.xquartz.org/

2. xquartz 실행 
```
$ open -a XQuartz

// 실행 여부 확인
ps aux | grep Xquartz
// 실행중일 경우 
> /opt/X11/bin/Xquartz :0 -listen tcp
```

3. keyboard 
```
//xorg.conf.d 경로 
/opt/X11/share/X11

//키맵핑 확인
xev

키입력하면 
keycode 와 keysym이 나온다.

//ex) a 를 눌렀을때
// keycode 8은 해당키의 x11키코드를 나타낸다. 
KeyRelease event, serial 33, synthetic NO, window 0x600001,
    root 0xc0, subw 0x600002, time 14550626, (58,60), root:(58,96),
    state 0x0, keycode 8 (keysym 0x61, a), same_screen YES,
    XLookupString gives 1 bytes: (61) "a"
    XFilterEvent returns: False
```

# 3. exegol 본격 설치

1. git 소스 설치
```
git clone "https://github.com/ThePorgs/Exegol"
```

2. 사용자로 exegol requirement 설치 
```
python3 -m pip install --user --requirement "Exegol/requirements.txt"
```

3. exegol wraper 추가
```
sudo ln -s "$(pwd)/Exegol/exegol.py" "/usr/local/bin/exegol"
```

4. exegol 자동 업그레이드 
	- 일단 패스 - 현재까지 문제 없음

5. exegol image install
```
exegol install
```

# 4. exegol 실행 및 사용법
 
1. exegol start  (최초 실행 컨테이너가 생성됨)
	- 실행 후 ifconfig 해서 tun0가 나오는지 확인 ! 
	- 컨테이너 생성시 --env 옵션은 docker-compose.yml 에 environment에 추가하는 옵션이다.
```
// 최초 실행 (컨테이너 생성) 
// vpn 옵션을 줘야 기능이 추가됨 
exegol start [컨테이너명] --vpn /[bhpt랩ovpn파일경로]/[bhpt랩ovpn파일명].ovpn --env TZ="Asia/Seoul"

full (원하는 옵션으로 설치 full은 모든 기능이 있어 용량이 큼)

// ex)
exegol start bhpt --vpn /Users/mac/Desktop/redraccoon/BHPT/2200610613922425384.ovpn --env TZ="Asia/Seoul"

// 컨테이너 실행 
exegol start bhpt
```

2. 시간변경 (혹시 위 --env 옵션으로 잘 동작 하지 않는 경우)
```
// exegol 컨테이너 접속 후 해당 명령어 실행
sudo ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime

// 도커 컨테이너 전체리스트
docker ps -a 

// 현재 도커컨테이너 시간
docker exec 9751544bd9b9 date
```


> reference 
>[exegol] https://exegol.readthedocs.io/en/latest/getting-started/install.html
>[docker-desktop]https://docs.docker.com/desktop/install/mac-install/