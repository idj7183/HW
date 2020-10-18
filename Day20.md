# Day20 HW

### 1. 1 ~ 100000 까지 출력하는 for문을 작성하고 소요된 시간(밀리초)를 출력하세요
### 2. 년, 월을 입력 받고 해당 월을 달력형태로 출력하세요. (토요일마다 줄바꿈이 일어나도록) 
### 3. 사용자가 -1을 입력할 때까지 문자열을 입력 받고
####    1) 입력된 문자열 중 소문자 'a'의 개수를 출력하세요.
####    2) 비출력문자(공백,엔터 등)을 제외한 문자의 총 개수를 출력하세요.

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
			String tmp = sc.next();
			if(tmp.equals("-1")) {
				System.out.println("a 개수 : " + cnt);
				System.out.println("공백을 제외한 문자열 : " + sb);
				break;
			}
			
			String[] str = tmp.split(" ");
			
			for(int i =0;i<str.length;i++) {
				sb.append(str[i]);
				String tmp2 = tmp.replace("a", "");
				cnt += str[i].length() - tmp2.length();
				//a를 문자열에서 지워서 문자열 사이의 차이를 알아보는 방식으로 a개수를 구했다.
			}
		}
	}
	
	public static void main(String[] args) {
		one(); //1번 실행
		
		int year = sc.nextInt();
		nt month = sc.nextInt();
		two(year,month); //2번 실행
		
		StringBuilder sb = new StringBuilder();
		three(sb); //3번 
	}
}
	
```
### 실행 결과
