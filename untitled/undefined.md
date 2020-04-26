# 와일드 카드 '?'

### 상속관계이거나 제한을 두지 않는 등의 여러 타입에 대한 대입이 가

### &lt;? extends T&gt; : 와일드 카드의 상한제한, 즉, T와 sub클래스만 가능 

### &lt;? super T&gt; : 와일드 카드의 하한제한, 즉, T와 super클래스만 가능 

### &lt;?&gt; , &lt;? extends  Object&gt; : 제한없음

```java
package sample.generics;

public class GiftBoxGenericInvariantUse {
	public void someMethod(GiftBox<Number> box) {
		/****/
	}
	public void someMethod2(GiftBox<? extends Number> box) {
		/****/
	}
	public void someMethod3(GiftBox<? super Number> box) {
		/****/
	}
	
	public static void main(String[] args) {
		GiftBoxGenericInvariantUse a= new GiftBoxGenericInvariantUse();
		
		//The method someMethod(GiftBox<Number>) in the type 
		//GiftBoxGenericInvariantUse is not applicable for the arguments (GiftBox<Integer>)
		//a.someMethod(new GiftBox<Integer>());
		
		a.someMethod2(new GiftBox<Integer>());
		
		//The method someMethod3(GiftBox<? super Number>) in the type
		//GiftBoxGenericInvariantUse is not applicable for the arguments (GiftBox<Integer>)
		//Integer는 Number의 슈퍼클래스가 아니므로 error
		//a.someMethod3(new GiftBox<Integer>());
		
		// Object는 Number의 슈퍼클래스이므로 가능
		a.someMethod3(new GiftBox<Object>());
	}
}

```



