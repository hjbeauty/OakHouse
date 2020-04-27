---
description: enum 열거형 정의 방법및 사용법
---

# 연속 데이터 열거형 상수

###  enum 열거형이름 { 상수명1, 상수명2,… }             

앞의 예제인 USACoinVO나 USACoinService를 연속적인 상수값을 갖는 enum으로 바꾸면 다음과 같다. 

{% code title="USACoins.java " %}
```java
package sample.enumtest;

public enum USACoins{ PENNY ,NICKLE ,DIME ,QUARTER }

```
{% endcode %}

enum 자료형 사용법 : 참조형변수를 만들어서 직관적으로 사용하면된다. 단, USACoin~~ 클래스의 PENNY:1, NICKLE:5 , DIME:10, QUARTER:25 라는 값으로 매핑되지 않는다.

{% code title="ContinuityEnumUse.java" %}
```java
package sample.enumtest;

public class ContinuityEnumUse {

	public static void main(String[] args) {
		USACoins coin = USACoins.PENNY;

		switch (coin) {
		case PENNY:
			System.out.println(coin);
			break;
		case NICKLE:
			System.out.println(coin);
			break;
		case DIME:
			System.out.println(coin);
			break;
		case QUARTER:
			System.out.println(coin);
			break;
		}
	// 매핑된 값 출력
		for(USACoins value : USACoins.values()){
		    System.out.println(value);
		}
	}
}

////////////////////////////////
PENNY
PENNY
NICKLE
DIME
QUARTER
```
{% endcode %}

