---
description: 용어 및 컬렉션의 제네릭 사용해보자
---

# Generics 클래스 사용

**간단히 제네릭을 알아보자**   
  
1. 컬렉션에 적용된 예  

> java.util.List와 Iterator의 선언부를 발췌한 것이다 으로 List &lt;E&gt; 로 선언되어 있어서 Obejct로 부터 파생된 모든 객체자료형은 올 수 있다 .

```bash
public interface List<E> { 
    void add(E x);
    Iterator<E> iterator();
}
public interface Iterator<E> { 
    E next();
    boolean hasNext();
}
```

> String 객체의 list를 만들고 싶다면 . List  객체 생성시 List를 구성하는 요소에 String 이라고 표시 하면 된다. 
>
>  List를 구성하는 것이 String이라고 선언을 미리 했으므로 형변환 이 필요하지 않다.  .

```bash
package sample.generics;

public class Person {
	private String id;
	private String name;
	private String addr;
	
	..........
	}
////////////////////////////////////////	
package sample.generics;

import java.util.ArrayList;
import java.util.Date;
import java.util.List;

public class ListESample {

	public static void main(String[] args) {
	
		List list1 = new ArrayList();
		list1.add(new Date());
		list1.add(new Person("kim123","김말자","서울"));
		
		for(int i=0; i<list1.size();i++) {
			if(list1.get(i) instanceof Person) {
				System.out.println(list1.get(i));
			}
		}
		
		List<Person> list2 = new ArrayList<Person>();
		//error
		//The method add(Person) in the type List<Person> is not applicable for the arguments (Date)
		//list2.add(new Date());
		list2.add(new Person("kim123","김말자","서울"));
		list2.add(new Person("park123","박말자","울산"));
		for(int i=0; i<list2.size();i++) {
			//Person의 인스턴스인지 확인할 필요가 없이 원하는 데이터를 사용할 수있다
			System.out.println(list2.get(i));
			
		}
	}
}
```



