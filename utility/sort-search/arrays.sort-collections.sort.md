# Arrays.sort\(\) ,Collections.sort\(\)

## 정렬 

### 자바가 제공하는 정렬 사용방법 등.........  

####   1. Arrays.sort\(\) 배열 정렬시 사용한다

  \* Object Array에서는 TimSort\(Merge Sort + Insertion Sort\)를 사용

    Ex\)String \[\], AA \[\] 등 

  \* Primitive Array에서는  Dual-Pivot Quicksort \(Quick Sort + Insertion Sort\)를 사용

    Ex\)int \[\] , char\[\] 등 

[![&#xCCA8;&#xBD80;&#xD30C;&#xC77C;](http://i1.daumcdn.net/icon/editor/p_etc_s.gif) 20190417.zip](javascript:checkVirus%28'grpid%3DzaqT%26fldid%3DSZKH%26dataid%3D31%26fileid%3D1%26regdt%3D20190417180523&url=http%3A%2F%2Fcfile299.uf.daum.net%2Fattach%2F993EAA335CB6EC4B2960C9'%29)

#### 2. java.util.Collections.sort\(\)

   Collection적인 클래스의 정렬에 사용

   Ex\) ArrayList, LinkedList 등 

### 개발자가 만든 객체자료형의 sort시 Collections.sort\(\)를 사용하고 싶다면

```java
접 class  클명  implements Comparable<클명>{
    @Override
    public int compareTo(클명 o) {   이 메소드를 구현 해 놓아야 한다.
    return  수치멤버 - o.수치멤버 ; 또는 
    return  객체자료형멤버.compareTo(o.객체자료형멤버) ;
   이런식으로 구현해주면 된다.
 }
}   
```

###    Collections.sort\( 클명의 리스트 주소    \)  ==&gt; compareTo\(\)가 자동으로 호출됨

* [적용 예\#1 - 성적처리](http://cafe.daum.net/OakHouse/SZL4/470) 
* [적용 예\#2 ](http://cafe.daum.net/OakHouse/JafA/25)

