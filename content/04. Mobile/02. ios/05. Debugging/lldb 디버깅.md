https://woowah.tistory.com/27
https://eunbin00.tistory.com/83
https://hyeyoo.com/64


**lldb로 앱 실행** 

putty  앱 있는 폴더 경로 이동 
```
// 앱 있는 폴더 경로 먼저 이동 
/var/containers/Bundle/Application/

// lldb로 앱실행 준비 
lldb [앱이름]  

// 바로 실행 
run 
r 

// break point 먼저 걸고 실행해도 됨.
```

**break point 걸기**
```
b [break point]
```

**다음줄 실행 next , n**
```
n
```

**함수 안으로 들어가기 step , s**
```
s
```

**break point 건너뛰기**
```
c
```

**lldb 종료**
```
exit
```

**이미 실행 중인 앱 attatch**
```
lldb-10

process attach -n [앱명칭]
```


(lldb) br s -a [서브주소]+[앱베이스주소]

**종료 후 해당 이름 가져와서 b 걸기**
```
b pthread_kill
```


```
register read
```


**모든섹션 덤프**

```
image dump sections [AppName] 
image dump sections safari
```

```
// 두번째 container의 좌측 첫번째 주소값 가져오기  
0x0000000100cfc000 
```

앱베이스 주소는 매번 변경됨 

```
image list

[0]   ... 0x00000001048b400   <- 앱베이스주소 
```

위 주소가 frida , Module.findBaseAddress('Oliveyoungmall'); 로 가져온 주소와 동일 

0x02db1e00