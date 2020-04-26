---
description: 'static , non static method'
---

# enum의  기본 메소드

**Static Methods**  
  
1. valueOf\(String arg\)

> String 으로 넘긴 값을 기준으로 enum의 원소를 리턴한다. 즉, USACoins.PENNY 와 USACoins.valueOf\("PENNY"\)은 같다.

2. valueOf\(Class&lt;T&gt; class, String arg\)

> 클래스를 넘겨서 받는다. 즉, USACoins.PENNY와 USACoins.valueOf\( USACoins.class, "PENNY"\); 는 같다.  내부적으로 valueOf\(String arg\)는 이 메쏘드를 호출다.

3. values\(\)

> enum의 요소들을 enum 타입의 배열로 리턴다. USACoins.values\(\) 는  
> new USACoins\[\]{USACoins.PENNY, USACoins.NICKLE, USACoins.DIME  , USACoins.QUARTER } 와 같다.

**Non Static Method**  
  
1. name\(\)

> 호출된 값의 이름을 리턴다.  
> USACoins.PENNY.name\(\) 은 "PENNY" 이라는 String 값을 리턴다.

2. ordinal\(\)

> 정의된 순서\(index \)를 리턴다. 0부터 시작한다.  
> 즉, USACoins.PENNY.ordinal\(\) 은 0을 USACoins.NICKLE.ordinal\(\)은 1을 리턴한다.

3. compareTo\(E o\)

> E는 자기 자신으로  USACoins의 경우는 USACoins가 된다.  
> compareTo\(\)는 ordinal\(\)을 호출해서 비교한다. 요소들 간에 일정한 순서가 있을 때 쓰면 된다.\(요일이나 월 , 직급등\)  
> 모든 enum은 Comparable을 구현하고 있다. Comparable 인터페이스에는 정의된 compareTo 메쏘드를 구현한 것이다.

{% code title="EnumMethodUse.java" %}
```java
package sample.enumtest;

import java.util.ArrayList;
import java.util.List;

public class EnumMethodUse {

	public static void main(String[] args) {
	
		USACoins coin = USACoins.PENNY;
		USACoins coin2 = USACoins.valueOf( USACoins.class, "PENNY"); 
		USACoins coin3 = USACoins.valueOf("PENNY");
		
		System.out.println(coin);
		System.out.println(coin2);
		System.out.println(coin3);

		// 요소들 출력
		for(USACoins value : USACoins.values()){
		    System.out.println(value);
		}
		
		System.out.println(coin.name());
		System.out.println(coin.ordinal());
		
		List<USACoins> coins = new ArrayList<USACoins>(); 
		coins.add(coin);
		coins.add(coin2);
		coins.add(coin3);
		System.out.println("coins의 0번째 데이터가 PENNY인가?" +
						    (coins.get(0).compareTo(coin)==0?"맞다":"아니다"));
		System.out.println("coins의 0번째 데이터가 DIME인가?" +
						    (coins.get(0).compareTo(USACoins.DIME)==0?"맞다":"아니다"));
	}

}
```
{% endcode %}



