---
description: <T extends  ObejctType>
---

# Bounded type parameter 제한된 제네릭

#### 제네릭 타입에 ‘extends’를 사용하면, 특정 타입으로 부터 파생된 클래스들만 대입할 수 있게 제한할 수 있다.

```java
package sample.generics;

class Fruit{
	//......
}
class Apple extends Fruit{
	//......
}
class Banana extends Fruit{
	//......
}
class Car{
	//......
}
public class FruitBox<T extends Fruit> {
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

```java
package sample.generics;

public class FruitBoxGenericUse {
	public static void main(String[] args) {
		FruitBox<Banana> fruitBox = new FruitBox<Banana>();
		//error 
		//Bound mismatch: The type Car is not a valid substitute 
		//for the bounded parameter <T extends Fruit> of the type FruitBox<T>
		//FruitBox<Car> fruitBox2 = new FruitBox<Car>();
	}
}

```

