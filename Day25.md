# 계산기 만들기
```
import java.awt.BorderLayout;
import java.awt.Dimension;
import java.awt.Font;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Stack;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JTextField;

class Cal{
	
	private JFrame frame = null;
	private JButton[] operator;
	private JButton[] num;
	private Stack<String> stack;
	private JTextField field;
	
	/**
	 * 
	 * @param s 생성되는 계산기 창 이름
	 * @return 계산기 창
	 */
	Cal(String s) {
		if(frame == null) {
			frame = new JFrame(s);
			frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
			frame.setSize(1300,600);
			frame.setLocationRelativeTo(null);
			
			this.button();
			
			this.addAll();
		}
		frame.setVisible(true);
	}
	
	/**
	 * @return 입력된 결과값들을 출력할 메시지 창 / 버튼들 설정
	 */
	public void button(){
		
		field = new JTextField();
		field.setEditable(false);
		field.setPreferredSize(new Dimension(1300,100));
		field.setFont(new Font("맑은 고딕",Font.BOLD,25));
		field.setHorizontalAlignment(JTextField.RIGHT);
		
		
		stack = new Stack<String>();
		StringBuilder sb = new StringBuilder();
		
		
		ActionListener listener = new ActionListener() {
			
			@Override
			public void actionPerformed(ActionEvent e) {
				JButton b = (JButton) e.getSource();
				
				if("="==b.getText()) {
					int a = 0; //최종 결과
					int tmp = 0; // 중간 값
					int ten = 0;
					char opttmp = 'A';
					
					while(!stack.isEmpty()) {
						char s = stack.pop().toCharArray()[0];
						if(s>=48&&s<=57) {
							tmp += (s-'0')*((int) Math.pow(10, ten));
							ten++;
							
							if(stack.isEmpty()) {
								if(opttmp=='+') {
									a = a + tmp;
								}
								else if(opttmp=='-')	{
									a = tmp - a;
								}
								else if(opttmp=='*')	{
									a = a * tmp;
								}
								else {
									a = tmp / a;
								}
							}
						}
						else {
							
							if(opttmp == 'A') {
								a = tmp;
								opttmp = s;
							}
							
							else {
								if(opttmp=='+') {
									a = a + tmp;
								}
								else if(opttmp=='-')	{
									a = tmp - a;
								}
								else if(opttmp=='*')	{
									a = a * tmp;
								}
								else {
									a = tmp / a;
								}
										
								opttmp = s;
							}
							
							tmp = 0;
							ten = 0;
						}
					}
					
					JOptionPane.showMessageDialog(frame, ("정답 : "+a));
					System.exit(0);
				}
				else {
					stack.push(b.getText());
					sb.append(b.getText());
			
					field.setText(sb.toString());
				}
				
			}
		};
		
		num = new JButton[10];
		for(int i =0;i<10;i++) {
			num[i] = new JButton(Integer.toString(i));
			num[i].setFont(new Font("맑은 고딕",Font.PLAIN,25));
			num[i].addActionListener(listener);
		}
		
		operator = new JButton[5];
		operator[0] = new JButton("+");
		operator[1] = new JButton("-");
		operator[2] = new JButton("*");
		operator[3] = new JButton("/");
		operator[4] = new JButton("=");
		
		for(int i =0;i<5;i++) {
			operator[i].setFont(new Font("맑은 고딕",Font.PLAIN,25));
			operator[i].addActionListener(listener);
		}
	}
	
	/**
	 * @return 만들어놨던 버튼들을 frame에 붙여넣는 과정
	 */
	public void addAll(){
		frame.setLayout(new BorderLayout());
		
		JPanel p1 = new JPanel();
		p1.setLayout(new GridLayout(4,3));
		
		for(int i =0;i<9;i++) {
			p1.add(num[i+1]);
		}
		p1.add(new JPanel());
		p1.add(num[0]);
		p1.add(new JPanel());
		
		JPanel p2 = new JPanel();
		p2.setLayout(new GridLayout(1,5));
		
		for(int i =0;i<5;i++) {
			p2.add(operator[i]);
		}
		
		frame.add(field,BorderLayout.NORTH);
		frame.add(p1,BorderLayout.CENTER);
		frame.add(p2,BorderLayout.SOUTH);
	}
}


public class HW {
	public static void main(String[] args) {
		
		new Cal("계산기");
		
	}
}
//예외 처리나 처음에 음수를 입력하는 경우의 수는 배제하였습니다.
//나누기는 정수끼리의 나누기 입니다(즉, 26/5는 5.2가 아닌 5의 결과값으로 출력됨)
```
## 코딩결과
![multi](https://user-images.githubusercontent.com/72785706/97256887-a1c20300-1857-11eb-92de-fe4547ed3613.png)
![divide](https://user-images.githubusercontent.com/72785706/97256889-a38bc680-1857-11eb-80fc-4ffac3e08daa.png)
![plus](https://user-images.githubusercontent.com/72785706/97256890-a4bcf380-1857-11eb-93ca-90678d5e21c9.png)
![minus](https://user-images.githubusercontent.com/72785706/97256877-9a025e80-1857-11eb-9813-ba7b2fbb06b7.png)


