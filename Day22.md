# Day21
### 문제
  - 1\. 단어 추가
  - 2\. 단어 검색\n"
  - 3\. 모든 단어 보기\n"
  - 4\. 퀴즈 풀기 \n
  - 0\. 종료\n입력 : ";
    + 키 : 한국어
    + 값 : 영어
### 코딩
```
import java.util.Map.Entry;
import java.util.HashMap;
import java.util.Random;
import java.util.Scanner;
import java.util.Set;

public class HW {
	
	private static final int ADD = 1;
	private static final int SEARCH = 2;
	private static final int SEE_ALL = 3;
	private static final int QUIZ = 4;
	private static final int EXIT = 0;

	public static void main(String[] args) {
	
		HashMap<String, String> word = new HashMap<>();
		Scanner sc = new Scanner(System.in);
		Random rc = new Random();
		
		while(true) {
			System.out.println("1. 단어 추가\n"
					+ "2. 단어 검색\n"
					+ "3. 모든 단어 보기\n"
					+ "4. 퀴즈 풀기 \n"
					+ "0. 종료");
			System.out.print("입력 : ");
			
			int k = sc.nextInt();
			sc.nextLine();
			
			switch(k) {
			case ADD:
				System.out.print("한글 : ");
				String tmp = sc.nextLine();
				System.out.print("영어 : ");
				String tmp2 = sc.nextLine();
				tmp = tmp.trim();
				tmp2 = tmp2.trim();
				word.put(tmp, tmp2);
				break;
			case SEARCH:
				System.out.print("찾으시는 단어를 입력해주세요 : ");
				tmp = sc.nextLine();
				
				if(!word.containsKey(tmp)) {
					System.out.println("존재하지 않는 키워드입니다!");
					break;
				}
				
				System.out.println("해당 단어의 영어는 " +word.get(tmp)+"입니다");
				break;
				
			case SEE_ALL:
				Set<Entry<String,String>> set = word.entrySet();
				for(Entry<String,String> e:set) {
					System.out.println("한글 : " + e.getKey() +"/영어 : "+e.getValue());
				}
				break;
				
			case QUIZ:
				System.out.print("Quiz를 몇 번 보시겠습니까 ? ");
				int recur = sc.nextInt();
				sc.nextLine();
			
				String[] mkeys= new String[word.size()];
				word.keySet().toArray(mkeys);
				
				for(int i =0;i<recur;i++) {
					int ran = rc.nextInt(word.size());
					
					System.out.println(mkeys[ran]+"를 영어로 표시해보세요");
					System.out.print("정답 : ");
					tmp = sc.nextLine();
					tmp = tmp.trim();
					
					if(word.get(mkeys[ran]).equals(tmp)) {
						System.out.println("정답!");
						continue;
					}
					System.out.println("오답!");
				}
				break;
				
			case EXIT:
				return;
				
			default:
				System.out.println("잘못된 입력입니다");
			}
		}
	}
}
```
* * *
## 결과값
```
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 1
한글 : 사과
영어 : apple
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 1
한글 : 바나나
영어 : banana
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 1
한글 : 파인애플
영어 : pineapple
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 2
찾으시는 단어를 입력해주세요 : 사과
해당 단어의 영어는 apple입니다
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 3
한글 : 사과/영어 : apple
한글 : 바나나/영어 : banana
한글 : 파인애플/영어 : pineapple
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 4
Quiz를 몇 번 보시겠습니까 ? 1
파인애플를 영어로 표시해보세요
정답 : pineapple
정답!
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 0
```

