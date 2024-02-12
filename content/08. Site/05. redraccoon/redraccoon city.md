
# 01. 접근법

```
ssh rcity<번호>@ctf.redraccoon.kr -p 31338
```

# 02. 명령어

- txt 확장자 전체 검색
```
find . -name "\*.txt"
```

- grep 
```
// 대소문자 무시 검색
cat flag.txt | grep 'flag is here' -i

// 전체 파일 시스템에서 "password"라는 단어가 포함된 파일 찾는 방법
grep -r "password" /
```

- file type 확인
```
file [파일명] 

// 파일 유형만 출력
file -b [파일명]
```

- elf  파일 읽기  
```
//파일에서 인쇄가능한 문자열 출력 
strings flag 

//binary file 확인
xxd flag

// elf파일 정보들? 확인
readelf -h flag 
```

- port 검색 netcat 
netcat 은  nc로 줄여 쓸 수 있음 
```
// 1-9999 범위의 포트 검색
netcat -z -v 127.0.0.1 1-9999


```

# 03. key

```
07 : h5Z8D2G4cW7L6x0R3f9
08 : F6jR2K3qH1gW7X5b0S9
```

