# 와일드 카드 '?'

### 상속관계이거나 제한을 두지 않는 등의 여러 타입에 대한 대입이 가

###  **공변\(covariant\)** &lt;? extends T&gt; : Upper bounded wildcard, 구체적인 방향으로 타입 변환을 허용하는 것 \(자기 자신과 자식 객체만 허용\) 즉, T와 sub클래스만 가능 

###  **반공변\(contravariance\)** &lt;? super T&gt; : Lower bounded wildcard, 추상적인 방향으로의 타입 변환을 허용하는 것\(자기 자신과 부모 객체만 허용\) 즉, T와 super클래스만 가능 

###  **무공변\(invariant\)** &lt;T&gt; : 오로지 자기 타입만 허용하는 것

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



