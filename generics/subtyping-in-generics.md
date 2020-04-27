# Subtyping in generics제네릭의 서브타이핑

제네릭 클래스나 인터페이스를 상속관계로 정의하고 매소드의 매개변수로 상속관계의 제네릭을 사용하려면 주의를 기울여야 한다.

```java
public void someMethod(Number n) { 
   /* ... */
 }
~~~~~~~

someMethod(new Integer(10));   // OK
someMethod(new Double(10.1));   // OK
~~~~~~~~~
Box<Number> box = new Box<Number>();
box.add(new Integer(10));   // OK
box.add(new Double(10.1));  // OK
```

Integer 와 Double은 Number와 상속관계이므로 문제가 없지만 다음 코드는 에러가 발생한다

```text
public void someMethod(Box<Number> n) { 
   /* ... */
 }
~~~~~~~

someMethod(new Box<Integer>());   // error
someMethod(new Box<Double>());   // error
```

1행의 Box&lt;Number&gt;는 Box&lt;Integer&gt;의 슈퍼타입도 서브타입도 아니므로  제네릭 클래스나 인터페이스를 상속관계로 정의하여 다형성적으로 사용하려면 다음에 나오는 와일드 카드 \(?\)를 사용 하여야 한다. 

```text
public void someMethod(Box< ? etends Number> n) { 
   /* ... */
 }
~~~~~~~

someMethod(new Box<Integer>());   // ok
someMethod(new Box<Double>());   // ok
```

```text
package sample.generics;

public class GiftBoxGenericInvariantUse {
	public void someMethod(GiftBox<Number> box) {
		/****/
	}
	public void someMethod2(GiftBox<? extends Number> box) {
		/****/
	}
	public static void main(String[] args) {
		GiftBoxGenericInvariantUse a= new GiftBoxGenericInvariantUse();
		//The method someMethod(GiftBox<Number>) in the type 
		//GiftBoxGenericInvariantUse is not applicable for the arguments (GiftBox<Integer>)
		//a.someMethod(new GiftBox<Integer>());
		a.someMethod2(new GiftBox<Integer>());
		
	}
}

```

