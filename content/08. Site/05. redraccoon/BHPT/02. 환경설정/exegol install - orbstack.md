
**현재 환경**

```
OS - mac 
version - sonoma 
cpu - m3 pro 
homebrew - installed
```

# 1. Requirements

## git 
- 현재 설치 되어있음

```
git
```

## python3 

```
// python3 설치
brew install python3

// 이름 변경
alias python=python3 
```

## docker

- docker desktop 사용하실 분 만 아니면 곧바로 orbstack 설치 

```
brew install --cask docker
```

- 설치 후 docker 앱 실행 해서 완벽히 설치


## docker 삭제 방법

> [https://docs.docker.com/desktop/uninstall/](https://docs.docker.com/desktop/uninstall/)

``` 
설정 - 일반 - 저장공간 - 응용프로그램 - docker 삭제

//잔여파일 삭제
rm -rf ~/Library/Group\ Containers/group.com.docker
rm -rf ~/Library/Containers/com.docker.docker (이거는 동작이 잘 안됨)
rm -rf ~/.docker
```


## orbstack

> https://orbstack.dev/download

```
brew install orbstack
```

- orbstack 앱 실행 - docker 선택

- docker 실행

```
docker run -p 80:80 docker/getting-started
```

- http://localhost:80/tutorial/  접속 될 경우 실행 완료


# 2. Exegol 설치 

- 소스에서 설치 로 진행 

```
git clone "https://github.com/ThePorgs/Exegol"

python3 -m pip install --user --requirement "Exegol/requirements.txt"
```

-  Exegol path 설정

```
sudo ln -s "$(pwd)/Exegol/exegol.py" "/usr/local/bin/exegol"

// 아래 진행해라고 해서 진행 
cd Exegol 
sudo python3 -m pip install --upgrade -r requirements.txt

// 다시 
exegol
```

- Exegol install 

```
exegol install 

full
```


# 3. Exegol 실행 및 사용법 

- Exegol start  (최초 실행 컨테이너가 생성됨)

```
// 최초 실행 (컨테이너 생성) 
// vpn 옵션을 줘야 기능이 추가됨 
exegol start bhpt --vpn /Users/[로컬유저명]/Desktop/redraccoon/BHPT/[bhpt랩ovpn파일명].ovpn 

full 

// 컨테이너 생성 이후 
exegol start bhpt

//ex 명령어
exegol start bhpt --vpn /Users/mac/Desktop/redraccoon/BHPT/1100610612922425374.ovpn
```

- 실행 후 ifconfig 해서 tun0가 나오는지 확인 ! 
- 설치 하고 나면 orbstack에서도 컨테이너 및 이미지 확인 가능 

- Exegol 컨테이너 종료

```
exit 

exegol stop bhpt //컨테이너명
```


- Exegol start 명령어

```
exegol start -h
```


- Exegol remove  명령어

```
// 생성된 컨테이너 삭제
exegol remove bhpt 
```


- 시간 변경

```
// exegol 컨테이너 접속 후 해당 명령어 실행
sudo ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime

// 추후 
Share timezone: Off -> on 변경방법 찾기 
```

- tmux 사용 

```
exegol start --shell tmux
```

## 4. VPN

- 만약 처음 컨테이너 생성시 vpn을 추가하지 않았다면 다음과 같은 방법 이 있음 
- exegol referece에 있지만 저는 잘 동작하지 않았습니다. 

```
"YOLO" 선택 : 컨테이너 생성 시(즉, 컨테이너를 처음 "시작"할 때) 컨테이너에서 openvpn을 실행하고 VPN을 시작할 수 있도록 컨테이너에 모든 권한을 부여합니다. 명령은 다음과 같아야 합니다. exegol start <container_name> <image_name> --privileged
```


# 5. X11 설치

> orbstack 에서는 지원해주지 않는듯


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

# 6. Docker 로 접속 방법

1. 컨테이너 실행 
```
docker container start exegol-bhpt
```

2. 실행 중인 컨테이너 목록 
```
docker ps -a
```

3. 컨테이너 종료 및 삭제
```
docker container stop exegol-bhpt

// 삭제
docker rm exegol-bhpt
```

5. 실행한 컨테이너 접속 방법
	- -it는 표준 입출력 을 열고 tty를 통해 접속 하겠다는 의미 
	- 컨테이너명 뒤에 접속 시 어떤 쉘을 사용할지 선택가능 bash가 표준이기에 bash로 적용 
```
docker exec -it exegol-bhpt /bin/bash
```

6. docker image 목록
```
docker images
```

7. docker image 삭제 
```
docker rmi nwodtuhs/exegol:full
```

8. docker image download
	- docker hub에서 해당 이미지 다운 
```
docker pull nwodtuhs/exegol:full
```

7. 컨테이너 생성
```
docker run --name exegol-bhpt nwodtuhs/exegol:full-3.1.2 -e="DISPLAY" --volume="$HOME/.Xauthority:/root/.Xauthority:rw"

docker run -v ~/.Xauthority:/root/.Xauthority -e DISPLAY=192.168.219.106:0 nwodtuhs/exegol:full

```

```
docker run -v ~/.Xauthority:/root/.Xauthority -e DISPLAY=$ip:0 sshipway/xclock
```


8. exegol update 이후
```
python3 -m pip install --user --requirement "Exegol/requirements.txt"
```


10. /.exegol/entrypoint.sh 경로 위치
```
/Users/mac/Exegol/exegol-docker-build/sources/install
```


> reference
> https://exegol.readthedocs.io/en/latest/getting-started/install.html#installation 
> https://gist.github.com/sorny/969fe55d85c9b0035b0109a31cbcb088



