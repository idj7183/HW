# Day20 HW

### 1. 1 ~ 100000 까지 출력하는 for문을 작성하고 소요된 시간(밀리초)를 출력하세요
### 2. 년, 월을 입력 받고 해당 월을 달력형태로 출력하세요. (토요일마다 줄바꿈이 일어나도록) 
### 3. 사용자가 -1을 입력할 때까지 문자열을 입력 받고
- (1) 입력된 문자열 중 소문자 'a'의 개수를 출력하세요.
- (2) 비출력문자(공백,엔터 등)을 제외한 문자의 총 개수를 출력하세요.

```
import java.util.Calendar;
import java.util.Scanner;

/**
 * 
 * @author DONGJIN IMQ
 * @version 1.0
 * 
 */

public class HW {
	static Scanner sc = new Scanner(System.in);
	
	/**
	 * @return 1~100000 사이 정수 출력과 출력하는데 걸린 시간
	 */
	public static void one() {
		long a = System.currentTimeMillis();
		for(int i =0;i<100000;i++) {
			System.out.println(i+1);
		}
		long b = System.currentTimeMillis();
		System.out.println("소요 시간 : "+ (b-a));
	}
	
	/**
	 * @param year 원하는 연도
	 * @param month 원하는 달
	 * 
	 * @return 달력
	 */
	public static void two(int year, int month) {
		Calendar cal = Calendar.getInstance();
		
		StringBuilder sb = new StringBuilder();
		
		sb.append("일\t");
		sb.append("월\t");
		sb.append("화\t");
		sb.append("수\t");
		sb.append("목\t");
		sb.append("금\t");
		sb.append("토\n");
		
		cal.set(year,(month-1),1);
		int end = cal.get(Calendar.DAY_OF_WEEK);
		int endday = cal.getActualMaximum(Calendar.DAY_OF_MONTH);
		
		int cnt = 0;
		for(int i =0;i<end-1;i++) {
			cnt++;
			sb.append("\t");
		}
		sb.append(1+"\t");
		
		for(int i =2;i<=endday;i++) {
			
			if(cnt==6){
				sb.append("\n"); cnt = -1;
			}
			
			sb.append(i+"\t");
			cnt++;
		}
		System.out.println(sb);
	}


	/**
	 * 
	 * @param sb 비어 있는 Stringbuilder
	 * @return 공백을 제외한 문자열과 sb에 포함되어 있는 a 개수
	 */
	public static void three(StringBuilder sb) {
		int cnt = 0;
		while(true) {
			System.out.print("문자열을 입력해주세요(종료는 -1을 입력해주세요) : ");
			String tmp = sc.nextLine();
// sc.nextLine()을 사용한 이유 : sc.next()를 사용하면 'a                -1'을 입력할 경우 a와 -1로 알아들어 함수가 종료됨
			if(tmp.equals("-1")) {
				System.out.println("a 개수 : " + cnt);
				System.out.println("공백을 제외한 문자열 : " + sb);
				break;
			}
			
			String str = tmp.replace(" ", "");
			
			String tmp2 = str.replace("a", "");
			cnt += str.length() - tmp2.length();
			sb.append(str);
		}
	}
	
	public static void main(String[] args) {
		one(); //1번 실행
		
		System.out.print("연도와 월을 입력해주세요 : ");
		int year = sc.nextInt();
		int month = sc.nextInt();
		two(year,month); //2번 실행
		
		sc.nextLine();
		//three()메서드에서 sc.nextLine()을 사용하기 때문에 sc.nextInt() 이후 남아있는 공백을 제거해준다.
		StringBuilder sb = new StringBuilder();
		three(sb); //3번 
	}
}
```
## 실행 결과

**1번 실행결과**

+ `1~100000출력값은 너무 많아 생략하겠습니다`

소요 시간 : 297

**2번 실행결과**	

+ 연도와 월을 입력해주세요 : **2020 2**

![제목 없음](https://user-images.githubusercontent.com/72785706/96362458-642eed00-1168-11eb-86a1-25d6ef214deb.png)

+ 컴퓨터에 저장된 2020년 2월 달력

![제목 없음](https://user-images.githubusercontent.com/72785706/96362852-5f1f6d00-116b-11eb-9430-f2c290fb8bdc.png)

**3번 실행결과**

![제목 없음](https://user-images.githubusercontent.com/72785706/96362829-15368700-116b-11eb-8d50-243db49cca13.png)

* * *
## 4번 문제
+ 회원가입과정은 다음과 같습니다.
	+	 이메일을 입력 받는다.
	+	 비밀번호를 2번 입력받는다.
	
+ 이때 다음 조건에 충족하면 저장, 그렇지 않으면 해당 항목을 재입력 받으세요
	+	이메일 조건
		- @ 를 포함하여야 한다.
		- com, co.kr, net 중 하나로 끝나야 한다
		- 메일서버(naver, gmail, hanmail 등) 이름을 포함해야 한다.
		- 아이디가 있어야 한다.
		- 공백이 있다면 제거한다.
	+	비밀번호 조건
		- 4자 이상 20자 이하여야 한다.
		- (선택사항) 특수기호, 숫자, 대소문자가 최소 1개씩 모두 있어야 한다. (String 클래스의 matches()사용)
		- 두 비밀번호가 동일해야 한다.

+   모두 정상적인 입력을 받았다면 사용자의 id, 패스워드, 이메일을 출력하세요.
	+ id 는 이메일의 @ 앞 부분을 추출합니다.
	+ 비밀번호는 앞 두 글자만 출력하고 나머지는 '*'로 대체합니다.
		-	예) pika1234 ==> pi******
	+ 이메일은 모두 출력합니다.


```
import java.util.ArrayList;

public class Email {
	
	private static Email instance;
	//Email을 추가할 때마다 naver, gmail, hanmail 등의 메일서버나 도메인명이 중복되어 저장될 수 있기 때문에 
	// 싱글톤 패턴을 사용하였다.

	private static ArrayList<String> mail_server = new ArrayList<String>();
	private static ArrayList<String> domain_name = new ArrayList<String>();
	
	private static ArrayList<String> id = new ArrayList<String>();
	private static ArrayList<String> r_passwd = new ArrayList<String>();
	
	private Email() {
		mail_server.add("naver");
		mail_server.add("gmail");
		mail_server.add("hanmail");
		
		domain_name.add("com");
		domain_name.add("co.kr");
		domain_name.add("net");
		// Email 객체를 생성할 때 메일서버와 도메인명 3개씩을 미리 저장해놓는다. 싱글톤 패턴이므로 한 번만 사용된다.
	}
	
	public static Email getInstance() {
		if(instance==null) {
			instance = new Email();
		}
		return instance;
	}
	
	/**
	 * 
	 * @param tmp 아이디
	 * @param passwd  비밀번호1
	 * @param passwd2  비밀번호2
	 * 
	 * @return 모든 조건을 만족시키는 아이디와 비밀번호면 DB에 해당 내용을 저장한다.
	 */
	void DB(String tmp, String passwd, String passwd2) {
		String reg = "^[a-zA-Z]+[0-9]+[0-9][a-zA-Z]*@[a-zA-Z0-9-]+\\.+[a-zA-Z0-9.]+$";
		
		/*
		 * <정규식 표현> : 스스로 공부한 거라 틀린게 있을 수도 있습니다. 있으면 수정 부탁드립니다.
		 * (정규식 넘나 어려운 거 같습니다...)
		 * 
		 * <이메일 조건>
		 * 1. @를 포함하여야 한다. & 아이디가 있어야 한다. & 숫자와 알파벳이 조합되어 있어야 한다(스스로 추가한 조건)
		 * 	[아이디]@[사이트 형식]으로 입력이 되어야 한다는 의미이다.
		 * 	또한, 일반 아이디에는 특수문자를 포함시키지 않는다
		 *  오직 0-9, a-z, A-Z만 포함시킨다고 가정하자.
		 *  이 정규식은 공백도 허용하지 않기 때문에 이 정규식과 비교하기 전에 공백을 없애주는 과정이 선행되어야한다.
		 *  [a-z]+[0-9]+[0-9][a-z]* : 이메일 형식은 무조건 알파벳으로 시작하며, 숫자와 알파벳이 혼합되어 있어야 한다
		 *                            무조건 내용이 입력되어야 한다.(+로 설정해준 이유)
		 *  @는 꼭 포함되어야 하기 때문에 @를 붙여줬다.
		 *  naver.com, gmail.co.kr 등은 도메인명이 저장되어 있는 DB를 사용해야 하기 떄문에 정확한 구분까지는 불가하다
		 *  (즉, 내가 natev를 쳤을 때 natev가 존재하는 메일 사이튼지 정규식으로 구분하기는 힘들다)
		 *  하지만, 최상위 도메인과 상위 도메인을 나누는 .은 무조건 들어가는 것은 알 수 있다.
		 *  [a-zA-Z0-9-]+\\.+[a-zA-Z0-9.]+ : .이전에 사이트 이름에는 알파벳 대소문자, 숫자, -가 들어갈 수 있다
		 *                                   .이후에는 최상위 도메인이 입력되는데, 대소문자, 숫자, .이 들어갈 수 있다
		 *                                   .이전, 이후 내용은 무조건 입력되어야 하므로 +를 사용했다.
		 */
	
		if(tmp.equals("-1")) {
			System.out.println("잘못된 입력 형태입니다!");
			return;
		}
		
		String tmp2 = tmp.replace(" ", "");
		/*
		 *	2. 공백이 있으면 제거한다
		 *	공백은 " "과 같기 때문에, " "를 ""로 대체해줘 제거해준다.
		 *	앞으로 id 조건 확인은 공백을 제거한 tmp2로 할 것이다.
		 */
		
		if(!tmp2.matches(reg)) {
			System.out.println("잘못된 입력 형태입니다!");
			return;
		}
		// 위에 설명한 정규식의 형태를 못지켰으면 저장 할 수 없다.

		boolean real = false;
		
		for(String s:domain_name) {
			if(tmp2.endsWith(s)) {
				real = true;
				break;
			}
		}
		
		if(!real) {
			System.out.println("잘못된 입력 형태입니다!");
			return;
		}
		//저장된 도메인명으로 끝나지 않으면 종료시킨다.

		String[] tmparr = tmp2.split("@");
		// 정규식에서 밝혔듯 @는 이메일명과 사이트 이름을 나눠주는 구간밖에 사용할 수 없으므로 무조건 
		// 이메일명과 사이트 이름으로 나눠진다.
		
		real = false;
		
		for(String s:mail_server) {
			if(tmparr[1].startsWith(s)) {
				real = true;
				break;
			}
		}
		//메일서버는 항상 @다음에 바로 표시되므로, tmparr[1]의 첫 부분에 존재하게된다.
		
		if(!real) {
			System.out.println("잘못된 입력 형태입니다!");
			return;
		}
		//메일서버에 포함되어 있지 않으면 종료시킨다.
		
		if(tmparr[0].length()<4||tmparr[0].length()>20) {
			System.out.println("잘못된 입력 형태입니다!");
			return;
		}
		// 추가한 조건 : 아이디는 4자 이상 20자 이하이다.
		// 여기까지 통과했으면 이메일 형태에는 문제가 없다.
		
		
		if(!passwd.equals(passwd2)) {
			System.out.println("잘못된 입력 형태입니다!");
			return;
		}
		//패스워드 입력 2개 값이 같지 않으면 저장하지 않는다.
		
		String pattern = "^(?=.*[0-9])(?=.*[a-z])(?=.*[A-Z]).{4,20}$";
		/*
		 * 모든 복잡한 코드의 원흉이다.
		 * (괜히 정규식 아이디에도 적용해보겠다고 하다가 시간이 기하급수적으로 늘었다....)
		 * ?=.*[0-9]는 사이트에선 알려줬는데, 내가 생각한 이유는 이러하다
		 * 무조건 0-9가 포함되어야 하는데, ?=를 사용하고 무조건 사용하면 ?=+가 입력될수도 있을 것 같았다
		 * 하지만 =+라는 패턴은 존재하지 않았다(아마 +=때문이 아닐까 싶다)
		 * 따라서 .을 통해 무조건 한 글자는 입력 받고, 이렇게 입력받은 숫자가 
		 * [0-9]패턴에 존재하는지 확인하는게 아닐까 싶다.
		 * (사실 이 부분은 진짜 모르겠습니다.... 그냥 제 생각엔 이런 것 같아서 써봤습니다)
		 * .{4,20}을 통해, 전체 패스워드 길이가 4자 이상 20자 이하인 것도 검증 가능하다
		 */
		if(!passwd.matches(pattern)) {
			System.out.println("잘못된 입력 형태입니다!");
			return;
		}
		//위 정규식 형태를 갖추지 못했다면 비밀번호로 입력될 수 없다.
		//만약 여기까지 통과했다면 이제야 비밀번호와 아이디를 입력할 수 있다.
		id.add(tmp2);
		r_passwd.add(passwd);
		return;
	}
	
	void print() {
		for(int i =0;i<id.size();i++) {
			System.out.println("아이디 : "+id.get(i).split("@")[0]);
			String tmp = r_passwd.get(i).substring(0,2)
				     +r_passwd.get(i).substring(2,r_passwd.get(i).length()).replaceAll(".", "*");
			System.out.println("비밀번호 : "+tmp);
		}
	}
	//이번 과제엔 필요 없지만, 메일 서버와 도메인 서버를 추가시키는 함수도 있으면 좋을 것 같다.
}


import java.util.Calendar;
import java.util.Scanner;

/**
 * 
 * @author DONGJIN IM
 * @version 1.0
 * 
 */

public class HW {
	static Scanner sc = new Scanner(System.in);
	
	public static void main(String[] args) {
	
		Email e = Email.getInstance();
		
		while(true) {
			System.out.print("이메일을 입력해주세요(종료를 원하시면 -1번을 주세요) : ");
			String tmp = sc.nextLine();
			if(tmp.equals("-1")) {
				break;
			}
			
			System.out.print("비밀번호를 입력해주세요 : ");
			String passwd = sc.nextLine();
			System.out.print("비밀번호를 다시 입력해주세요 : ");
			String passwd2 = sc.nextLine();
			
			e.DB(tmp, passwd, passwd2);
		}
		
		e.print();
	}
}
```
## 실행 결과
+ 이메일을 입력해주세요(종료를 원하시면 1번을 눌러주세요) : @naver.com
+ 비밀번호를 입력해주세요 : WJgnUCQZ1
+ 비밀번호를 다시 입력해주세요 : WJgnUCQZ1
+ 잘못된 입력 형태입니다!
+ 이메일을 입력해주세요(종료를 원하시면 1번을 눌러주세요) : Daven32       @          naver.com
+ 비밀번호를 입력해주세요 : WJgnUCQZ1
+ 비밀번호를 다시 입력해주세요 : WJgnUCQZ1
+ 이메일을 입력해주세요(종료를 원하시면 1번을 눌러주세요) : Daven31@hanmail.net
+ 비밀번호를 입력해주세요 : wJgnUCQZ1
+ 비밀번호를 다시 입력해주세요 : wJgnUCQZ1
+ 이메일을 입력해주세요(종료를 원하시면 1번을 눌러주세요) : Daven30@gmail.co.kr
+ 비밀번호를 입력해주세요 : wjgnUCQZ1
+ 비밀번호를 다시 입력해주세요 : wjgnUCQZ1
+ 이메일을 입력해주세요(종료를 원하시면 1번을 눌러주세요) : Daven29naver.com
+ 비밀번호를 입력해주세요 : wjgnUCQZ1
+ 비밀번호를 다시 입력해주세요 : wjgnUCQZ1
+ 잘못된 입력 형태입니다!
+ 이메일을 입력해주세요(종료를 원하시면 1번을 눌러주세요) : Daven29@naver.com
+ 비밀번호를 입력해주세요 : dddddAAAAA
+ 비밀번호를 다시 입력해주세요 : dddddAAAAA
+ 잘못된 입력 형태입니다!
+ 이메일을 입력해주세요(종료를 원하시면 1번을 눌러주세요) : Daven29@naver.com
+ 비밀번호를 입력해주세요 : dddddAAAAA3
+ 비밀번호를 다시 입력해주세요 : dddddAAAAA3
+ 이메일을 입력해주세요(종료를 원하시면 1번을 눌러주세요) : Daven28@naver.com
+ 비밀번호를 입력해주세요 : AAdd33
+ 비밀번호를 다시 입력해주세요 : AAdd3
+ 잘못된 입력 형태입니다!
+ 이메일을 입력해주세요(종료를 원하시면 1번을 눌러주세요) : -1

## 프린트 결과
+ 아이디 : Daven32
+ 비밀번호 : WJ*******
+ 아이디 : Daven31
+ 비밀번호 : wJ*******
+ 아이디 : Daven30
+ 비밀번호 : wj*******
+ 아이디 : Daven29
+ 비밀번호 : dd*********
* * *
## 알게된 점
여기서 쓰는 것도 뭣하지만 위에 코드를 javadoc파일을 만드려하면 실패하는 것을 알 수 있다.

알고보니 javadoc은 영문만 저장 가능한 것 같다.(한국말은 에러가 뜬다)

javadoc 생성을 위해서는 주석과 도큐먼트 주석 모두 영어로 쓰는 습관을 들여야겠다












