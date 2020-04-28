---
description: 객체의 복제
---

# System.arraycopy\(\) ,Object.clone\(\)

## 개념 정리 및 적용  ****

### \*\*\*\*[**2020.04.28 국여주**](http://cafe.daum.net/OakHouse/Sdlx/20)\*\*\*\*

### [ **2020.04.28 박주영**](http://cafe.daum.net/OakHouse/Sdlx/19)\*\*\*\*

 [**2020.04.28 김연수**](http://cafe.daum.net/OakHouse/Sdlx/18)\*\*\*\*

 [**2020.04.28 과제-김하현** ](http://cafe.daum.net/OakHouse/Sdm0/17)\*\*\*\*

### [clone\(\)](http://cafe.daum.net/OakHouse/NZT3/134)

다음 ArrayEx의 결과는 ? 

```
class ArrayEx{
  public static void main(String[] arg){
  char[] abc = {'A', 'B', 'C', 'D'};
  char[] number = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9'};
  System.out.println(new String(abc));
  System.out.println(new String(number));
 
  char[] result = new char[abc.length+number.length];
  System.arraycopy(abc, 0, result, 0, abc.length);
  System.arraycopy(number, 0, result, abc.length, number.length);
  System.out.println(new String(result));
 
  System.arraycopy(abc, 0, number, 0, abc.length);
  System.out.println(new String(number));
 
  System.arraycopy(abc, 0, number, 6, 3);
  System.out.println(new String(number));
  }
}
```



