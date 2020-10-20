# Day21 HW
### 문제
+ User 클래스 
  - 필드 : 아이디, 패스워드, 이메일 
  - 메서드 : 
    * 1. 생성자(String, String, String)
    * 2. Getter Setter
  - toString 오버라이드 
  - hashCode 오버라이드 (자동 완성 사용)
  - String GetHiddenPassword() : 앞 두글자, 나머지 '*' 처리 
    	
+ 메뉴)
  - 1 회원 가입
  - 2 로그인  ==> 아이디, 패스워드 입력 받고 "성공!" / "실패" 출력
  - 3 모든 회원 조회 ==> 모든 회원들의 모든 정보 (비밀번호는 getHiddenPassword() 사용)
  - 4 회원 탈퇴 ==> 아이디, 패스워드 입력 받고 성공 시 삭제 진행, 없는 아이디라면 "미등록 회원" 출력
  - 5 회원 조회 (id로 검색) ==> 아이디 입력 받고 있으면 회원 모든 정보 출력, 없는 아이디라면 "미등록 회원" 출력
  - 0. 종료

```
import java.util.ArrayList;
import java.util.Scanner;

class User{
	private ArrayList<String> id = new ArrayList<>();
	private ArrayList<String> passwd = new ArrayList<>();
	private ArrayList<String> e_mail = new ArrayList<>();
	
	public User() {}
	public User(String iD, String passwd, String e_mail) {
		super();
		setId(iD);
		setPasswd(passwd);
		setE_mail(e_mail);
	}
	
	public ArrayList<String> getId() {
		return id;
	}

	public void setId(String Id) {
		id.add(Id);
	}

	public ArrayList<String> getPasswd() {
		return passwd;
	}

	public void setPasswd(String passwd) {
		this.passwd.add(passwd);
	}

	public ArrayList<String> getE_mail() {
		return e_mail;
	}

	public void setE_mail(String e_mail) {
		this.e_mail.add(e_mail);
	}
	
	@Override
	public String toString() {
		
		StringBuilder sb = new StringBuilder();
		for(int i =0;i<id.size();i++) {
			sb.append("ID : " + id.get(i)+", PASSWORD : "+GetHiddenPassword(i)+", e-mail : "+e_mail.get(i)+"\n");
		}
		
		String tmp = sb.toString();
		return tmp;
	}

	@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + ((e_mail == null) ? 0 : e_mail.hashCode());
		result = prime * result + ((id == null) ? 0 : id.hashCode());
		result = prime * result + ((passwd == null) ? 0 : passwd.hashCode());
		return result;
	}
	
	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		User other = (User) obj;
		if (e_mail == null) {
			if (other.e_mail != null)
				return false;
		} else if (!e_mail.equals(other.e_mail))
			return false;
		if (id == null) {
			if (other.id != null)
				return false;
		} else if (!id.equals(other.id))
			return false;
		if (passwd == null) {
			if (other.passwd != null)
				return false;
		} else if (!passwd.equals(other.passwd))
			return false;
		return true;
	}

	String GetHiddenPassword(int i) {
		
		StringBuilder sb = new StringBuilder();
		sb.append("비밀번호 : ");
		
		String tmp = passwd.get(i).substring(0,2)+passwd.get(i).substring(2).replaceAll(".", "*");
		
		tmp = "비밀번호 : " + tmp;
		
		return tmp;
	}
}


public class Main {
	
	public static final int Sign = 1;
	public static final int log_in = 2;
	public static final int search_all = 3;
	public static final int Sign_out = 4;
	public static final int search = 5;
	public static final int EXIT = 0;
	
	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
		User user = new User();
		
		while(true) {
			System.out.println("회원가입 1번/로그인 2번/모든 회원 조회 3번/회원 탈퇴 4번/회원 조회(id로 검색) 5번, 종료는 0번");
			
			int n = sc.nextInt();
			
			switch(n) {
			case Sign:
				System.out.print("ID를 입력해주세요 : ");
				String tmp = sc.next();
				System.out.print("비밀번호를 입력해주세요 : ");
				String tmp2 = sc.next();
				System.out.print("이메일을 입력해주세요 : ");
				String tmp3 = sc.next();
				
				user.setId(tmp);
				user.setPasswd(tmp2);
				user.setE_mail(tmp3);
				
				break;
			case log_in:
				System.out.print("ID를 입력해주세요 : ");
				tmp = sc.next();
				System.out.print("비밀번호를 입력해주세요 : ");
				tmp2 = sc.next();
				
				if(!user.getId().contains(tmp)||!user.getPasswd().contains(tmp2)) {
					System.out.println("실패");
					break;
				}
				
				System.out.println("성공!");
			break;
				
			case search_all:
				System.out.println(user.toString());
				break;
				
			case Sign_out:
				System.out.print("ID를 입력해주세요 : ");
				tmp = sc.next();
				System.out.print("비밀번호를 입력해주세요 : ");
				tmp2 = sc.next();
				
				if(user.getId().contains(tmp)&&user.getPasswd().contains(tmp2)) {
					user.getId().remove(tmp);
					user.getPasswd().remove(tmp2);
					System.out.println("삭제 성공!");
					break;
				}
				
				System.out.println("미등록 회원");
				break;
				
			case search:
				tmp = sc.next();
				
				ArrayList<String> tmp1 = user.getId();
				int index = 0;
				for(int i =0;i<tmp1.size();i++) {
					if(tmp1.get(i).equals(tmp)) {
						index = i;
						break;
					}
				}

				System.out.println("ID : " + tmp);
				System.out.println("PASSWD : "+user.GetHiddenPassword(index));
				System.out.println("E-mail : "+user.getE_mail().get(index));
				break;
				
			case EXIT:
				return;
				
			default:
				System.out.println("잘못 입력하셨습니다");

			}
			
			
		}
	}
}
```
* * *
## 실행 결과
```
회원가입 1번/로그인 2번/모든 회원 조회 3번/회원 탈퇴 4번/회원 조회(id로 검색) 5번, 종료는 0번
1
ID를 입력해주세요 : AAA
비밀번호를 입력해주세요 : BBB
이메일을 입력해주세요 : AAA@BBB
회원가입 1번/로그인 2번/모든 회원 조회 3번/회원 탈퇴 4번/회원 조회(id로 검색) 5번, 종료는 0번
1
ID를 입력해주세요 : CCC
비밀번호를 입력해주세요 : DDD
이메일을 입력해주세요 : CCC@DDD
회원가입 1번/로그인 2번/모든 회원 조회 3번/회원 탈퇴 4번/회원 조회(id로 검색) 5번, 종료는 0번
2
ID를 입력해주세요 : AAA
비밀번호를 입력해주세요 : BBB
성공!
회원가입 1번/로그인 2번/모든 회원 조회 3번/회원 탈퇴 4번/회원 조회(id로 검색) 5번, 종료는 0번
3
ID : AAA, PASSWORD : 비밀번호 : BB*, e-mail : AAA@BBB
ID : CCC, PASSWORD : 비밀번호 : DD*, e-mail : CCC@DDD

회원가입 1번/로그인 2번/모든 회원 조회 3번/회원 탈퇴 4번/회원 조회(id로 검색) 5번, 종료는 0번
4
ID를 입력해주세요 : AAA
비밀번호를 입력해주세요 : BBB
삭제 성공!
회원가입 1번/로그인 2번/모든 회원 조회 3번/회원 탈퇴 4번/회원 조회(id로 검색) 5번, 종료는 0번
4
ID를 입력해주세요 : AAA
비밀번호를 입력해주세요 : BB
미등록 회원
회원가입 1번/로그인 2번/모든 회원 조회 3번/회원 탈퇴 4번/회원 조회(id로 검색) 5번, 종료는 0번
3
ID : CCC, PASSWORD : 비밀번호 : DD*, e-mail : AAA@BBB

회원가입 1번/로그인 2번/모든 회원 조회 3번/회원 탈퇴 4번/회원 조회(id로 검색) 5번, 종료는 0번
5
CCC
ID : CCC
PASSWD : 비밀번호 : DD*
E-mail : AAA@BBB
회원가입 1번/로그인 2번/모든 회원 조회 3번/회원 탈퇴 4번/회원 조회(id로 검색) 5번, 종료는 0번
0
```



