# What is Lambda?

## 단순화된 구조로 입력과 출력을 가능하게 하는 익명화된 함수 표기법

> 함수인데 함수명을 따로 만들지 않고서  호출하는 방식

## 사용법 

### \(매개변수, ...\) -&gt; { 실행문 ... }

> \(매개변수, ...\)는 { 실행문 } 블록을 실행하기 위해 필요한 값을 제공한다.  매개 변수의 이름은 일반매개변수와 같이 명시하면된다. 매개변수 자료형은 명시하지 않아도 된다. -&gt; 기호는 매개 변수를 이용해서 { 실행문 } 의 내용을  실행한다는 뜻이다

![](../.gitbook/assets/image%20%281%29.png)

```bash
@FunctionalInterface
interface Say{
    int something(int a,int b);
}
//////////////////////////////////
class Person{
    public void hi(Say line) {
	int number = line.something(3,4);
	System.out.println("Number is "+number);
    }
}
```

```bash
람다식 사용X #1

Say say= new Say() {
    public int something(int a, int b) {
	System.out.println("#1");
	System.out.println("#2");
	System.out.println("매개변수 number is "+a+","+b);
	return 2020;
    }
};

Person rin = new Person();
rin.hi(say);
```

```bash
람다식 사용X #2

Person rin = new Person();
rin.hi(new Say() {
    public int something(int a, int b) {
	System.out.println("#1");
	System.out.println("#2");
	System.out.println("매개변수 number is "+a+","+b);
	return 2020;
    }
});
```

```bash
람다식 사용 

Person rin = new Person();
rin.hi((a,b) ->{
	System.out.println("#1");
	System.out.println("#2");
	System.out.println("매개변수 number is "+a+","+b);
	return 2020;
});
```

 예제 전체 자바 파일 

{% code title="Say.java" %}
```java
package sample.lambda;
@FunctionalInterface
public interface Say {
	int something(int a,int b);
	// @FunctionalInterface을 사용해서 메소드가 추가되면 에러발생
	//int something2(int a,int b); 
}

```
{% endcode %}

{% code title="Person.java" %}
```java
package sample.lambda;

public class Person {
	public void hi(Say line) {
		int number = line.something(3, 4);
		System.out.println("Number is " + number);
	}
}

```
{% endcode %}

{% code title="PersonUse.java" %}
```java
package sample.lambda;

public class PersonUse {
	public class 이름이있는Inner클래스 implements Say{
		 public int something(int a, int b) {
				System.out.println("매개변수 number is "+a+","+b);
				return a+b;
		}
	}
	public void lambadaNoUse() {
		Say  say = new 이름이있는Inner클래스();
		Person rin = new Person();
		rin.hi(say);
	}
	public void lambadaNoUse1() {
		Say say= 
			new Say() {// 익명 inner 클래스의 인스턴스 생성문
			    public int something(int a, int b) {
				System.out.println("#1");
				System.out.println("#2");
				System.out.println("매개변수 number is "+a+","+b);
				return 2020;
		    }
		};
		Person rin = new Person();
		rin.hi(say);
	}
	public void lambadaNoUse2() {
		Person rin = new Person();
		rin.hi(
				new Say() {// 익명 inner 클래스의 인스턴스 생성문 , 
					        // 재사용 불가 이유는 인스턴스를 참조하는 레퍼런스가 없어서
				    public int something(int a, int b) {
					System.out.println("#1");
					System.out.println("#2");
					System.out.println("매개변수 number is "+a+","+b);
					return 2020;
			    }
			}	
		);
	}
	public void lambadaUse1() {
		Say say= 
				/*new Say() {// 익명 inner 클래스의 인스턴스 생성문
				    public int something*/(int a, int b)-> {
					System.out.println("#1");
					System.out.println("#2");
					System.out.println("매개변수 number is "+a+","+b);
					return 2020;
			    }
			/*}*/;
			Person rin = new Person();
			rin.hi(say);
	}
	public void lambadaUse2() {
		Person rin = new Person();
		rin.hi(
				/*new Say() {// 익명 inner 클래스의 인스턴스 생성문 , 
					        // 재사용 불가 이유는 인스턴스를 참조하는 레퍼런스가 없어서
				    public int something*/(int a, int b)-> {
					System.out.println("#1");
					System.out.println("#2");
					System.out.println("매개변수 number is "+a+","+b);
					return 2020;
			    }
			/*}*/	
		);
	}
	public void lambadaUse2_2() {
		Person rin = new Person();
		rin.hi(
				/*new Say() {// 익명 inner 클래스의 인스턴스 생성문 , 
					        // 재사용 불가 이유는 인스턴스를 참조하는 레퍼런스가 없어서
				    public int something*/( a,  b)-> {
					System.out.println("#1");
					System.out.println("#2");
					System.out.println("매개변수 number is "+a+","+b);
					return 2020;
			    }
			/*}*/	
		);
	}
	
	public static void main(String[] args) {
		PersonUse new_PersonUse인스턴스참조자=new PersonUse();
		new_PersonUse인스턴스참조자.lambadaNoUse() ;
		System.out.println("/////");
		new_PersonUse인스턴스참조자.lambadaNoUse1() ;
		System.out.println("/////");
		new_PersonUse인스턴스참조자.lambadaNoUse2() ;
		System.out.println("/////");
		new_PersonUse인스턴스참조자.lambadaUse1() ;
		System.out.println("/////");
		new_PersonUse인스턴스참조자.lambadaUse2() ;
	}

}







```
{% endcode %}

