# Recursive type bound 재귀적 타입 바운드

재귀적 타입 바운드는 타입 매개변수가 자신을 포함하는 수식에 의해 한정되는 것으로 `Comparable` 인터페이스와 가장 많이 사용된다.

```java
public interface Comparable<T> {
    int compareTo(T o);
}
```

 타입 매개변수 `T`는 자신과 비교될 수 있도록 비교대상을 요소로 정의한 것이다.`Comparable`을 구현하는 요소들의 목록을 sort, max, min 값을 구하기 위해서는 목록의 모든 요소들이 서로 비교 가능해야 한다. 

```java
static <T extends Comparable<T>> T max(List<T> list) {
    Iterator<T> iterator = list.iterator();
    T result = iterator.next();
    while (iterator.hasNext()) {
        T t = iterator.next();
        if (t.compareTo(result) > 0) result = t;
    }

    return result;
}
```

 1번행 `<T extends Comparable<T>>` ==&gt;  자신과  비교될  수 있는 모든  자료형 T라는 뜻이다. 

