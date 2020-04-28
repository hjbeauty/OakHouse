# Sort , Search

### 자바에서 제공하는 lib를 사용하지 않고 만든 정렬 예제

> [ 순차정렬, 버블정렬 ..  이진 검색 \#1](http://cafe.daum.net/OakHouse/SZL4/261)
>
> [Bubble Sort , Sequential Sort, 이진검색 \#2](http://cafe.daum.net/OakHouse/SZL4/259)

> [merge sort , quick sort , insert sort , time sort 설명 및  간단예제](http://cafe.daum.net/OakHouse/SZL4/296)
>
>
>
> >

#### merge sort

* merge sort는 O\(n log n\) 비교 기반 정렬 알고리즘이다. 분할 정복 알고리즘의 하나이다. 존 폰 노이만이 1945년에 개발했다.
  1. 리스트의 길이가 0 또는 1이면 이미 정렬된 것으로 본다. 그렇지 않은 경우에는
  2. 정렬되지 않은 리스트를 절반으로 잘라 비슷한 크기의 두 부분 리스트로 나눈다.
  3. 각 부분 리스트를 재귀적으로 합병 정렬을 이용해 정렬한 두 부분 리스트를 다시 하나의 정렬된 리스트로 합병한다.

top-down 방식 코드

```text

// Array A[] has the items to sort; array B[] is a work array.
TopDownMergeSort(A[], B[], n)
{
    CopyArray(A, 0, n, B);           // duplicate array A[] into B[]
    TopDownSplitMerge(B, 0, n, A);   // sort data from B[] into A[]
}

// Sort the given run of array A[] using array B[] as a source.
// iBegin is inclusive; iEnd is exclusive (A[iEnd] is not in the set).
TopDownSplitMerge(B[], iBegin, iEnd, A[])
{
    if(iEnd - iBegin < 2)                       // if run size == 1
        return;                                 //   consider it sorted
    // split the run longer than 1 item into halves
    iMiddle = (iEnd + iBegin) / 2;              // iMiddle = mid point
    // recursively sort both runs from array A[] into B[]
    TopDownSplitMerge(A, iBegin,  iMiddle, B);  // sort the left  run
    TopDownSplitMerge(A, iMiddle,    iEnd, B);  // sort the right run
    // merge the resulting runs from array B[] into A[]
    TopDownMerge(B, iBegin, iMiddle, iEnd, A);
}

//  Left source half is A[ iBegin:iMiddle-1].
// Right source half is A[iMiddle:iEnd-1   ].
// Result is            B[ iBegin:iEnd-1   ].
TopDownMerge(A[], iBegin, iMiddle, iEnd, B[])
{
    i = iBegin, j = iMiddle;

    // While there are elements in the left or right runs...
    for (k = iBegin; k < iEnd; k++) {
        // If left run head exists and is <= existing right run head.
        if (i < iMiddle && (j >= iEnd || A[i] <= A[j])) {
            B[k] = A[i];
            i = i + 1;
        } else {
            B[k] = A[j];
            j = j + 1;
        }
    }
}

CopyArray(A[], iBegin, iEnd, B[])
{
    for(k = iBegin; k < iEnd; k++)
        B[k] = A[k];
}

```

#### quick sort

* Quicksort는 다른 원소와의 비교만으로 정렬을 수행하는 비교 정렬의 일종이다. 퀵 정렬의 복잡도는 최악의 경우 O\(n^2\)이고, 평균적으로 O\(n log n\)이다. 퀵 정렬은 분할 정복\(divide and conquer\) 방법을 통해 리스트를 정렬한다.
  1. 리스트 가운데서 하나의 원소를 고른다. 이렇게 고른 원소를 피벗이라고 한다.
  2. 리스트 가운데서 하나의 원소를 고른다. 이렇게 고른 원소를 피벗이라고 한다.
  3. 분할된 두 개의 작은 리스트에 대해 재귀\(Recursion\)적으로 이 과정을 반복한다. 재귀는 리스트의 크기가 0이나 1이 될 때까지 반복된다.

```text
public void quickSort(int[] arr, int left, int right) {
    int i, j, pivot, tmp;
    if (left < right) {
        i = left;   j = right;
        pivot = arr[(left+right)/2];
        //분할 과정
        while (i < j) {
            while (arr[j] > pivot) j--;
            // 이 부분에서 arr[j-1]에 접근해서 익셉션 발생가능함.
            while (i < j && arr[i] <= pivot) i++;

            tmp = arr[i];
            arr[i] = arr[j];
            arr[j] = tmp;
        }
        //정렬 과정
        quickSort(arr, left, i - 1);
        quickSort(arr, i + 1, right);
    }
}
```

#### insert sort

* 삽입 정렬\(揷入整列, insertion sort\)은 자료 배열의 모든 요소를 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교하여, 자신의 위치를 찾아 삽입함으로써 정렬을 완성하는 알고리즘이다.
* k번째 반복 후의 결과 배열은, 앞쪽 k + 1 항목이 정렬된 상태이다. 각 반복에서 정렬되지 않은 나머지 부분 중 첫 번째 항목은 제거되어 정확한 위치에 삽입된다.
* 배열이 길어질수록 효율이 떨어지지만, 구현이 간단하다는 장점이 있다. 선택 정렬이나 거품 정렬에 비교하여 빠르며, 안정 정렬이고 in-place 알고리즘이다.

```text
void insertionSort(int[] arr)
{

   for(int index = 1 ; index < arr.length ; index++){

      int temp = arr[index];
      int aux = index - 1;

      while( (aux >= 0) && ( arr[aux] > temp ) ) {

         arr[aux+1] = arr[aux];
         aux--;
      }
      arr[aux + 1] = temp;
   }
}
```

#### tim sort

* Merge sort 와 Insert sort 를 혼용한 것으로, 현실 세계에 있는 데이터가 랜덤하게 흩어진 형태 보다 대략 정렬된 상태로 있다는 것에 기반하여 디자인된 알고리즘이다.
* Merge sort의 최악 시간 복잡도와, Insert Sort의 최고 시간 복잡도를 갖고 가게 되므로, 정렬의 시간 복잡도를 O\(n\) ~ O\(n log n\) 사이를 보장한다는 점이다.
* 자바에서 JDK7 이후부터 객체들의 기본 정렬 알고리즘으로 적용되었다.
  1. 데이터의 처음부터 검색하여, 연속성이 있는 부분들을 run이라는 단위로 분류
  2. 연속성이 전혀 없는 random한 데이터들은 minrun이라는 단위로 분류되고, insert sort를 수행해 run으로 만듬
  3. stack에 run을 쌓고, 위쪽 run들이 더 짧은 경우 위쪽 run들에 merge sort를 수행하여 위로갈수록 큰 run으로 만들기를 반복한다

##  Super Powers

Becoming a super hero is a fairly straight forward process:

```
$ give me super-powers
```

{% hint style="info" %}
 Super-powers are granted randomly so please submit an issue if you're not happy with yours.
{% endhint %}

Once you're strong enough, save the world:

{% code title="hello.sh" %}
```bash
# Ain't no code for that yet, sorry
echo 'You got to trust me on this, I saved the world'
```
{% endcode %}



