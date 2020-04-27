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
    int someting(int a,int b);
}
//////////////////////////////////
class Person{
    public void hi(Say line) {
	int number = line.someting(3,4);
	System.out.println("Number is "+number);
    }
}
```

```bash
람다식 사용X #1

Say say= new Say() {
    public int someting(int a, int b) {
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
    public int someting(int a, int b) {
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



