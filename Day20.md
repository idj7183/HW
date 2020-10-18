# Day20 HW
* * *

<pre>
<code>
public static void one() {
		long a = System.currentTimeMillis();
		for(int i =0;i<100000;i++) {
			System.out.println(i+1);
		}
		long b = System.currentTimeMillis();
		System.out.println("소요 시간 : "+ (b-a));
	}
</code>
</pre>
