# Day24
### 이전 영단어를 Map에 저장하는 과제에 아래 추가 조건을 성립시키도록 코딩
  1. 프로그램이 종료되면 map객체를 word.w에 저장
  2. 프로그램이 실행될 때, word.w에 저장된 map 객체를 꺼낸다.(파일이 없는 경우 그대로 진행)
  
```
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.util.Map.Entry;
import java.util.Random;
import java.util.Scanner;
import java.util.TreeMap;

class Dictionary{

	/**
	 * 
	 * @param map
	 * @return 갱신된 map객체를 word.w에 저장하고 프로그램 종료
	 */
	public void exit(TreeMap<String, String> map) {
		System.out.println("프로그램 종료");

		try(FileOutputStream out = new FileOutputStream("words.w");
			ObjectOutputStream obOut = new ObjectOutputStream(out)){
			obOut.writeObject(map);
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	
	/**
	 * 
	 * @param map
	 * @param w 영단어
	 * @return Map에 영단어의 존재여부와 영단어 형식을 검증
	 */
	public boolean check(TreeMap<String, String> map, String w) {
		String pattern = "^[a-zA-Z]*$";
		if(map.containsKey(w)) {
			System.out.println("이미 존재하는 단어입니다");
			return false;
		}
		
		if(!w.matches(pattern)) {
			System.out.println("영어가 아닙니다");
			return false;
		}
		
		return true;
	}
	
	/**
	 * 
	 * @param map
	 * @param w 영단어
	 * @param m 뜻
	 * @return 영단어와 뜻을 map에 저장. check 메서드가 true를 도출할 때만 실행되는 함수
	 */
	public void write(TreeMap<String, String> map, String w, String m) {
		map.put(w, m);
	}
	
	/**
	 * 
	 * @param map
	 * @param w 영단어
	 * @return 영단어가 map(사전)에 저장되어 있는지 확인하고, 있으면 뜻을 말해주고 없으면 미등록 단어라고 알려준다
	 *         
	 */
	public void search(TreeMap<String, String> map, String w) {
		if(map.containsKey(w)) {
			System.out.println(map.get(w));
		}
		else {
			System.out.println("미등록 단어");
		}
	}

	/**
	 * 
	 * @param map
	 * @return map에 존재하는 모든 단어 리스트 확인
	 */
	public void list(TreeMap<String, String> map) {
		StringBuilder sb = new StringBuilder();
		sb.append("---- 단어 리스트 ----\n");
		
		for(Entry<String, String> e : map.entrySet()) {
			sb.append(e.getKey() + ":" + e.getValue() + "\n");
		}
		sb.append("-----------------");
		System.out.println(sb);
	}
	
	/**
	 * 
	 * @param map
	 * @param ans 입력한 정답(한글)
	 * @param w 퀴즈로 나온 영단어
	 * @return 맞추면 정답, 틀리면 땡을 출력
	 */
	public void quiz(TreeMap<String, String> map, String ans, String w) {
		if(ans.equals(map.get(w))) {
			System.out.println("정답!");
		}
		else {
			System.out.println("땡");
		}
	}
}

public class HW {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		Random rc = new Random();
		
		TreeMap<String, String> wordMap = new TreeMap<>();
		
		try(FileInputStream input = new FileInputStream("words.w")
    
        ;ObjectInputStream oInput = new ObjectInputStream(input)) {
			TreeMap<String, String> tmp = (TreeMap<String, String>) oInput.readObject();
			wordMap.putAll(tmp); 
		} catch (FileNotFoundException e) {
			System.out.println("존재하지 않는 파일");
		} catch(Exception e) {
			System.out.println("정상적이지 않은 절차");
			return;
		}
		
		String menu = "1. 단어 추가\n" +"2. 단어 검색\n" + "3. 모든 단어 보기\n"+ "4. 퀴즈 풀기 \n" + "0. 종료\n"
   				 +"입력 : ";
		String select;
		String w, m;
		String pattern = "^[a-zA-Z]*$";
		
		Dictionary d = new Dictionary();
		boolean real;
		
		while (true) {
			System.out.print(menu);
			select = sc.next().trim();

			switch (select) {
			case "0":
				d.exit(wordMap);
				return;
				
			case "1":
				System.out.print("영단어를 입력해주세요 : ");
				w = sc.next().trim();
				real =  d.check(wordMap,w);
				if(real) {
					System.out.print("뜻을 입력해주세요 : ");
					m = sc.next().trim();
					d.write(wordMap,w,m);
				}
				break;
				
			case "2":
				System.out.print("영단어를 입력해주세요 : ");
				w = sc.next().trim();
				if(w.matches(pattern)) {
					d.search(wordMap, w);
				}
				else {
					System.out.println("영어가 아닙니다");
				}
				break;
				
			case "3":
				if(wordMap.isEmpty()) {
					System.out.println("저장된 영단어가 없습니다");
					break;
				}
				d.list(wordMap);
				break;
				
			case "4":	
				String[] arr = new String[wordMap.size()];
				wordMap.keySet().toArray(arr);
				
				int tmp = rc.nextInt(wordMap.size());
				w = arr[tmp];
				
				System.out.print(w+"의 뜻은?");
				m = sc.next().trim();
				
				d.quiz(wordMap, m, w);
				break;
			
			default:
				break;
			}
		}
	}
}
```
* * *
## 실행 결과
### 첫 번째 실행
```
존재하지 않는 파일
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 1
영단어를 입력해주세요 : word
뜻을 입력해주세요 : 단어
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 1
영단어를 입력해주세요 : wㅇrd
영어가 아닙니다
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 0
프로그램 종료
```
### 두 번째 실행
```
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 3
---- 단어 리스트 ----
word:단어
-----------------
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 1
영단어를 입력해주세요 : book
뜻을 입력해주세요 : 책
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 4
book의 뜻은?책
정답!
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 2
영단어를 입력해주세요 : book
책
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 3
---- 단어 리스트 ----
book:책
word:단어
-----------------
1. 단어 추가
2. 단어 검색
3. 모든 단어 보기
4. 퀴즈 풀기 
0. 종료
입력 : 0
프로그램 종료
```

