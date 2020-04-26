---
description: 'enum을 다루기 전에 enum이 나오기 전에 사용했던 방법을 먼저 알아보자. 나열형, 열거형 , 연관된 상수'
---

# 연관된 상수를 만드는 방법

#### ~~**`연관된 상수를 만드는 방법은 다음과 같다.`**~~

1.  class에 final static 변수 선언 :  

{% code title="USACoinVO.java " %}
```java
package sample.enumtest;

public class USACoinVO {
	   public static final int PENNY = 1;// 1 cent
     public static final int NICKLE = 5;//5 cent
     public static final int DIME = 10; //10 cent
     public static final int QUARTER = 25;//25 cent
}

```
{% endcode %}

2.  interface 에 변수 선언 :

{% code title="USACoinService.java" %}
```java
package sample.enumtest;

public interface USACoinService {
	  int PENNY = 1;// 1 cent
    int NICKLE = 5;//5 cent
    int DIME = 10; //10 cent
    int QUARTER = 25;//25 cent

}

```
{% endcode %}

class, interface에서 만든 상수 사용 예 :

{% code title="CoinUse.java" %}
```java
package sample.enumtest;

public class CoinUse {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int coin = 5;
		String coinStr="";
		
		switch (coin) {
		case USACoinVO.PENNY:
			coinStr="PENNY";
			break;
		case USACoinVO.NICKLE:
			coinStr="NICKLE";
			break;
		case USACoinVO.DIME:
			coinStr="DIME";
			break;
		case USACoinVO.QUARTER:
			coinStr="QUARTER";
			break;
		}
		System.out.printf("USACoinVO 클래스 사용 : %d , %s \n",coin,coinStr);
		
		switch (coin) {
		case USACoinService.PENNY:
			coinStr="PENNY";
			break;
		case USACoinService.NICKLE:
			coinStr="NICKLE";
			break;
		case USACoinService.DIME:
			coinStr="DIME";
			break;
		case USACoinService.QUARTER:
			coinStr="QUARTER";
			break;
		}
		System.out.printf("USACoinService 인터페이스 사용 : %d , %s \n",coin,coinStr);
	}//main() end

}

```
{% endcode %}

{% hint style="warning" %}
 위와 같이 연관성있는 상수를 만들어 사용할 수 있지만 몇가지 문제점이 있다.

**1**. **타입에 불안정**하다 : 실행시 타입으로 인한 문제가 발생한다                                                 ****                             **2**.  **상수자체가 의미를 전달하지 못한다.**  ****상수를 출력해도 의미를 출력하지 못한다.                                         **3**.  **No**  **namespace :** 상수에 접근하기 위해 상수명자체를 사용할 수 없다. ==&gt; 다음 예제와 같이    USACoinService.NICKLE을  import static sample.enumtest.USACoinVO.NICKLE; 이렇게 static import 로 선언후 NICKLE 을 사용하는 방법으로 namespace를 대신하여 사용한다.  
{% endhint %}

{% code title="CoinUseStaticImport.java" %}
```java
package sample.enumtest;
import static sample.enumtest.USACoinVO.PENNY;
import static sample.enumtest.USACoinVO.NICKLE;
import static sample.enumtest.USACoinVO.DIME;
import static sample.enumtest.USACoinVO.QUARTER;

public class CoinUseStaticImport {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int coin = 5;
		String coinStr="";
		
		switch (coin) {
		case PENNY:
			coinStr="PENNY";
			break;
		case NICKLE:
			coinStr="NICKLE";
			break;
		case DIME:
			coinStr="DIME";
			break;
		case QUARTER:
			coinStr="QUARTER";
			break;
		}
		System.out.printf("USACoinVO 클래스 사용 : %d , %s \n",coin,coinStr);

	}//main() end

}

```
{% endcode %}

{% hint style="warning" %}
이러한 불편한 점을 보안하여 사용되는 것이 enum 나열형상수이다.
{% endhint %}

