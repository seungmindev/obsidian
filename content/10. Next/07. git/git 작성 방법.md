

# 1. 협업

> https://parkparkpark.tistory.com/176

1. vscode 열기
2. 좌측에 리포지토리 복제 선택
3. vscode 상단에 clone 한 url 입력 시 연동 완료 
4. vscode 에서 터미널 열기
5. git branch 현재 브랜치 확인
```
git branch 

* main 
```

6. branch 생성
```
git branch test 

// 생성 후 확인
git branch   

* main
  test
```

7. 생성 한 브런 치 접속 
```
git checkout test
Switched to branch 'seungmin'

// 다시 확인
* test
  main
```

8. 파일 수정 후 커밋 
```
git add .
git commit -m "커밋 메시지"

git push origin seungmin
```

9. 다시 깃허브의 저장소로 돌아가서 
	 main을 눌러보면 하단에 새로운 seungmin 브런치 추가 되어있음 
10. seungmin으로 들어가보면 커밋이 생기고 pr을 날릴 것인지 생긴것을 알 수 있다.
11. compare & pull request를 누르고 
	우측 리뷰어에 담당자를 추가해주고 
	정성스레 내용을 작성후 요청한다.

# 2. PR


https://velog.io/@dongvelop/Github-%ED%98%91%EC%97%85%ED%95%98%EA%B8%B0-PR%EB%B6%80%ED%84%B0-merge%EA%B9%8C%EC%A7%80