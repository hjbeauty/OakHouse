---
description: 'enum이란, 서로 연관된 상수들의 집합'
---

# 열거 자료형\(enumerated type\), enum\(열거형상수\)

## enum이란, 서로 연관된 상수들의 집합                                  

#### public  abstract  class  Enum &lt;E extends Enum&gt;  extends Object  implements Comparable, Serializable                                                           enum은 class , interface 와 같은  하나의 클래스를 만드는 명령어.           Object로 부터 확장\(상속받고\)되고 Comparable과 Serializable을 구현한 추상클래스로 비교와 직렬화가 가능한 '객체'이다.   

enum을 정의 하는 방법으로 연속된 데이타를 갖도록 정의하는 것과 불연속데이터로 초기화를 시키는 방법이 있다.

### [연관된 상수를 만드는 방법 - final static  ](final-static.md)

### [연속 데이터 열거형 상수](continuity-data.md)

### [enum의 기본 메소드 ](base-method.md)

### [불연속 데이터 열거형 상수 ](discontinuity-data.md)

### [enum 장점/단점](benefits-drawbacks.md)

### [https://docs.oracle.com/javase/tutorial/reflect/special/enum.html](https://docs.oracle.com/javase/tutorial/reflect/special/enum.html)

## 비트 서초152기 조사자료 

{% tabs %}
{% tab title="4회차팀-1조 과제" %}
{% embed url="http://cafe.daum.net/OakHouse/Sdm0/12" caption="2020.04.22 과제\(제네릭, enum, 알고리즘\) - 김하현" %}

![](http://cfile260.uf.daum.net/image/99A2E5475EA02B2A1BE024)

>

{% embed url="http://cafe.daum.net/OakHouse/Sdm0/13" caption="2020.04.22 과제 남윤대" %}

```text
enum
           enum이란 관련이 있는 상수들의 집합이다.
           흔히 상수를 정의할 때 final static string과 같은 방식으로 상수를 정의한다.
           하지만 이렇게 정의해서 코딩하는 경우 다양한 문제가 발생하낟.
           이 문제점을 보완하기 위해 자바 1.5버전부터 새롭게 추가된 것이 enum이다.
           enum은 열거형이라고 불리며, 서로 연관된 상수들의 집합을 의미한다.
           어떤 클래스가 상수만으로 작성되어 있으면 반드시 class로 선언할 필요는 없다.
           이럴 때 class로 선언된 부분에 enum이라고 선언하면 이 객체는 상수의 집합이라는 것을
           명시적으로 나타낸다. enum은 enumeration이라는 셈, 계산, 열거, 목록이라는 영단어의
           앞부분만 따서 만든 예약어이다.
enum의 특징
           1. 열거형으로 선언된 순서에 따라 0부터 index 값을 가진다.(순차적으로 증가)
           2. enum 열거형으로 지정된 상수들은 모두 대문자로 선언한다.
           3. 열거형 변수들을 선언한 후 마지막에 세미콜론(;)을 찍지 않는다.
           4. 상수와 특정 값을 연결시킬 경우 마지막에 세미콜론(;)을 붙여줘야 한다.
enum의 장점

           1. 코드가 단순해지며, 가독성이 좋다.
           2. 인스턴스 생성과 상속을 방지하여 상수값의 타입안정성이 보장된다.
           3. enum class를 사용해 새로운 상수들의 타입을 정의함으로 정의한 타입 이외의 타입을 가진
               데이터값을 컴파일 시 체크한다.
           4. 키워드 enum을 사용하기 때문에 구현의 의도가 열거임을 분명하게 알 수 있다.
```

**enum 메소드**

![](http://cfile248.uf.daum.net/image/998C25485EA046952C7D56)

```text
원하는 enum Type 가져오는 방법
           1. enum형 객체를 만들어서 가져오기. -> DevType tp1 = DevType.MOBILE;
           2. valueOf() 메소드를 이용해서 가져오기. -> DevType tp2 = DevType.valueOf(“WEB”)
```
{% endtab %}

{% tab title="4회차팀-2조 과제" %}
{% embed url="http://cafe.daum.net/OakHouse/Sdlz/9" caption="2020.04.22 - 과제 김로만" %}

```text
enum in Java
Enumerations serve the purpose of representing a group of named constants in a programming language. For example the 4 suits in a deck of playing cards may be 4 enumerators named Club, Diamond, Heart, and Spade, belonging to an enumerated type named Suit. Other examples include natural enumerated types (like the planets, days of the week, colors, directions, etc.).
Enums are used when we know all possible values at compile time, such as choices on a menu, rounding modes, command line flags, etc. It is not necessary that the set of constants in an enum type stay fixed for all time.

In Java (from 1.5), enums are represented using enum data type. Java enums are more powerful than C/C++ enums . In Java, we can also add variables, methods and constructors to it. The main objective of enum is to define our own data types(Enumerated Data Types).

Every enum constant is always implicitly public static final. Since it is static, we can access it by using enum Name. Since it is final, we can’t create child enums.
We can declare main() method inside enum. Hence we can invoke enum directly from the Command Prompt.
Enum and Inheritance :

All enums implicitly extend java.lang.Enum class. As a class can only extend one parent in Java, so an enum cannot extend anything else.
toString() method is overridden in java.lang.Enum class,which returns enum constant name.
enum can implement many interfaces.
values(), ordinal() and valueOf() methods :

These methods are present inside java.lang.Enum.
values() method can be used to return all values present inside enum.
Order is important in enums.By using ordinal() method, each enum constant index can be found, just like array index.
valueOf() method returns the enum constant of the specified string value, if exists.
// Java program to demonstrate working of values(), 
// ordinal() and valueOf() 
enum Color 
{ 
    RED, GREEN, BLUE; 
} 
  
public class Test 
{ 
    public static void main(String[] args) 
    { 
        // Calling values() 
        Color arr[] = Color.values(); 
  
        // enum with loop 
        for (Color col : arr) 
        { 
            // Calling ordinal() to find index 
            // of color. 
            System.out.println(col + " at index "
                             + col.ordinal()); 
        } 
  
        // Using valueOf(). Returns an object of 
        // Color with given constant. 
        // Uncommenting second line causes exception 
        // IllegalArgumentException 
        System.out.println(Color.valueOf("RED")); 
        // System.out.println(Color.valueOf("WHITE")); 
    } 
} 
Output :

RED at index 0
GREEN at index 1
BLUE at index 2
RED
```

{% embed url="http://cafe.daum.net/OakHouse/Sdlz/10" caption="2020.04.22 과제 - 이찬영" %}

```text
2. Java Enum

>> enum이란?

- 데이터 중에서 몇 가지로 한정된 값만을 갖는 경우가 있다.

- 예를 들어 계절 : 봄, 여름, 가을, 겨울

- 이렇게 한정된 값만을 가지는 데이터 타입이 Enumeration Type (enum)이다.

>> 예제

- Season.java
package com.example.demo.Enum;
public enum Season {
	SPRING,SUMMER,AUTUMN,WINTER
}

- EnumUse.java
package com.example.demo.Enum;
public class EnumUse {
	public static void main(String[] args) {
		Season season = Season.SPRING;
		System.out.println(season);
	}
}


결과)
SPRING

////////////////////////////////
- FirstName.java
package com.example.demo.Enum;
public enum FirstName {
	LEE("이"),
	PARK("박"),
	SUNG("성");

	private final String name;

	FirstName(String name) {
		this.name = name;
	}
	
	public String getName() {
		return name;
	}
}

- FirstNameUse.java

package com.example.demo.Enum;



public class FirstNameUse {

	

	public static void main(String[] args) {

		FirstName[] first = FirstName.values();

		for(FirstName name : first)

			System.out.println(name);

		for(FirstName name : first)

			System.out.println(name.getName());

	}

}


결과)
LEE
PARK
SUNG
이
박
성

```
{% endtab %}

{% tab title="4회차팀-3조 과제" %}
{% embed url="http://cafe.daum.net/OakHouse/Sdly/14" caption="2020.04.22 과제 - 고재현" %}

```text
Enum 이란 ?

 서로 연관된 상수들의 집합을 의미합니다.



평소 열거형 상수를 선언하려면 다음과 같이 했다.

1.   클래스 내에 final static 로 변수 선언
2.   interface 에 상수선언

기존방식의 문제
한 클래스에 final static 으로 다 선언하자니 네임충돌 발생할 수도 있고, 복잡함
인터페이스를 사용하면 위 문제는 해결되나, 타입안정성이 떨어짐 
(컴파일 때 형검사를 하지 않으므로 오류발생 소지)
enum의 장점
코드가 단순해지고, 가독성이 짱
인스턴스 생성과 상속을 방지하여 상수값의 타입안정성이 보장 (컴파일 때 체크)
enum 키워드를 사용해서 구현의 의도가 열거임을 분명히 나타냄



예제를 통해 쉽게 이해합시다



public enum BoyFriend { 
		REDBOY,
		BLUEBOY, 
		BLACKBOY;
 }


이 클래스의 class파일은 


class Compiled from"BoyFriend.java"
public final class BoyFriend extends java.lang.Enum<BoyFriend> {
		public static final BoyFriend REDBOY;
		public static final BoyFriend BLUEBOY;
		public static final BoyFriend BLACKBOY;
		public static BoyFriend[] values();
		public static BoyFriend valueOf(java.lang.String);
		static {};
}

컴파일 시 static final이 붙은걸 볼 수 있다. 
그리고 열거해준다.


사용법은 
생성자를 사용 : REDBOY("rank1","LCY") 하거나  
직접 호출 : User.REDBOY 로 호출 하거나 
메소드 사용 : User.valueOf("REDBOY") 한다.

근데 다 사용법이 달라욤 

↓생성자 이용
public enum User {
	REDBOY("111", "devljh"),
	BLUEBOY("222", "powerman"),
	BLACKBOY("333", "goodgame");
	
	private String id;
	private String nickname;
	
	
	User(String id, String nickname) {
		this.id = id; 
		this.nickname= nickname;
	}
	
	public String getId() {
		return id;
	}
	public String getNickName() {
		return nickname;
	}
}


사실 enum 은 이해가 잘 안가요 :p
```
{% endtab %}

{% tab title="4회차팀-4조 과제" %}
{% embed url="http://cafe.daum.net/OakHouse/Sdlx/9" caption="2020.04.22 박주영" %}

```text
1) Enum

#특징

-자바의 특별한 클래스이다.
-Enum은 "enumerations-특정지어 열거된" 의 약어이다.
-final 한 variables들로 이루어진 상수의 집합이다.
-enum을 만들기 위해서 enum 키워드를 사용한다. (클래스나 인터페이스를 사용하지 않는다.)

-Variables를 ","로 구분한다. 이 때, 대문자로 쓴다.


#예시

public enum Day {
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY,
    THURSDAY, FRIDAY, SATURDAY
}


public class EnumTest {
    Day day;
   
    public EnumTest(Day day) {
        this.day = day;
    }
   
    public void tellItLikeItIs() {
        switch (day) {
            case MONDAY:
                System.out.println("Mondays are bad.");
                break;
                   
            case FRIDAY:
                System.out.println("Fridays are better.");
                break;
                        
            case SATURDAY: case SUNDAY:
                System.out.println("Weekends are best.");
                break;
                       
            default:
                System.out.println("Midweek days are so-so.");
                break;
        }
    }
   
    public static void main(String[] args) {
        EnumTest firstDay = new EnumTest(Day.MONDAY);
        firstDay.tellItLikeItIs();
        EnumTest thirdDay = new EnumTest(Day.WEDNESDAY);
        thirdDay.tellItLikeItIs();
        EnumTest fifthDay = new EnumTest(Day.FRIDAY);
        fifthDay.tellItLikeItIs();
        EnumTest sixthDay = new EnumTest(Day.SATURDAY);
        sixthDay.tellItLikeItIs();
        EnumTest seventhDay = new EnumTest(Day.SUNDAY);
        seventhDay.tellItLikeItIs();
    }
}



결과:

Mondays are bad.
Midweek days are so-so.
Fridays are better.
Weekends are best.
Weekends are best.



#Enum의 장점
- 코드가 단순해진다.
- 인스턴스 생성과 상속을 방지한다. (final 하기 때문)
- enum 클래스를 통해 상수의 타입을 정의함으로써 정의한 타입의외의 것이 있는지 여부를 컴파일 시 체크한다.
- 키워드 enum 을 사용하여 구현의 의도가 열거임을 알 수 있다.
```
{% endtab %}

{% tab title="4회차팀-5조 과제" %}
{% embed url="http://cafe.daum.net/OakHouse/Sdlu/9" caption="  2020.04.22 과제 - 강정민" %}

```text
enum

- 클래스처럼 보이게 하는 상수

- 서로 관련있는 상수들끼리 모아 상수들을 정의하는것

- enum 클래스 형을 기반으로 한 클래스형 선언


 - 특징 - 

1. 열거형으로 선언된 순서에 따라 0부터 index 값을 가진다.(순차적으로 증가)

2. enum 열거형으로 지정된 상수들은 모두 대문자로 선언한다.

3. 열거형 변수들을 선언한 후 마지막에 세미콜론(;)을 찍지 않는다.

4. 상수와 특정 값을 연결시킬경우 마지막에 세미콜론(;)을 붙여줘야한다.


```

![](http://cfile249.uf.daum.net/image/99EBC53E5EA014E62FA7A3)

{% embed url="http://cafe.daum.net/OakHouse/Sdlu/10" caption="2020.04.22 과제 - 이건호" %}

```text
Enum

Enumeration은 프로그래밍 언어에서 상수의 그룹을 나타낼 때 사용한다.

Enum은 컴파일 당시 우리가 모든 가능한 값을 알고있는 경우 사용된다. 항상 enum안의 상수는 타입이 정해져 있어야 하는것은 아니다. 


Enum의 중요점

1. 모든 enum은 클래스를 사용해서 내부적으로 정의된다.

2. 모든 enum 상수들은 객체 타입의 enum이다. 

3. enum타입은 swiitch 구문의 아규먼트로 넣을 수 있다. 

4. 모든 enum은 상수는 내부적으로 public static final으로 정의되고, enum 이름으로 사용할 수 잇다. final이므로 자식enum을 만들수는 없다. 

enum내부에 main()메서드를 선언 할 수있다. 그래서 enum을 커맨드 프롬프트에서 직접 호출 할 수 있다. 


enum과 상속 
1. 모든 enum들은 내부적으로 java.lang.Enum 클래스에 의해 상속된다. 클래스는 하나의 부모 클래스에 의해서만 상속되므로, enum은 다른것을 상속할 수가 없다.

2. toString() 메서드는 java.lang.Enum 클래스에서 오버라이드 된다. 이것은 enum 상수 이름을 리턴한다.

3. enum은 다양한 인터페이스들을 상속 할 수 있다.
```

{% embed url="http://cafe.daum.net/OakHouse/Sdlu/11" caption="2020.04.22 과제 - 박지혜" %}

```text
2. Enum 열거형상수

Enum은 열거형이라고 불리며, 서로 연관된 상수들의 집합을 의미한다.

기존에 상수를 정의하는 방법이였던 final static string 과 같이 문자열이나 숫자들을 나타내는 기본자료형의 값을 enum을 이용해서 같은 효과를 낼 수 있다.



Enum의 장점

1. 코드가 단순해지며, 가독성이 좋다.

2. 인스턴스 생성과 상속을 방지하여 상수값의 타입안정성이 보장된다.

3. enum class를 사용해 새로운 상수들의 타입을 정의함으로 정의한 타입 이외의 타입을 가진 데이터값을 컴파일 시 체크한다.

4. 키워드 enum을 사용하기 때문에 구현의 의도가 열거임을 분명하게 알 수 있다.
```
{% endtab %}
{% endtabs %}







