
https://saltlee.tistory.com/158

getbooleanExtra()
: string, defaultvalue 

onCreate() {

Intent intent = getIntent();

variable = intent.getBooleanArrayExtra(name)  
variable = intent.getBooleanExtra(name, defaultValue)
intent의 값을 받을 때는 위와 같이 메소드를 사용.  
Array의 경우는 defaultValue 값 설정이 없음  
기본 데이터형의 경우는 defaultValue 설정  
  
**※ defaultValue**
Activity의 값이 넘어 올 때 제대로 넘어 올 수 있지만 name등이 틀리거나 잘 못된 값이 올 수 있음  
변수 선언할때 기본 데이터값을 설정하듯이(int n = 0;) name에 해당하는 값이 없는 경우 설정되는 값

출처: [https://sshbug.tistory.com/23](https://sshbug.tistory.com/23) [SsonG's:티스토리]