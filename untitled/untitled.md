---
description: 'Generics  타입, 타입파라매터'
---

# Parameterized type

### 제네릭타입 = 제네릭 클래스 + 제네릭 인터페이스  

### 제네릭 클래스 ==&gt; class  클래스명 &lt;타입매개변수, , &gt;

### 제네릭 인터페이스 ==&gt; interface 인터페이스명 &lt;타입매개변수, , &gt;

#### 제네릭 타입은 하나이상의 타입 매개파라매터\(type parameter\)를 선언하고 있는 클래스/인터페이스를 제네릭 클래스 또는 제네릭 인터페이스라 하고 이를 합쳐서 말하는 것, 간단히 말하면  내부에서 사용할 멤버변수의 타입을 매개변수로 가지는 클래스와 인터페이스를 말한다. 

매개변수화 타입 \(Parameterized type\) 에는 실 타입 매개변수\(Actual type parameter\) 와 형식 타입 매개변수\(Formal type parameter\)가 있다 List &lt;String&gt; list ; ==&gt; &lt;String&gt; 은 실 타입 매개변수이고 ,                  public interface List&lt;E&gt; { ...} ==&gt; 에서 &lt;E&gt;는 형식 타입 매개변수다. 

### **&lt;T&gt;** 

1. 클래스 정의시 Object  대신 타입변수 T 사용 

> * Object로 대입 : 인스턴스 생성시 타입변수 T 자리를 생략하면 Object로 파생된 모든 객체자료형의 인스턴스가 들어간다. 
> * 지정한 실제 타입 : **어느** 한가지 자료형만 사용하게 되므로 형변환을 생략가능하다.

{% code title="GiftBox.java" %}
```julia
package sample.generics;

public class GiftBox<T> {
	private T contents;

	public T getContents() {
		return contents;
	}

	public void setContents(T contents) {
		this.contents = contents;
	}

	@Override
	public String toString() {
		return "Box [contens=" + contents + "]";
	}
}

```
{% endcode %}

```java
package sample.generics;

public class GiftBoxGenericUse {
	public static void main(String[] args) {
		GiftBox box = new GiftBox();
		box.setContents("과자");
		// error 
		// Type mismatch: cannot convert from Object to String
		//String contents1 =box.getContens();
		String contents1 =(String)box.getContents();
				
		GiftBox<String> box2 = new GiftBox<String>();
		box2.setContents("꽃");
		String contents2 =box2.getContents();
	}
}

```

> 위 예에서 9행에 에러가 나는 이유는 getContentsString\(\)의 리턴자료형이 Object인데 String으로 받기 때문이다. 이에 반해 14행은 String을 리턴하므로 에러가 발생하지 않는다.

### 멀티 타입 파라미터 &lt;K,V,...&gt; ****

> 제네릭 타입은 두 개 이상의 멀티 파라미터를 콤마로 구분하여 이용할 수 있다.

{% code title="CodeMap.java" %}
```java
package sample.generics;

import java.util.HashMap;

public class CodeMap<K, V> {
	private K key;
	private V value;
	
	public void put(K key, V value) {
		this.key = key;
		this.value = value;
	}
	public V get(K key) {
		return value;
	}
//생성자 , setter , getter 
	@Override
	public String toString() {
		return "CodeMap [key=" + key + ", value=" + value + "]";
	}
}
```
{% endcode %}

```java
package sample.generics;

public class CodeMapGenericUse {
	public static void main(String[] args) {
		Person p1=new Person("Kim123", "김말자", "서울");
		CodeMap<Integer, Person> codeMap = new CodeMap<Integer, Person>();
		codeMap.put(1, p1);
	
		Person person = codeMap.get(2);
		System.out.println(person);
		
		CodeMap<Integer, Person> codeMap2 = new CodeMap<Integer, Person>();
		codeMap2.put(1,p1);
		
		System.out.println(codeMap2);
	}
}

```

### 제네릭 메소드\(Generic method\) &lt;T, R&gt; R method\(T t\) <a id="4981"></a>

> 클래스나 인터페이스에 제네릭을 사용하듯이 메소드에도 제네릭을 적용할 수 있다. 주로 static  메소드에 쓰인다. 제네릭 메소드의 타입 매개변수를 선언할 때 타입 매개변수의 위치는 메소드의 접근 지시자와 반환 타입 사이이다.

public &lt;타입파라미터, ...&gt; 리턴타입 메소드명\(매개변수, ...\) { ... }

{% code title="" %}
```java

package sample.generics;

import java.util.HashMap;

public class CodeMap<K, V> {
	private K key;
	private V value;
	
	public void put(K key, V value) {
		this.key = key;
		this.value = value;
	}
	public V get(K key) {
		return value;
	}
	public static <K,V> boolean valueCompare(CodeMap<K, V> c1,CodeMap<K, V> c2 ) {
		return c1.key.equals(c2.key) && c1.value.equals(c2.value);
	}	
//생성자 , setter , getter 
	@Override
	public String toString() {
		return "CodeMap [key=" + key + ", value=" + value + "]";
	}
}
```
{% endcode %}

```java
package sample.generics;

public class CodeMapGenericUse {
	public static void main(String[] args) {
		Person p1=new Person("Kim123", "김말자", "서울");
		CodeMap<Integer, Person> codeMap = new CodeMap<Integer, Person>();
		codeMap.put(1, p1);
	
		Person person = codeMap.get(2);
		System.out.println(person);
		
		CodeMap<Integer, Person> codeMap2 = new CodeMap<Integer, Person>();
		codeMap2.put(1,p1);
		System.out.println(codeMap2);
		
		boolean res=CodeMap.valueCompare(codeMap, codeMap2);
		System.out.println(res);
	}
}

```

