# Simple example

## 두수의 사칙연산 

```java
package lambda.bit;

interface Operator {
	public int opFunc(int a, int b);
}

public class LambdaTest1 {
	// 람다식 문법 (매개변수 목록)->{실행문}
	public static void exec(Operator op) {
		int k = 10;
		int m = 20;
		int value = op.opFunc(k, m);
		System.out.println(value);
	}

	public static void main(String[] args) {
		exec((i, j) -> {
			return i + j;
		});
		exec((i, j) -> {
			return i - j;
		});
		exec((i, j) -> {
			return i * j;
		});
		exec((i, j) -> {
			return i / j;
		});
	}
}

```

## 두수 중 큰수 와 작은 수 찾기

```java
package lambda.bit;

public class LambdaTest2 {
	@FunctionalInterface // 함수형 인터페이스 체크 어노테이션
	public interface MyNumber {
		int get(int num1, int num2);
	}

	public static void main(String[] args) {
		MyNumber max = (x, y) -> (x >= y) ? x : y;
		MyNumber min = (x, y) -> (x <= y) ? x : y;
		int a = 10;
		int b = 30;
		System.out.println(a+" , "+b+"중 큰수 " + max.get(a, b));
		System.out.println(a+" , "+b+"중 작은수 " + min.get(a, b));
	}
}

```

## Thread run\(\) 호출 

```java
package lambda.bit;
public class ThreadLambdaTest {
	
	public static void main(String[] args) {
		
		Thread thread1 = new MyThread();
		thread1.start();
		//////////////////////////////////
		
		Thread thread2 = new Thread(){
			public void run() {
				System.out.println("Hello World!!#1");
			}
		};
		thread2.start();
		//////////////////////////////////
		
		new Thread(()->{
			System.out.println("Hello World!!#2");
		}).start();
		
	}
}
class MyThread extends Thread {
	public void run() {
		System.out.println("Hello World!!#3");
	}
}
```

## Runnable run\(\) 호출 

```java
package lambda.bit;
public class RunnableLambdaTest {
    public static void main(String[] args) {
        Runnable runnable = () -> {
            for (char ch='A'; ch <= 'z'; ch++) {
                System.out.print(ch);
            }
        };
        Thread thread = new Thread(runnable);
        thread.start();
    }
}
```



