# no Collections.sort\(\)

## 자바에서 제공하는 lib를 사용하지 않고 만든 정렬 예제

> [ 순차정렬, 버블정렬 ..  이진 검색 \#1](http://cafe.daum.net/OakHouse/SZL4/261)
>
> [Bubble Sort , Sequential Sort, 이진검색 \#2](http://cafe.daum.net/OakHouse/SZL4/259)
>
>  [InsertionSort ](http://cafe.daum.net/OakHouse/MzQX/214)
>
> [SelectionSort](http://cafe.daum.net/OakHouse/MzQX/209) 
>
> [버블 소트 rank\(\) 만들어서 사용해보기](http://cafe.daum.net/OakHouse/JafA/9)

> [merge sort , quick sort , insert sort , time sort 설명 및  간단예제](http://cafe.daum.net/OakHouse/SZL4/296)
>
> [Merge sort 쪼개보기 ](http://cafe.daum.net/OakHouse/SZL4/294)

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



## \*\*\*\*[**자료구조요약**](http://cafe.daum.net/OakHouse/NZT3/28)\*\*\*\*

[과제및질문30기](http://cafe.daum.net/_c21_/bbs_list?grpid=zaqT&fldid=NZT3&listnum=)**과제003\[09.10.16\]\_자료구조요약\_유준영**![](http://img1.daumcdn.net/thumb/C30x30/?fname=http://i1.daumcdn.net/cafeimg/img_profile/profile_cob.png)[유준영](javascript:)추천 0조회 10709.10.16 11:49댓글 [0](http://cafe.daum.net/_c21_/bbs_nsread?grpid=zaqT&fldid=NZT3&contentval=0000Szzzzzzzzzzzzzzzzzzzzzzzzz&datanum=28&searchlist_uri=%2F_c21_%2Fcafesearch&search_ctx=LrpNuZSucOsx.YncUoV2ej_tRpHqkOL1hFNwnK7pMwx2pUU9oYvq-CADq-lzJK_p_TYbLZznvSbg3qy8mowcMNh423a2OuJx6S98.wUXI9Eg29HccobGx.ln6dXQeDhEud6My9x_UN4NWPYs2bJFXPgh1odP.EP8KdgYsyACDmNY-Nbah8z14WrgaW8lqJaP.T.DnJZIPDs7Gp5TXzYBB9l8RJswHGQdvRKBOTdyxqiwtmyIRQasPWyz1HVvDMRzdZpDdR3wpWLcEwrqw.QRJfGQFutUtE8qjzCthFB-NstPDypNNygg9A_16ONB3mtiOUadOBnfBo_4zflMBsegsjUsbvVaCr4f#comment-btn)북마크공유하기기능 더보기

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>1&#xC7A5;.&#xC790;&#xB8CC;&#xAD6C;&#xC870; &#xAC1C;&#xC694;
          <br />1.&#xC790;&#xB8CC;&#xC758; &#xC815;&#xC758;
          <br />&#xC790;&#xB8CC;(data) : &#xC5B4;&#xB5A4; &#xC0AC;&#xC2E4;&#xC774;&#xB098;
          &#xAC1C;&#xB150;&#xC758; &#xAC12;&#xB4E4; &#xB610;&#xB294; &#xAC12;&#xB4E4;&#xC758;
          &#xC9D1;&#xD569;
          <br />&#xC790;&#xB8CC;&#xC758; &#xAD6C;&#xC131;&#xB2E8;&#xC704; :&#xD544;&#xB4DC;,&#xB808;&#xCF54;&#xB4DC;,&#xD30C;&#xC77C;(&#xB808;&#xCF54;&#xB4DC;&#xC758;
          &#xBAA8;&#xC784;).
          <br />2.&#xBB38;&#xC81C; &#xD480;&#xC774;&#xC758; &#xB2E8;&#xACC4;
          <br />&#xC790;&#xB8CC;&#xAD6C;&#xC870;: &#xC790;&#xB8CC;&#xB294; &#xC790;&#xB8CC;
          &#xC6D0;&#xC18C;&#xC758; &#xC9D1;&#xD569;&#xC73C;&#xB85C; &#xAD6C;&#xC131;&#xB418;&#xC5B4;
          &#xC788;&#xC73C;&#xBA70;, &#xC790;&#xB8CC; &#xC6D0;&#xC18C;&#xAC04;&#xC5D0;&#xB294;
          &#xB17C;&#xB9AC;&#xC801;&#xC778; &#xAD00;&#xACC4;&#xAC00; &#xC788;&#xB2E4;.
          &#xC790;&#xB8CC; &#xAD6C;&#xC870;&#xB97C; &#xC5B4;&#xB5A4; &#xC790;&#xB8CC;
          &#xAD6C;&#xC870;&#xB85C; &#xAD6C;&#xC131;&#xD574;&#xC57C; &#xD560;&#xAE4C;&#xB97C;
          &#xC120;&#xD0DD;
          <br />&#xC5F0;&#xC0B0;&#xC791;&#xC5C5;: &#xC790;&#xB8CC;&#xAD6C;&#xC870;&#xB97C;
          &#xB9CC;&#xB4E4;&#xAC70;&#xB098; &#xC5C6;&#xC560;&#xB294; &#xC791;&#xC5C5;,
          &#xC790;&#xB8CC;&#xAD6C;&#xC870;&#xC5D0; &#xC0C8;&#xB85C;&#xC6B4; &#xC6D0;&#xC18C;&#xB97C;
          &#xC0BD;&#xC785;/&#xC0AD;&#xC81C;/&#xAC31;&#xC2E0;
          <br />&#xC800;&#xC7A5;&#xBC29;&#xBC95;: &#xC790;&#xB8CC;&#xAD6C;&#xC870;&#xB97C;
          &#xAE30;&#xC5B5;&#xC7A5;&#xC18C; &#xB0B4;&#xC5D0;&#xC11C; &#xBB3C;&#xB9AC;&#xC801;&#xC73C;&#xB85C;
          &#xD45C;&#xD604;&#xD55C; &#xAC83;&#xC744; &#xC800;&#xC7A5;&#xAD6C;&#xC870;&#xB77C;&#xACE0;
          &#xD558;&#xACE0;, &#xD55C; &#xC790;&#xB8CC;&#xAD6C;&#xC870;&#xC5D0; &#xB300;&#xD55C;
          &#xC800;&#xC7A5; &#xAD6C;&#xC870;&#xB294; &#xC5EC;&#xB7EC; &#xAC00;&#xC9C0;&#xC77C;&#xC218;
          &#xC788;&#xB2E4;
          <br />&#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xC5B8;&#xC5B4;: &#xD504;&#xB85C;&#xADF8;&#xB7A8;
          &#xC5B8;&#xC5B4;&#xC5D0; &#xB530;&#xB77C; &#xC120;&#xD0DD;&#xB41C; &#xC790;&#xB8CC;
          &#xAD6C;&#xC870;&#xAC00; &#xC81C;&#xACF5; &#xB418;&#xC9C0; &#xC54A;&#xC744;
          &#xC218;&#xAC00; &#xC788;&#xC74C;
          <br />3.&#xC790;&#xB8CC;&#xAD6C;&#xC870;-&#xCEF4;&#xD4E8;&#xD130;&#xAC00; &#xCD08;&#xAE30;&#xC5D0;&#xB294;
          &#xC8FC;&#xB85C; &#xC218;&#xCE58;&#xC801;&#xC778; &#xBB38;&#xC81C;&#xB97C;
          &#xD480;&#xAE30; &#xC704;&#xD574; &#xC0AC;&#xC6A9;&#xB418;&#xC5C8;&#xC73C;&#xB098;,
          &#xC810;&#xCC28; &#xBE44;&#xC218;&#xCE58;&#xC801;&#xC778; &#xBB38;&#xC81C;&#xB97C;
          &#xD574;&#xACB0;&#xD558;&#xAE30; &#xC704;&#xD574; &#xB354; &#xB9CE;&#xC774;
          &#xC0AC;&#xC6A9;&#xD55C;&#xB2E4;.
          <br />&#xC218;&#xCE58;&#xC801;&#xC778; &#xBB38;&#xC81C; &#xD574;&#xACB0; : &#xC815;&#xC218;,
          &#xC2E4;&#xC218;, &#xBC30;&#xC5F4;
          <br />&#xBE44;&#xC218;&#xCE58;&#xC801;&#xC778; &#xBB38;&#xC81C; &#xD574;&#xACB0;
          : &#xAD6C;&#xC870;&#xCCB4;, &#xD3EC;&#xC778;&#xD130;, &#xB4F1;
          <br />4.&#xC54C;&#xACE0;&#xB9AC;&#xC998;
          <br />4.1.&#xC54C;&#xACE0;&#xB9AC;&#xC998; &#xC815;&#xC758;
          <br />&#xC54C;&#xACE0;&#xB9AC;&#xC998;-&#xD2B9;&#xC815;&#xD55C; &#xBB38;&#xC81C;&#xB97C;
          &#xD480;&#xAE30; &#xC704;&#xD574; &#xC815;&#xD574;&#xC9C4; &#xC77C;&#xB828;&#xC758;
          &#xBA85;&#xB839; ,&#xCEF4;&#xD4E8;&#xD130;&#xC5D0; &#xC758;&#xD574; &#xC218;&#xD589;
          &#xB420;&#xC218; &#xC788;&#xACE0;, &#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xC791;&#xC131;&#xC774;
          &#xAC00;&#xB2A5;&#xD558;&#xC5EC;&#xC57C;&#xD568;.
          <br />&#xD504;&#xB85C;&#xADF8;&#xB7A8;-&#xCD94;&#xC0C1;&#xC801;&#xC778; &#xD615;&#xD0DC;&#xB85C;
          &#xD45C;&#xD604;&#xD55C; &#xC54C;&#xACE0;&#xB9AC;&#xC998;&#xC744; &#xCEF4;&#xD4E8;&#xD130;&#xAC00;
          &#xC218;&#xD589; &#xD560;&#xC218; &#xC787;&#xB3C4;&#xB85D; &#xAD6C;&#xCCB4;&#xC801;&#xC778;
          &#xD615;&#xD0DC;&#xB85C; &#xD45C;&#xD604;&#xD55C; &#xAC83;
          <br />&#xC54C;&#xACE0;&#xB9AC;&#xC998;&#xC758; &#xC870;&#xAC74;-&#xBA85;&#xD655;&#xC131;,&#xC720;&#xD55C;&#xC131;,&#xC720;&#xD6A8;&#xC131;,&#xC815;&#xD655;&#xC131;
          <br
          />4.2.&#xC54C;&#xACE0;&#xB9AC;&#xC998;&#xACFC; &#xC790;&#xB8CC;&#xAD6C;&#xC870;&#xC758;
          &#xAD00;&#xACC4;-&#xC8FC;&#xC5B4;&#xC9C4; &#xBB38;&#xC81C;&#xC5D0;&#xC11C;
          &#xC218;&#xD589;&#xB420; &#xC5F0;&#xC0B0;&#xC791;&#xC5C5;&#xC758; &#xC720;&#xD615;&#xC744;
          &#xACE0;&#xCC30;&#xD558;&#xACE0; &#xC774;&#xB7EC;&#xD55C; &#xC791;&#xC5C5;&#xB4E4;&#xC774;
          &#xD6A8;&#xACFC;&#xC801;&#xC73C;&#xB85C; &#xC218;&#xD589;&#xB420; &#xC218;
          &#xC788;&#xB3C4;&#xB85D; &#xC790;&#xB8CC;&#xB97C; &#xD45C;&#xD604;
          <br />-&gt;&#xC790;&#xB8CC;&#xC5D0; &#xB300;&#xD55C; &#xAE30;&#xBCF8; &#xC5F0;&#xC0B0;&#xC73C;&#xB85C;
          &#xCD08;&#xAE30;&#xD654;,&#xC18C;&#xBA78;,&#xC870;&#xD68C;,&#xC21C;&#xD68C;,&#xC0BD;&#xC785;,&#xC0AD;&#xC81C;,&#xD0D0;&#xC0C9;,&#xC815;&#xB82C;,&#xD569;&#xBCD1;&#xC774;
          &#xC788;&#xB2E4;.
          <br />4.3.&#xC54C;&#xACE0;&#xB9AC;&#xC998;&#xC758; &#xAE30;&#xC220;&#xBC29;&#xBC95;-&#xC790;&#xC5F0;&#xC5B8;&#xC5B4;
          &#xBC29;&#xBC95;,&#xD750;&#xB984;&#xB3C4; &#xBC29;&#xBC95;,&#xC54C;&#xACE0;&#xB9AC;&#xC998;
          &#xC5B8;&#xC5B4; &#xBC29;&#xBC95;,&#xD2B9;&#xC131; &#xD504;&#xB85C;&#xADF8;&#xB7A8;
          &#xC5B8;&#xC5B4; &#xBC29;&#xBC95;
          <br />5.&#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC758; &#xAE30;&#xBCF8; &#xC81C;&#xC5B4;
          &#xAD6C;&#xC870;
          <br />5.1.&#xC81C;&#xC5B4;&#xAD6C;&#xC870;&#xC758; &#xAE30;&#xBCF8; 4&#xAC00;&#xC9C0;-&#xC21C;&#xCC28;&#xAD6C;&#xC870;,&#xC120;&#xD0DD;&#xAD6C;&#xC870;,&#xBC18;&#xBCF5;&#xAD6C;&#xC870;,&#xAC74;&#xB108;&#xB700;
          &#xAD6C;&#xC870; (&#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC758; &#xC81C;&#xC5B4;&#xAD6C;&#xC870;&#xB294;
          &#xC785;&#xAD6C;&#xC640; &#xCD9C;&#xAD6C;&#xAC00; &#xD558;&#xB098;&#xC5EC;&#xC57C;
          &#xD568;)
          <br />5.2.&#xC120;&#xD0DD;&#xAD6C;&#xC870;-if&#xAD6C;&#xC870;,switch&#xAD6C;&#xC870;
          <br
          />5.3.&#xBC18;&#xBCF5;&#xAD6C;&#xC870;-while&#xAD6C;&#xC870;,for&#xAD6C;&#xC870;,do-while&#xAD6C;&#xC870;
          <br
          />-&gt;for&#xAC00; &#xC138; &#xAD6C;&#xC870;&#xC911;&#xC5D0; &#xAC00;&#xC7A5;
          &#xBD84;&#xBA85;&#xD55C; &#xAD6C;&#xC870;&#xC774;&#xBBC0;&#xB85C; &#xAC00;&#xC7A5;
          &#xBA3C;&#xC800; &#xACE0;&#xB824;&#xD558;&#xACE0;,&#xBC18;&#xBCF5; &#xC2E4;&#xD589;&#xD558;&#xAE30;&#xC804;&#xC5D0;
          &#xBC18;&#xBCF5; &#xC870;&#xAC74;&#xC744; &#xAC80;&#xC0AC;&#xD574;&#xC57C;&#xD55C;&#xB2E4;&#xBA74;
          while &#xAD6C;&#xC870;&#xAC00; &#xC801;&#xC808;&#xD558;&#xB2E4;.
          <br />5.4.&#xAC74;&#xB108;&#xB700;&#xAD6C;&#xC870;-break&#xBB38;,continue&#xBB38;,goto&#xBB38;(&#xAC70;&#xC758;&#xC0AC;&#xC6A9;&#xD558;&#xC9C0;
          &#xC54A;&#xC74C;)
          <br />6.&#xC21C;&#xD658;&#xAD6C;&#xC870;
          <br />6.1.&#xC21C;&#xD658;&#xD568;&#xC218;-&#xC5B4;&#xB5A4;&#xD568;&#xC218;&#xAC00;
          &#xC790;&#xAE30;&#xC790;&#xC2E0;&#xC744; &#xC9C1;&#xC811; &#xD638;&#xCD9C;
          &#xD560; &#xB54C;&#xC758; &#xD568;&#xC218;
          <br />-&gt;&#xC21C;&#xD658;&#xD568;&#xC218;&#xAC00; &#xBB34;&#xD55C;&#xC815;
          &#xC218;&#xD589;&#xB418;&#xC9C0; &#xC54A;&#xAE30; &#xC704;&#xD574;&#xC11C;&#xB294;
          &#xC790;&#xC2E0;&#xC744; &#xD638;&#xCD9C;&#xD558;&#xC9C0; &#xC54A;&#xACE0;
          &#xD568;&#xC218;&#xC758; &#xAC12;&#xC774; &#xC815;&#xC758;&#xB418;&#xB294;
          &#xACBD;&#xC6B0;&#xAC00; &#xC788;&#xC5B4;&#xC57C; &#xD558;&#xACE0;, &#xC790;&#xC2E0;&#xC744;
          &#xD638;&#xCD9C;&#xD560; &#xB54C; &#xC804;&#xB2EC;&#xD558;&#xB294; &#xC778;&#xC790;&#xB294;
          &#xD604;&#xC7AC; &#xC8FC;&#xC5B4;&#xC9C4; &#xC778;&#xC790;&#xBCF4;&#xB2E4;
          &#xC791;&#xC544;&#xD558;&#xBA70; &#xD638;&#xCD9C;&#xD560; &#xB54C;&#xB9C8;&#xB2E4;
          base case&#xC5D0; &#xAC00;&#xAE4C;&#xC6CC;&#xC838;&#xC57C;&#xD55C;&#xB2E4;.
          <br
          />-&gt;&#xD53C;&#xBCF4;&#xB098;&#xCE58; &#xC218;&#xC5F4;-Fibonacci &#xD568;&#xC218;&#xB294;
          &#xC798; &#xC815;&#xC758;&#xB41C; &#xD568;&#xC218;&#xB85C; &#xC774;&#xC720;&#xB294;
          n=1, n=2 &#xC77C;&#xB54C; &#xC790;&#xC2E0;&#xC744; &#xD638;&#xCD9C;&#xD558;&#xC9C0;
          &#xC54A;&#xACE0; &#xD568;&#xC218; &#xAC12;&#xC774; &#xC8FC;&#xC5B4;&#xC9C0;&#xBA70;,
          F(n)&#xC740; n &#xBCF4;&#xB2E4; &#xC801;&#xC744; &#xAC12;&#xC73C;&#xB85C;
          &#xC815;&#xC758;&#xB418;&#xACE0; , &#xD638;&#xCD9C;&#xB420; &#xB54C;&#xB9C8;&#xB2E4;
          n=1&#xC5D0; &#xAC00;&#xAE4C;&#xC6CC;&#xC9C0;&#xAE30; &#xB54C;&#xBB38;&#xC774;&#xB2E4;.
          <br
          />
          <br />2&#xC7A5;.&#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xC791;&#xC131;
          <br />1.&#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC791;&#xC131; &#xAE30;&#xBC95;
          <br
          />1.1.&#xAD6C;&#xC870;&#xD654; &#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xC791;&#xC131;-goto
          &#xBB38; &#xC5C6;&#xB294; &#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xC791;&#xC131;,
          &#xBAA8;&#xB4C8;&#xD654; &#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xC791;&#xC131;,&#xD558;&#xD5A5;&#xC2DD;
          &#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xC791;&#xC131;
          <br />1.2.&#xAC1D;&#xCCB4;&#xC9C0;&#xD5A5; &#xD504;&#xB85C;&#xADF8;&#xB7A8;
          &#xC791;&#xC131;
          <br />-&#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xC791;&#xC131;&#xC758; &#xC0DD;&#xC0B0;&#xC131;&#xC744;
          &#xD5A5;&#xC0C1;&#xC2DC;&#xD0A4;&#xAE30; &#xC704;&#xD55C; &#xAE30;&#xBC95;&#xC784;
          <br
          />-&#xAD6C;&#xC870;&#xD654; &#xAE30;&#xBC95;&#xC5D0;&#xC11C;&#xB294; &#xBAA8;&#xB4C8;&#xC774;
          &#xD568;&#xC218; &#xC911;&#xC2EC;&#xC774;&#xACE0;, &#xC790;&#xB8CC;&#xB294;
          &#xD568;&#xC218;&#xC5D0;&#xC11C; &#xC0AC;&#xC6A9;&#xB41C;&#xB2E4;&#xB294;
          &#xBD80;&#xCC28;&#xC801;&#xC778; &#xC5ED;&#xD65C;&#xC784;
          <br />-&#xAC1D;&#xCCB4;&#xC9C0;&#xD5A5; &#xAE30;&#xBC95;&#xC5D0;&#xC11C; &#xBAA8;&#xB4C8;&#xC740;
          &#xC790;&#xB8CC; &#xC911;&#xC2EC;&#xC774;&#xACE0; &#xD568;&#xC218;&#xB294;
          &#xC774; &#xC790;&#xB8CC;&#xB97C; &#xC0AC;&#xC6A9;&#xD55C;&#xB2E4;&#xB294;
          &#xBD80;&#xCC28;&#xC801;&#xC778; &#xC5ED;&#xD65C;&#xC784;
          <br />-&#xC790;&#xB8CC;&#xB97C; &#xBAA8;&#xB4C8; &#xC911;&#xC2EC;&#xC73C;&#xB85C;
          &#xD558;&#xACE0;, &#xC774;&#xC790;&#xB8CC;&#xC640; &#xADF8; &#xC678; &#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xAC04;&#xC758;
          &#xC0C1;&#xD638; &#xC791;&#xC6A9;&#xC744; &#xCC98;&#xB9AC;&#xD574;&#xC904;
          &#xD568;&#xC218;&#xB97C; &#xC774; &#xC790;&#xB8CC;&#xC5D0; &#xBD99;&#xC5EC;&#xC11C;
          &#xD55C; &#xAD6C;&#xC870;&#xB85C; &#xB9CC;&#xB4E0; &#xAC83;&#xC774; &#xD074;&#xB798;&#xC2A4;&#xC774;&#xB2E4;.
          <br
          />2.&#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC758; &#xC678;&#xD615;-&#xC77D;&#xAE30;&#xC27D;&#xACE0;,
          &#xACC4;&#xC0B0;&#xC2DC;&#xAC04; &#xC9E7;&#xACE0;, &#xD504;&#xB85C;&#xADF8;&#xB7A8;
          &#xC678;&#xD615;&#xC740; &#xC77C;&#xAD00;&#xC131;&#xC788;&#xAC8C; &#xC720;&#xC9C0;&#xD55C;&#xB2E4;.
          <br
          />3.&#xD504;&#xB85C;&#xADF8;&#xB7A8;
          <br />3.1.&#xAD6C;&#xBB38;&#xC624;&#xB958; (syntax error) : &#xC791;&#xC131;&#xB41C;
          &#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC774; &#xCEF4;&#xD4E8;&#xD130; &#xC5B8;&#xC5B4;&#xC758;
          &#xADDC;&#xCE59;&#xC5D0; &#xC5B4;&#xAE0B;&#xB0A0; &#xB54C; &#xB098;&#xD0C0;&#xB098;&#xB294;
          &#xC624;&#xB958;
          <br />3.2.&#xB17C;&#xB9AC; &#xC624;&#xB958; (logic error) : &#xC131;&#xACF5;&#xC801;&#xC73C;&#xB85C;
          &#xCEF4;&#xD30C;&#xC77C;&#xB41C; &#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC774;
          &#xC2E4;&#xC2DC;&#xB420; &#xB54C; &#xB098;&#xD0C0;&#xB098;&#xB294; &#xC624;&#xB958;</p>
        <p>3&#xC7A5;.&#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC758; &#xD6A8;&#xC728;&#xC131;(&#xCEF4;&#xD30C;&#xC77C;&#xBC29;&#xC2DD;)
          <br
          />1.&#xAE30;&#xBCF8;&#xAC1C;&#xB150;-&#xD6A8;&#xC728;&#xC131;&#xBA74;&#xC5D0;&#xC11C;
          &#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC758; &#xACC4;&#xC0B0;&#xC18D;&#xB3C4;&#xAC00;
          &#xD5A5;&#xC0C1;&#xB418;&#xB098; &#xC2E4;&#xC2DC;&#xAC04; &#xCC98;&#xB9AC;&#xC5D0;&#xC11C;
          &#xBB38;&#xC81C;
          <br />2.&#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC758; &#xACC4;&#xC0B0;&#xC2DC;&#xAC04;
          &#xCE21;&#xC815;
          <br />2.1.&#xCE21;&#xC815;&#xB0B4;&#xC6A9;
          <br />-&#xACC4;&#xC0B0; &#xC2DC;&#xAC04;&#xC740; &#xC790;&#xB8CC;&#xD615;&#xC5D0;
          &#xB530;&#xB77C; &#xC5F0;&#xC0B0; &#xC2DC;&#xAC04;&#xC774; &#xB2E4;&#xB984;
          ( &#xC815;&#xC218;&#xD615; &lt; &#xBD80;&#xB3D9;&#xC18C;&#xC218;&#xC810;&#xD615;)
          <br
          />-&#xAC19;&#xC740; &#xC790;&#xB8CC;&#xD615;&#xB3C4; &#xC5F0;&#xC0B0; &#xC885;&#xB958;&#xC5D0;
          &#xB530;&#xB77C; &#xC5F0;&#xC0B0; &#xC2DC;&#xAC04;&#xC774; &#xB2E4;&#xB984;(+,
          - &lt; * /)
          <br />-&#xC8FC;&#xC18C; &#xC5F0;&#xC0B0;&#xC790;&#xC640; &#xAD6C;&#xC870;&#xCCB4;
          &#xBA64;&#xBC84; &#xC5F0;&#xC0B0;&#xC740; &#xC2DC;&#xAC04;&#xC774; &#xC18C;&#xC694;
          &#xB418;&#xC9C0; &#xC54A;&#xB294;&#xB2E4;.
          <br />-&#xCEF4;&#xD4E8;&#xD130;&#xC5D0; &#xB530;&#xB77C; &#xC5F0;&#xC0B0; &#xC2DC;&#xAC04;&#xC774;
          &#xB2E4;&#xB974;&#xB2E4;.
          <br />-register &#xC0AC;&#xC6A9;&#xD558;&#xBA74; &#xC18D;&#xB3C4;&#xAC00; &#xD5A5;&#xC0C1;&#xB41C;&#xB2E4;.
          <br
          />-2&#xCC28;&#xC6D0; &#xBC30;&#xC5F4; &#xBCF4;&#xB2E4;&#xB3C4; 1&#xCC28;&#xC6D0;
          &#xBC30;&#xC5F4;&#xC744; &#xC0AC;&#xC6A9;&#xD558;&#xAC70;&#xB098; &#xD3EC;&#xC778;&#xD130;
          &#xC0AC;&#xC6A9;&#xC740; &#xACC4;&#xC0B0; &#xC2DC;&#xAC04;&#xC744; &#xB2E8;&#xCD95;&#xC2DC;&#xD0A8;&#xB2E4;.
          <br
          />2.2.profiler&#xC0AC;&#xC6A9;- profiler&#xB294; &#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC758;
          &#xC2E4;&#xD589;&#xC2DC;&#xAC04;&#xC744; &#xBD84;&#xC11D;&#xD574;&#xC8FC;&#xB294;
          &#xB3C4;&#xAD6C;
          <br />3.&#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC758; &#xD6A8;&#xC728;&#xD654; &#xBC29;&#xBC95;-
          &#xBE60;&#xB978; &#xAE30;&#xACC4;&#xB97C; &#xC0AC;&#xC6A9;&#xD558;&#xAC70;&#xB098;
          &#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC758; &#xCD5C;&#xC801;&#xD654;&#xB97C;
          &#xC2DC;&#xD0A8;&#xB2E4;.</p>
        <p>4&#xC7A5;.&#xC54C;&#xACE0;&#xB9AC;&#xC998;&#xC758; &#xBD84;&#xC11D;
          <br
          />1.&#xC54C;&#xACE0;&#xB9AC;&#xC998; &#xBD84;&#xC11D;&#xC758; &#xD544;&#xC694;&#xC131;
          <br
          />1.1.&#xC54C;&#xACE0;&#xB9AC;&#xC998; &#xBD84;&#xC11D;&#xC758; &#xAE30;&#xC900;-&#xC18C;&#xC694;&#xACC4;&#xC0B0;
          &#xC2DC;&#xAC04;,&#xAE30;&#xC5B5;&#xC7A5;&#xC18C; &#xC0AC;&#xC6A9;&#xB7C9;,&#xC815;&#xD655;&#xC131;,&#xAC04;&#xACB0;&#xC131;
          <br
          />1.2.&#xC18C;&#xC694;&#xACC4;&#xC0B0; &#xC2DC;&#xAC04;&#xACFC; &#xAE30;&#xC5B5;&#xC7A5;&#xC18C;
          &#xC0AC;&#xC6A9;&#xB7C9;&#xC774; &#xC911;&#xC694;&#xD55C; &#xC774;&#xC720;
          <br
          />-&#xC54C;&#xACE0;&#xB9AC;&#xC998;&#xC774; &#xD544;&#xC694;&#xB85C;&#xD558;&#xB294;
          &#xCEF4;&#xD4E8;&#xD130;&#xC758; &#xAE30;&#xC5B5;&#xC6A9;&#xB7C9;&#xACFC;
          &#xACC4;&#xC0B0;&#xC2DC;&#xAC04;&#xC758; &#xCD94;&#xC815;&#xCE58;&#xB098;
          &#xCD5C;&#xB300;&#xCE58;&#xB97C; &#xC54C; &#xC218; &#xC788;&#xC74C;.
          <br
          />2.&#xACC4;&#xC0B0;&#xB7C9;
          <br />2.1.&#xACC4;&#xC0B0;&#xB7C9;&#xC758; &#xCE21;&#xC815; &#xBC29;&#xBC95;
          <br
          />-&#xCEF4;&#xD4E8;&#xD130; &#xAE30;&#xC885;&#xC774;&#xB098;,&#xD504;&#xB85C;&#xADF8;&#xB7A8;
          &#xC5B8;&#xC5B4;&#xC640;, &#xAE30;&#xD0C0; &#xADC0;&#xCC2E;&#xC740; &#xC791;&#xC5C5;&#xB54C;&#xBB38;&#xC5D0;
          &#xCEF4;&#xD4E8;&#xD130; &#xC2E4;&#xD589;&#xC2DC;&#xAC04;&#xC740; &#xACC4;&#xC0B0;&#xB7C9;&#xC73C;&#xB85C;
          &#xC4F0;&#xC9C0; &#xC54A;&#xB294;&#xB2E4;.
          <br />-&#xC54C;&#xACE0;&#xB9AC;&#xC998;&#xC5D0;&#xC11C; &#xAE30;&#xBCF8;&#xC5F0;&#xC0B0;
          &#xC2E4;&#xD589;&#xD69F;&#xC218;&#xB97C; &#xACC4;&#xC0B0;&#xD558;&#xACE0;,
          &#xAE30;&#xBCF8; &#xC5F0;&#xC0B0;&#xC774; &#xB2E4;&#xB97C;&#xACBD;&#xC6B0;
          &#xC2E4;&#xD589; &#xD69F;&#xC218;&#xC5D0; &#xAC00;&#xC911;&#xCE58;&#xB97C;
          &#xC918;&#xC11C; &#xC0C1;&#xB300;&#xC801; &#xACC4;&#xC0B0;&#xB7C9;&#xC744;
          &#xAD6C;&#xD55C;&#xB2E4;.
          <br />2.2.&#xACC4;&#xC0B0;&#xB7C9;&#xC758; &#xD45C;&#xD604;
          <br />-&#xACC4;&#xC0B0;&#xB7C9;&#xC740; &#xC0C1;&#xC218;&#xB85C; &#xD45C;&#xD604;
          &#xD558;&#xC9C0; &#xC54A;&#xB294; &#xC774;&#xC720; - &#xAE30;&#xBCF8; &#xC5F0;&#xC0B0;&#xC758;
          &#xD69F;&#xC218;&#xAC00; &#xC785;&#xB825;&#xC5D0; &#xB530;&#xB77C; &#xC88C;&#xC6B0;&#xB428;,&#xC785;&#xB825;&#xC758;
          &#xD06C;&#xAE30;&#xAC00; &#xAC19;&#xB354;&#xB77C;&#xB3C4; &#xC785;&#xB825;
          &#xC0C1;&#xD0DC;&#xC5D0; &#xB530;&#xB77C; &#xACC4;&#xC0B0;&#xB7C9;&#xC774;
          &#xD2C0;&#xB9BC;.
          <br />-&#xCD5C;&#xC545;&#xC758; &#xACC4;&#xC0B0;&#xB7C9; - &#xC218;&#xD589;&#xD560;
          &#xACC4;&#xC0B0;&#xB7C9;&#xC758; &#xC0C1;&#xD55C;&#xCE58;&#xB97C; &#xC81C;&#xACF5;&#xD558;&#xACE0;,&#xB300;&#xBD80;&#xBD84;&#xC758;
          &#xACBD;&#xC6B0; &#xCD5C;&#xC545;&#xC758; &#xACC4;&#xC0B0;&#xB7C9;&#xC744;
          &#xC0AC;&#xC6A9;&#xD558;&#xBA70;,&#xC54C;&#xACE0;&#xB9AC;&#xC998;&#xC758;
          &#xACC4;&#xC0B0;&#xB7C9;&#xC774;&#xB77C;&#xACE0; &#xD558;&#xBA74;, &#xCD5C;&#xC545;&#xC758;
          &#xACC4;&#xC0B0;&#xB7C9;&#xC744; &#xB73B;&#xD55C;&#xB2E4;.
          <br />-&#xCD5C;&#xC120;&#xC758; &#xACC4;&#xC0B0;&#xB7C9;(B(n)), &#xD3C9;&#xADE0;&#xACC4;&#xC0B0;&#xB7C9;(A(n))
          <br
          />2.3.&#xACC4;&#xC0B0;&#xB7C9;&#xC758; &#xCC28;&#xC218;
          <br />-&#xC9C0;&#xC218;&#xD615; &#xC54C;&#xACE0;&#xB9AC;&#xC998;(exponential
          algorithm) : &#xC54C;&#xACE0;&#xB9AC;&#xC998;&#xC758; &#xC2E4;&#xD589;
          &#xC2DC;&#xAC04;(&#xACC4;&#xC0B0;&#xB7C9;)&#xC774; &#xC9C0;&#xC218;&#xD615;&#xC73C;&#xB85C;
          &#xD45C;&#xD604;
          <br />-&#xB2E4;&#xD56D;&#xC2DD; &#xC54C;&#xACE0;&#xB9AC;&#xC998;(polynomial
          algorithm) : &#xC54C;&#xACE0;&#xB9AC;&#xC998;&#xC758; &#xC2E4;&#xD589;
          &#xC2DC;&#xAC04;(&#xACC4;&#xC0B0;&#xB7C9;)&#xC774; &#xB2E4;&#xD56D;&#xC2DD;&#xC73C;&#xB85C;
          &#xD45C;&#xD604;
          <br />3.&#xAE30;&#xC5B5;&#xC7A5;&#xC18C; &#xC0AC;&#xC6A9;&#xB7C9;-&#xAE30;&#xC5B5;&#xC7A5;&#xC18C;
          &#xC0AC;&#xC6A9;&#xB7C9; &#xBD84;&#xC11D;&#xC740; &#xACC4;&#xC0B0;&#xB7C9;
          &#xBD84;&#xC11D;&#xBCF4;&#xB2E4; &#xC27D;&#xB2E4;. &#xAE30;&#xC5B5;&#xC7A5;&#xC18C;
          &#xC0AC;&#xC6A9;&#xB7C9;&#xACFC; &#xACC4;&#xC0B0;&#xB7C9;&#xC758; &#xAD00;&#xACC4;&#xB294;
          trade-off&#xAD00;&#xACC4;&#xC774;&#xB2E4;.
          <br />4.&#xC815;&#xD655;&#xC131;-&#xBCF5;&#xC7A1;&#xD55C; &#xC54C;&#xACE0;&#xB9AC;&#xC998;&#xC77C;
          &#xACBD;&#xC6B0;, &#xC791;&#xC740; &#xBD80;&#xBD84;&#xC73C;&#xB85C; &#xBD84;&#xD560;&#xD558;&#xC5EC;,
          &#xAC01; &#xBD80;&#xBD84;&#xC774; &#xBAA8;&#xB450; &#xC815;&#xD655;&#xD558;&#xB2E4;&#xB294;
          &#xAC83;&#xC744; &#xC99D;&#xBA85;&#xD568;&#xC73C;&#xB85C;&#xC368; &#xC804;&#xCCB4;
          &#xC54C;&#xACE0;&#xB9AC;&#xC998;&#xC774; &#xC810;&#xD655;&#xD558;&#xB2E4;&#xB294;
          &#xAC83;&#xC744; &#xC99D;&#xBA85;&#xD55C;&#xB2E4;.
          <br />5.&#xAC04;&#xACB0;&#xC131;-&#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC758; &#xC815;&#xD655;&#xC131;&#xC744;
          &#xC27D;&#xAC8C; &#xC99D;&#xBA85;&#xD560; &#xC218; &#xC788;&#xACE0;, &#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC758;
          &#xC218;&#xC815; &#xC791;&#xC5C5;&#xC744; &#xC27D;&#xAC8C; &#xD560;&#xC218;
          &#xC788;&#xB2E4;.</p>
        <p>5&#xC7A5;.&#xC815;&#xC218;,&#xC2E4;&#xC218; &#xBB38;&#xC790;
          <br />1.&#xC815;&#xC218;-&#xC18C;&#xC218;&#xC810;&#xC774; &#xC5C6;&#xB294; &#xC77C;&#xBC18;
          &#xC218; (&#xC74C;&#xC218;&#xB294; 2&#xC758; &#xBCF4;&#xC218;&#xB97C; &#xC0AC;&#xC6A9;&#xD55C;&#xB2E4;)
          <br
          />2.&#xC2E4;&#xC218;-&#xC18C;&#xC218;&#xC810;&#xC774; &#xC788;&#xB294; &#xC218;
          (&#xC804;&#xCCB4; &#xBD80;&#xD638;,&#xAC00;&#xC218;,&#xC9C0;&#xC218; &#xBD80;&#xD638;,
          &#xC9C0;&#xC218;&#xB85C; &#xAD6C;&#xC131;)
          <br />3,&#xBB38;&#xC790;-&#xBB38;&#xC790;&#xAC00; &#xAE30;&#xC5B5;&#xC7A5;&#xC18C;&#xC5D0;
          &#xC800;&#xC7A5;&#xB418;&#xB294; &#xB2E8;&#xC704;&#xB294; byte,&#xBB38;&#xC790;&#xB97C;
          &#xC774;&#xC9C4;&#xC218;&#xB85C; &#xD45C;&#xD604;&#xD558;&#xAE30; &#xC704;&#xD574;
          ASCII&#xC640; EBCDIC&#xB97C; &#xC0AC;&#xC6A9;&#xD55C;&#xB2E4;.</p>
        <p>6&#xC7A5;.&#xBC30;&#xC5F4;,&#xAD6C;&#xC870;&#xCCB4;,&#xD3EC;&#xC778;&#xD130;
          <br
          />1.&#xBC30;&#xC5F4;
          <br />1.1.&#xBC30;&#xC5F4;&#xC758; &#xC800;&#xC7A5;&#xBC29;&#xBC95;
          <br />-&#xC77C;&#xCC28;&#xC6D0; &#xBC30;&#xC5F4;&#xC758; &#xC800;&#xC7A5; &#xBC29;&#xBC95;:&#xAE30;&#xC5B5;&#xC7A5;&#xC18C;&#xC5D0;
          &#xC800;&#xC7A5;&#xB418;&#xB294; &#xBB3C;&#xB9AC;&#xC801;&#xC778; &#xC21C;&#xC11C;&#xB97C;
          &#xB17C;&#xB9AC;&#xC801; &#xC21C;&#xC11C;&#xC640; &#xAC19;&#xB3C4;&#xB85D;
          &#xC800;&#xC7A5;&#xD568;. &#xC6D0;&#xC18C; a[i+1]&#xC758; &#xC800;&#xC7A5;
          &#xC7A5;&#xC18C;&#xAC00; a[i] &#xC800;&#xC7A5; &#xC7A5;&#xC18C;&#xC5D0;
          &#xBC14;&#xB85C; &#xC778;&#xC811;
          <br />-&#xB2E4;&#xCC28;&#xC6D0; &#xBC30;&#xC5F4;&#xC758; &#xC800;&#xC7A5; &#xBC29;&#xBC95;:&#xD589;&#xC6B0;&#xC120;
          &#xC21C;&#xC11C; (row major order) &#xBC29;&#xBC95; ,&#xC5F4;&#xC6B0;&#xC120;
          &#xC21C;&#xC11C; (column major order) &#xBC29;&#xBC95;
          <br />1.2.&#xBC30;&#xC5F4;&#xC758; &#xC5F0;&#xC0B0;
          <br />-&#xBC30;&#xC5F4;&#xC758; &#xC800;&#xC7A5;&#xC21C;&#xC11C;&#xB97C; &#xACE0;&#xB824;&#xD558;&#xC5EC;
          &#xC778;&#xC811;&#xD55C; &#xC6D0;&#xC18C;&#xB97C; &#xCC28;&#xB840;&#xB85C;
          &#xCC98;&#xB9AC;&#xD558;&#xB294; &#xAC83;&#xC774; &#xD6A8;&#xC728;&#xC801;&#xC784;.
          <br
          />-&#xC0BD;&#xC785;/&#xC0AD;&#xC81C; &#xC5F0;&#xC0B0;&#xC758; &#xD69F;&#xC218;&#xAC00;
          &#xB9CE;&#xB2E4;&#xBA74; &#xBC30;&#xC5F4;&#xC740; &#xD6A8;&#xC728;&#xC801;&#xC778;
          &#xC790;&#xB8CC; &#xAD6C;&#xC870;&#xAC00;&#xC544;&#xB2D8;.
          <br />1.3.&#xD76C;&#xC18C; &#xBC30;&#xC5F4;
          <br />-&#xD76C;&#xC18C; &#xBC30;&#xC5F4; &#xBC30;&#xC5F4;&#xC758; &#xC6D0;&#xC18C;&#xAC12;&#xC774;
          0&#xC778; &#xC6D0;&#xC18C;&#xAC00; &#xBE44;&#xAD50;&#xC801; &#xB9CE;&#xC740;
          &#xBC30;&#xC5F4;
          <br />-&#xD76C;&#xC18C; &#xBC30;&#xC5F4;&#xC744; &#xD45C;&#xD604;&#xD558;&#xAE30;
          &#xC704;&#xD574;&#xC11C; &#xBC30;&#xC5F4; &#xAC12;&#xC774; 0&#xC774; &#xC544;&#xB2CC;
          &#xC6D0;&#xC18C;&#xB9CC; &#xC800;&#xC7A5;&#xD558;&#xB294; &#xBC29;&#xBC95;&#xC774;
          &#xD544;&#xC694;
          <br />2.&#xAD6C;&#xC870;&#xCCB4;
          <br />2.1.&#xC815;&#xC758;-&#xB17C;&#xB9AC;&#xC801;&#xC73C;&#xB85C; &#xC11C;&#xB85C;
          &#xAD00;&#xB828;&#xB41C; &#xC790;&#xB8CC;&#xB4E4;&#xC744; &#xC9D1;&#xB2E8;&#xD654;&#xD55C;
          &#xC790;&#xB8CC;&#xAD6C;&#xC870;, &#xAD6C;&#xC870;&#xCCB4;&#xC640; &#xBA64;&#xBC84;&#xB97C;
          &#xB808;&#xCF54;&#xB4DC;(record)&#xC640; &#xD544;&#xB4DC;(field)&#xB77C;
          &#xBD80;&#xB984;.
          <br />2.2.&#xAD6C;&#xC870;&#xCCB4;&#xC758; &#xC800;&#xC7A5; &#xBC29;&#xBC95;-&#xAD6C;&#xC870;&#xCCB4;&#xC758;
          &#xCCAB; &#xB9F4;&#xBC84;&#xAC00; &#xCCAB; &#xC704;&#xCE58;&#xC5D0; &#xC800;&#xC7A5;&#xB418;&#xACE0;,
          &#xB9C8;&#xC9C0;&#xB9C9; &#xBA64;&#xBC84;&#xAC00; &#xB9C8;&#xC9C0;&#xB9C9;
          &#xC704;&#xCE58;&#xC5D0; &#xC800;&#xC7A5;&#xB41C;&#xB2E4;.
          <br />3.&#xD3EC;&#xC778;&#xD130;
          <br />3.1.&#xD3EC;&#xC778;&#xD130;&#xC640; &#xBC30;&#xC5F4;- a &#xB294; a[0]&#xB97C;
          &#xAC00;&#xB974;&#xD0A4;&#xB294; &#xD3EC;&#xC778;&#xD130;&#xC774;&#xB2E4;..
          a&#xAC00; &#xC8FC;&#xC18C; &#xAC12;&#xC774;&#xBBC0;&#xB85C; a&#xB294; &#xBCC0;&#xC218;&#xAC00;
          &#xC544;&#xB2C8;&#xACE0; &#xC0C1;&#xC218;&#xC774;&#xB2E4;.
          <br />3.2.&#xB3D9;&#xC801; &#xAE30;&#xC5B5;&#xC7A5;&#xC18C; &#xD560;&#xB2F9;-
          &#xC2E4;&#xD589;&#xC2DC;&#xAC04;&#xC5D0; &#xAE30;&#xC5B5;&#xC7A5;&#xC18C;&#xB97C;
          &#xD560;&#xB2F9;&#xD558;&#xB294; &#xAC83;&#xC774;&#xBA70;, C&#xC5D0;&#xC11C;&#xB294;
          malloc()&#xB97C; &#xC0AC;&#xC6A9;, C++&#xC5D0;&#xC11C;&#xB294; new&#xB77C;&#xB294;
          &#xC5F0;&#xC0B0;&#xC790;&#xB97C; &#xC0AC;&#xC6A9;&#xD55C;&#xB2E4;.</p>
        <p>7&#xC7A5;.&#xC815;&#xB82C;,&#xD0D0;&#xC0C9;
          <br />1.&#xC815;&#xB82C;
          <br />1.1.&#xC120;&#xD0DD;&#xC815;&#xB82C;
          <br />-&#xAE30;&#xCD08;&#xC801;&#xC778; &#xC815;&#xB82C; &#xC54C;&#xACE0;&#xB9AC;&#xC998;&#xC758;
          &#xD558;&#xB098;&#xB85C; &#xC804;&#xCCB4; &#xC6D0;&#xC18C;&#xB4E4; &#xC911;&#xC5D0;&#xC11C;
          &#xAE30;&#xC900; &#xC704;&#xCE58;&#xC5D0; &#xB9DE;&#xB294; &#xC6D0;&#xC18C;&#xB97C;
          &#xC120;&#xD0DD;&#xD558;&#xC5EC; &#xC790;&#xB9AC;&#xB97C; &#xAD50;&#xD658;&#xD558;&#xB294;
          &#xBC29;&#xC2DD;&#xC73C;&#xB85C; &#xC815;&#xB82C;&#xD55C;&#xB2E4;.
          <br />-&#xBA54;&#xBAA8;&#xB9AC;&#xC758; &#xC0AC;&#xC6A9;&#xACF5;&#xAC04;&#xC740;
          n&#xAC1C;&#xC758; &#xC6D0;&#xC18C;&#xC5D0; &#xB300;&#xD574; n&#xAC1C;&#xC758;
          &#xBA54;&#xBAA8;&#xB9AC;&#xB97C; &#xC0AC;&#xC6A9;&#xD558;&#xACE0;, &#xC2DC;&#xAC04;&#xBCF5;&#xC7A1;&#xB3C4;&#xB294;
          O(n^2)&#xC774;&#xB2E4;.
          <br />1.2.&#xC0BD;&#xC785;&#xC815;&#xB82C;
          <br />-&#xC815;&#xB82C;&#xB418;&#xC9C0; &#xC54A;&#xC740; &#xB9AC;&#xC2A4;&#xD2B8;&#xC758;
          &#xD55C; &#xC6D0;&#xC18C;&#xC529;&#xC744; &#xC815;&#xB82C;&#xB41C; &#xB9AC;&#xC2A4;&#xD2B8;&#xC5D0;
          &#xC81C; &#xC704;&#xCE58;&#xB97C; &#xCC3E;&#xC544; &#xC0BD;&#xC785;&#xD55C;&#xB2E4;.
          <br
          />-&#xCE74;&#xB4DC;&#xB97C; &#xD55C; &#xC7A5;&#xC529; &#xB3CC;&#xB824;&#xBC1B;&#xC744;
          &#xB54C; &#xC190;&#xC5D0; &#xC774;&#xBBF8; &#xC815;&#xB82C;&#xB418;&#xC5B4;
          &#xC788;&#xB294; &#xCE74;&#xB4DC; &#xC18D;&#xC5D0; &#xC0C8; &#xCE74;&#xB4DC;&#xB97C;
          &#xC0BD;&#xC785;&#xD558;&#xB294; &#xBC29;&#xBC95;&#xC774;&#xB2E4;.
          <br />1.3.&#xBC84;&#xBE14;&#xC815;&#xB82C;
          <br />-&#xBC14;&#xB85C; &#xC778;&#xC811;&#xD574; &#xC788;&#xB294; &#xB450; &#xAC1C;&#xC758;
          &#xC6D0;&#xC18C;&#xB97C; &#xBE44;&#xAD50;&#xD558;&#xC5EC; &#xC21C;&#xC11C;&#xAC00;
          &#xBC14;&#xB00C;&#xC5B4; &#xC788;&#xC73C;&#xBA74; &#xC11C;&#xB85C; &#xC704;&#xCE58;&#xB97C;
          &#xBC14;&#xAFB8;&#xC5B4; &#xC791;&#xC740; &#xAC12;&#xC758; &#xC6D0;&#xC18C;&#xB97C;
          &#xBC30;&#xC5F4;&#xC758; &#xC704;&#xCABD;&#xC5D0; &#xC624;&#xAC8C; &#xD558;&#xACE0;
          &#xD070;&#xAC12;&#xC758; &#xC6D0;&#xC18C;&#xB97C; &#xC544;&#xB798;&#xCABD;&#xC73C;&#xB85C;
          &#xAC00;&#xB3C4;&#xB85D; &#xD558;&#xB294; &#xAC83;&#xC774;&#xB2E4;.
          <br
          />-&#xAC01; pass &#xAC00; &#xB05D;&#xB098;&#xBA74; &#xD070; &#xAC12;&#xC758;
          &#xC6D0;&#xC18C;&#xAC00; &#xC81C; &#xC704;&#xCE58;&#xB85C; &#xAC00;&#xAC8C;&#xB41C;&#xB2E4;.
          <br
          />1.4.&#xC258;&#xC815;&#xB82C;
          <br />-&#xBC84;&#xBE14;&#xC815;&#xB82C;&#xC5D0;&#xC11C; &#xC790;&#xB8CC;&#xC758;
          &#xC704;&#xCE58;&#xAC00; &#xC815;&#xB82C;&#xB41C; &#xC704;&#xCE58;&#xC5D0;&#xC11C;
          &#xBA40;&#xB9AC; &#xB5A8;&#xC5B4;&#xC838; &#xC788;&#xB2E4;&#xBA74; &#xC5EC;&#xB7EC;&#xBC88;
          &#xAD50;&#xD658;&#xC774; &#xD544;&#xC694;&#xD558;&#xAE30; &#xB54C;&#xBB38;&#xC5D0;,
          &#xBA40;&#xB9AC; &#xB5A8;&#xC5B4;&#xC838; &#xC788;&#xB294; &#xC6D0;&#xC18C;&#xB07C;&#xB9AC;
          &#xBE44;&#xAD50; &#xAD50;&#xD658;&#xD558;&#xB3C4;&#xB85D; &#xD568;.
          <br
          />1.5.&#xD569;&#xBCD1; &#xC815;&#xB82C;
          <br />-&#xC815;&#xB82C;&#xB41C; &#xBC30;&#xC5F4;&#xC758; &#xD569;&#xBCD1;:&#xAC01;
          &#xBC30;&#xC5F4;&#xC758; &#xC6D0;&#xC18C;&#xB97C; &#xC21C;&#xCC28;&#xC801;&#xC73C;&#xB85C;
          &#xBE44;&#xAD50;&#xD558;&#xC5EC; &#xC791;&#xC740; &#xAC12;&#xC744; &#xBCC4;&#xB3C4;&#xC758;
          &#xBC30;&#xC5F4;&#xC5D0; &#xCD9C;&#xB825;
          <br />-&#xD569;&#xBCD1; &#xC815;&#xB82C;- &#xC6D0; &#xD569;&#xBCD1;&#xC744;
          &#xC77C;&#xBC18;&#xD654; &#xD558;&#xC5EC; &#xC784;&#xC758;&#xC758; m &#xAC1C;
          &#xBD80;&#xBD84; &#xB9AC;&#xC2A4;&#xD2B8;&#xB97C; &#xD569;&#xBCD1;(&#xB2E4;&#xC911;
          &#xD569;&#xBCD1;, m-&#xC6D0; &#xD569;&#xBCD1;&#xC815;&#xB82C;)
          <br />1.6.&#xD035;&#xC815;&#xB82C;
          <br />-&#xAC00;&#xC7A5; &#xD6A8;&#xC728;&#xC801;&#xC778; &#xBC29;&#xBC95;&#xC73C;&#xB85C;
          &#xC138; &#xB2E8;&#xACC4;&#xB85C; &#xC218;&#xD589;&#xB41C;&#xB2E4;.
          <br
          />-&gt; &#xD55C; &#xD328;&#xC2A4; &#xB3D9;&#xC548; &#xC784;&#xC758;&#xC758;
          &#xC6D0;&#xC18C;&#xB97C; &#xC120;&#xC815;&#xD55C;&#xB2E4;. ( pivot &#xC6D0;&#xC18C;)
          <br
          />-&gt; &#xC774; &#xC6D0;&#xC18C;&#xB97C; &#xAE30;&#xC900;&#xC73C;&#xB85C;
          &#xC804;&#xCCB4;&#xB97C; &#xB450; &#xBD80;&#xBD84;&#xB9AC;&#xC2A4;&#xD2B8;&#xB85C;
          &#xBD84;&#xD560;&#xD55C;&#xB2E4;.(pivot &#xAC12;&#xC744; &#xAE30;&#xC900;&#xC73C;&#xB85C;
          &#xAC12;&#xC774; &#xD070; &#xC6D0;&#xC18C;&#xC640; &#xAC12;&#xC774; &#xC801;&#xC740;
          &#xB9AC;&#xC2A4;&#xD2B8;&#xB85C; &#xBD84;&#xB958;)
          <br />-&gt; &#xAC01; &#xBD80;&#xBD84; &#xB9AC;&#xC2A4;&#xC5D0; &#xB300;&#xD558;&#xC5EC;
          &#xB2E8;&#xACC4; 2&#xB97C; &#xBC18;&#xBCF5; &#xC218;&#xD589;&#xD55C;&#xB2E4;.
          <br
          />1.7.&#xBCF4;&#xC870;&#xD14C;&#xC774;&#xBE14;&#xC744; &#xC0AC;&#xC6A9;&#xD55C;
          &#xC815;&#xB82C;
          <br />-&#xBCF4;&#xC870; &#xD14C;&#xC774;&#xBE14;&#xC5D0;&#xB294; &#xB808;&#xCF54;&#xB4DC;
          &#xBC88;&#xD638;(&#xB808;&#xCF54;&#xB4DC; &#xC778;&#xB371;&#xC2A4;)&#xB97C;
          &#xC800;&#xC7A5;&#xD558;&#xACE0;, &#xC2E4;&#xC81C; &#xB370;&#xC774;&#xD130;&#xB97C;
          &#xC815;&#xB82C;&#xD558;&#xB294; &#xB300;&#xC2E0; &#xBCF4;&#xC870;&#xD14C;&#xC774;&#xBE14;&#xC758;
          &#xB808;&#xCF54;&#xB4DC; &#xBC88;&#xD638;&#xB97C; &#xC815;&#xB82C;&#xD55C;&#xB2E4;.
          <br
          />2.&#xD0D0;&#xC0C9;
          <br />2.1.&#xC120;&#xD615; &#xD0D0;&#xC0C9;
          <br />-&#xD0D0;&#xC0C9;&#xD558;&#xACE0;&#xC790; &#xD558;&#xB294; &#xC790;&#xB8CC;&#xC640;
          &#xBC30;&#xC5F4;&#xC758; &#xC6D0;&#xC18C;&#xB97C; &#xD558;&#xB098;&#xC529;
          &#xC21C;&#xCC28;&#xC801;&#xC73C;&#xB85C; &#xBE44;&#xAD50;&#xD55C;&#xB2E4;.
          <br
          />2.2.&#xC774;&#xC9C4; &#xD0D0;&#xC0C9;
          <br />-&#xC77C;&#xBC18;&#xC801;&#xC73C;&#xB85C; &#xC0AC;&#xC804;&#xC5D0; &#xB2E8;&#xC5B4;&#xB97C;
          &#xCC3E;&#xB294; &#xBC29;&#xBC95;&#xACFC; &#xBE44;&#xC2B7;&#xD558;&#xB2E4;.
          <br
          />-&#xBC30;&#xC5F4;&#xC758; &#xC6D0;&#xC18C;&#xAC00; &#xC815;&#xB82C;&#xB418;&#xC5B4;&#xC57C;
          &#xD55C;&#xB2E4;.
          <br />-&#xBC30;&#xC5F4;&#xC758; &#xC911;&#xC559; &#xC6D0;&#xC18C;&#xB97C; &#xCC3E;&#xC544;
          &#xAC12;&#xC744; &#xBE44;&#xAD50;&#xD55C; &#xD6C4;, &#xBE44;&#xAD50; &#xACB0;&#xACFC;&#xC5D0;
          &#xB530;&#xB77C; &#xC911;&#xC559;&#xC758; &#xC55E; &#xD639;&#xC740; &#xB4B7;
          &#xBD80;&#xBD84;&#xC744; &#xC774;&#xC804;&#xACFC; &#xB3D9;&#xC77C; &#xD558;&#xAC8C;
          &#xAC80;&#xC0C9;&#xD558;&#xB294; &#xBC29;&#xBC95;&#xC774;&#xB2E4;.
          <br />-&#xC774;&#xC9C4; &#xD0D0;&#xC0C9;&#xC740; &#xBC30;&#xC5F4;&#xC5D0;&#xC11C;
          &#xC790;&#xB8CC; &#xC6D0;&#xC18C;&#xC758; &#xC0BD;&#xC785;&#xC774;&#xB098;
          &#xC0AD;&#xC81C;&#xAC00; &#xAC70;&#xC758; &#xC5C6;&#xB294; &#xACBD;&#xC6B0;&#xC5D0;
          &#xC801;&#xD569;
          <br />2.3.&#xC778;&#xB371;&#xC2A4; &#xC21C;&#xCC28; &#xD0D0;&#xC0C9;
          <br />-&#xC815;&#xB82C;&#xB41C; &#xBC30;&#xC5F4;&#xC5D0;&#xC11C; &#xD0D0;&#xC0C9;&#xD558;&#xB294;
          &#xBC29;&#xBC95;&#xC73C;&#xB85C;, &#xBC30;&#xC5F4;&#xC758; &#xAD6C;&#xAC04;
          &#xC815;&#xBCF4;&#xB97C; &#xAC00;&#xC9C0;&#xB294; &#xC778;&#xB371;&#xC2A4;
          &#xD14C;&#xC774;&#xBE14;&#xC744; &#xAD6C;&#xCD95;&#xD558;&#xC5EC; &#xD0D0;&#xC0C9;&#xD55C;&#xB2E4;.
          <br
          />-&#xC774;&#xC9C4; &#xD0D0;&#xC0C9;&#xBCF4;&#xB2E4; &#xD0D0;&#xC0C9; &#xAD6C;&#xAC04;&#xC744;
          &#xC904;&#xC77C;&#xC218; &#xC788;&#xB2E4;.
          <br />-&#xC778;&#xB371;&#xC2A4; &#xD14C;&#xC774;&#xBE14;&#xC774; &#xCEE4;&#xC9C0;&#xBA74;
          &#xC774;&#xCC28; &#xBCF4;&#xC870; &#xC778;&#xB371;&#xC2A4; &#xD14C;&#xC774;&#xBE14;&#xC744;
          &#xAD6C;&#xCD95;&#xD560; &#xC218; &#xC788;&#xB2E4;.</p>
        <p>8&#xC7A5;.&#xC2A4;&#xD0DD;,&#xD050;,&#xB9AC;&#xC2A4;&#xD2B8;,&#xD2B8;&#xB9AC;,&#xD574;&#xC2F1;
          <br
          />1.&#xC2A4;&#xD0DD;
          <br />1.1.&#xC815;&#xC758;-&quot;&#xC2A4;&#xD0DD;&quot;&#xC774;&#xB780; &#xC5EC;&#xB7EC;
          &#xAC1C;&#xC758; &#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xB4E4;&#xC774;
          &#xC77C;&#xC815;&#xD55C; &#xC21C;&#xC11C;&#xB85C; &#xB098;&#xC5F4;&#xB41C;
          &#xC790;&#xB8CC; &#xAD6C;&#xC870;&#xB85C;, &#xD55C;&#xCABD; &#xB05D;&#xC5D0;&#xC11C;&#xB9CC;
          &#xC0C8;&#xB85C;&#xC6B4; &#xD56D;&#xBAA9;&#xC744; &#xC0BD;&#xC785;&#xD558;&#xAC70;&#xB098;
          &#xAE30;&#xC874; &#xD56D;&#xBAA9;&#xC744; &#xC0AD;&#xC81C;&#xD560; &#xC218;
          &#xC788;&#xB3C4;&#xB85D; &#xACE0;&#xC548;&#xB41C; &#xAC83;&#xC774;&#xB2E4;.
          <br
          />1.2.&#xAD6C;&#xC870;
          <br />-&#xC2A4;&#xD0DD;&#xC740; &#xAE30;&#xC800;(base)&#xB85C;&#xBD80;&#xD130;
          &#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xB4E4;&#xC744; &#xCC28;&#xB840;&#xB85C;
          &#xC313;&#xC544;&#xC62C;&#xB9B0; &#xBAA8;&#xC591;&#xC744; &#xAC00;&#xC9C4;&#xB2E4;.
          <br
          />-&#xC0BD;&#xC785;&#xACFC; &#xC0AD;&#xC81C;&#xB294; &#xD604;&#xC7AC; &#xC800;&#xC7A5;&#xB41C;
          &#xCD5C;&#xC0C1;&#xC704; &#xD56D;&#xBAA9;&#xC774; &#xC704;&#xCE58;&#xD55C;
          top &#xC5D0;&#xC11C;&#xB9CC; &#xC77C;&#xC5B4;&#xB09C;&#xB2E4;.
          <br />-top &#xC704;&#xCE58;&#xB294; &quot;&#xC2A4;&#xD0DD; &#xD3EC;&#xC778;&#xD130;&quot;&#xB77C;&#xB294;
          &#xC9C0;&#xC2DC;&#xC790;&#xAC00; &#xAC00;&#xB9AC;&#xD0A8;&#xB2E4;.
          <br />-&#xC2A4;&#xD0DD; &#xD3EC;&#xC778;&#xD130;&#xB294; &#xC2A4;&#xD0DD; &#xAE30;&#xC800;&#xC5D0;&#xC11C;
          &#xC2DC;&#xC791;&#xD558;&#xC5EC; &#xD56D;&#xBAA9;&#xC774; &#xC0BD;&#xC785;&#xB418;&#xBA74;
          &#xD558;&#xB098; &#xC99D;&#xAC00;&#xD558;&#xACE0;, &#xC0AD;&#xC81C;&#xB418;&#xBA74;
          &#xD558;&#xB098; &#xAC10;&#xC18C;&#xD55C;&#xB2E4;.
          <br />-&#xC2A4;&#xD0DD;&#xC5D0;&#xB294; &#xD55C;&#xACC4;&#xAC00; &#xC788;&#xC5B4;&#xC11C;
          &#xADF8; &#xD55C;&#xACC4;&#xB97C; &#xCD08;&#xACFC;&#xD558;&#xB3C4;&#xB85D;
          &#xC0BD;&#xC785;&#xD560; &#xC218; &#xC5C6;&#xB2E4;.
          <br />1.3.&#xC2A4;&#xD0DD;&#xC5D0; &#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;
          &#xC0BD;&#xC785; (push)
          <br />-&#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xC744; &#xC0BD;&#xC785;&#xD558;&#xB824;&#xBA74;
          &#xC2A4;&#xD0DD; &#xD3EC;&#xC778;&#xD130;&#xB97C; &#xD558;&#xB098;&#xB9CC;&#xD07C;
          &#xC99D;&#xAC00;&#xC2DC;&#xCF1C; &#xC8FC;&#xACE0; &#xC2A4;&#xD0DD;&#xC758;
          top &#xC5D0; &#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xC744; &#xC800;&#xC7A5;&#xD55C;&#xB2E4;.
          <br
          />-&#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xC744; &#xC0BD;&#xC785;&#xD558;&#xAE30;
          &#xC804;&#xC5D0; &#xC0C8;&#xB85C;&#xC6B4; &#xD56D;&#xBAA9;&#xC744; &#xC800;&#xC7A5;&#xD560;
          &#xBE48; &#xACF5;&#xAC04;&#xC774; &#xC788;&#xB294;&#xC9C0; &#xAC80;&#xC0AC;(Full&#xAC80;&#xC0AC;)&#xD574;&#xC57C;
          &#xD55C;&#xB2E4;.
          <br />1.4.Full&#xAC80;&#xC0AC;
          <br />-&#xC2A4;&#xD0DD;&#xC774; &#xAC00;&#xB4DD;&#xCC28; &#xC788;&#xC73C;&#xBA74;
          &#xC0C8;&#xB85C;&#xC6B4; &#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xC744;
          &#xC0BD;&#xC785;&#xD560; &#xC218; &#xC5C6;&#xB2E4;. &#xB370;&#xC774;&#xD0C0;
          &#xD56D;&#xBAA9;&#xC744; &#xC0BD;&#xC785;&#xD558;&#xAE30; &#xC804;&#xC5D0;
          &#xBA3C;&#xC800;, &#xC2A4;&#xD0DD; &#xD3EC;&#xC778;&#xD130;&#xAC00; &#xC2A4;&#xD0DD;&#xC758;
          &#xD55C;&#xACC4;&#xC5D0; &#xB3C4;&#xB2EC;&#xD574; &#xC788;&#xB294;&#xC9C0;
          &#xAC80;&#xC0AC;&#xD574;&#xC57C; &#xD55C;&#xB2E4;
          <br />1.5.&#xC2A4;&#xD0DD;&#xC5D0;&#xC11C; &#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;
          &#xC0AD;&#xC81C; (pop)
          <br />-&#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xC744; &#xC0AD;&#xC81C;&#xD558;&#xB824;&#xBA74;
          &#xC2A4;&#xD0DD;&#xC758; top &#xC5D0; &#xC788;&#xB294; &#xB370;&#xC774;&#xD0C0;
          &#xD56D;&#xBAA9;&#xC744; &#xC81C;&#xAC70;&#xD558;&#xACE0; &#xC2A4;&#xD0DD;
          &#xD3EC;&#xC778;&#xD130;&#xB97C; &#xD558;&#xB098;&#xB9CC;&#xD07C; &#xAC10;&#xC18C;&#xC2DC;&#xCF1C;
          &#xC900;&#xB2E4;.
          <br />-&#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xC744; &#xC0AD;&#xC81C;&#xD558;&#xAE30;
          &#xC804;&#xC5D0; &#xC2A4;&#xD0DD;&#xC774; &#xBE44;&#xC5B4;&#xC788;&#xB294;&#xC9C0;&#xB97C;
          &#xAC80;&#xC0AC;(Empty&#xAC80;&#xC0AC;)&#xD574;&#xC57C; &#xD55C;&#xB2E4;.
          <br
          />1.6.Empty &#xAC80;&#xC0AC;
          <br />-&#xC2A4;&#xD0DD;&#xC774; &#xBE44;&#xC5B4; &#xC788;&#xC73C;&#xBA74;, &#xB370;&#xC774;&#xD0C0;
          &#xD56D;&#xBAA9;&#xC744; &#xC0AD;&#xC81C;&#xD560; &#xC218; &#xC5C6;&#xB2E4;.
          &#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xC744; &#xC0AD;&#xC81C;&#xD558;&#xAE30;
          &#xC804;&#xC5D0; &#xC2A4;&#xD0DD; &#xD3EC;&#xC778;&#xD130;&#xAC00; &#xAE30;&#xC800;&#xC5D0;
          &#xB3C4;&#xB2EC;&#xD574; &#xC788;&#xB294;&#xC9C0;&#xB97C; &#xAC80;&#xC0AC;&#xD574;&#xC57C;
          &#xD55C;&#xB2E4;.
          <br />2.&#xD050;
          <br />2.1.&#xC815;&#xC758;-&quot;&#xD050;&quot;&#xB294; &#xC5EC;&#xB7EC; &#xAC1C;&#xC758;
          &#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xB4E4;&#xC774; &#xC77C;&#xC815;&#xD55C;
          &#xC21C;&#xC11C;&#xB85C; &#xB098;&#xC5F4;&#xB41C; &#xC790;&#xB8CC; &#xAD6C;&#xC870;&#xC774;&#xB2E4;.
          &#xC2A4;&#xD0DD;&#xACFC;&#xB294; &#xB2EC;&#xB9AC; &#xD55C;&#xCABD; &#xB05D;&#xC5D0;&#xC11C;&#xB294;
          &#xC0BD;&#xC785;&#xB9CC; &#xD560; &#xC218; &#xC788;&#xACE0;, &#xC0AD;&#xC81C;&#xB294;
          &#xBC18;&#xB300;&#xCABD; &#xB05D;&#xC5D0;&#xC11C;&#xB9CC; &#xD560; &#xC218;
          &#xC788;&#xB3C4;&#xB85D; &#xB418;&#xC5B4; &#xC788;&#xB2E4;.
          <br />2.2.&#xC885;&#xB958;-&#xD050;&#xC5D0;&#xB294; &#xD55C; &#xBC29;&#xD5A5;&#xC73C;&#xB85C;
          &#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xB4E4;&#xC774; &#xC0BD;&#xC785;/&#xC0AD;&#xC81C;&#xB418;&#xB294;
          &#xC120;&#xD615; &#xD050;&#xC640; &#xC2DC;&#xC791;&#xC810;&#xACFC; &#xB05D;&#xC810;&#xC774;
          &#xC11C;&#xB85C; &#xC5F0;&#xACB0;&#xB418;&#xC5B4; &#xC788;&#xB294; &#xD658;&#xD615;
          &#xD050;&#xAC00; &#xC788;&#xB2E4;.
          <br />2.2.1.&#xC120;&#xD615;&#xD050;
          <br />-&#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xC744; &#xC0BD;&#xC785;&#xD558;&#xB824;&#xBA74;
          &#xD050;&#xC758; rear &#xD3EC;&#xC778;&#xD130;&#xB97C; &#xD558;&#xB098;&#xB9CC;&#xD07C;
          &#xC99D;&#xAC00;&#xC2DC;&#xCF1C; &#xC8FC;&#xACE0; &#xADF8; &#xC704;&#xCE58;&#xC5D0;
          &#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xC744; &#xC800;&#xC7A5;&#xD55C;&#xB2E4;.
          <br
          />-&#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xC744; &#xC0AD;&#xC81C;&#xD558;&#xB824;&#xBA74;
          &#xD050;&#xC758; front &#xD3EC;&#xC778;&#xD130;&#xB97C; &#xD558;&#xB098;&#xB9CC;&#xD07C;
          &#xC99D;&#xAC00;&#xC2DC;&#xD0A4;&#xACE0; &#xADF8; &#xC704;&#xCE58;&#xC5D0;
          &#xC788;&#xB294; &#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xC744; &#xC0AD;&#xC81C;&#xD55C;&#xB2E4;.
          <br
          />-&#xC0BD;&#xC785;&#xC774; &#xACC4;&#xC18D;&#xB418;&#xC5B4; rear &#xD3EC;&#xC778;&#xD130;&#xAC00;
          &#xC0C1;&#xD55C;&#xC5D0; &#xB3C4;&#xB2EC;&#xD558;&#xBA74; &#xB354;&#xC774;&#xC0C1;
          &#xC0BD;&#xC785;&#xC774; &#xBD88;&#xAC00;&#xB2A5;&#xD55C; &#xC0C1;&#xD0DC;&#xAC00;
          &#xB41C;&#xB2E4;.
          <br />2.2.2.&#xD658;&#xD615;&#xD050;
          <br />-&#xC0BD;&#xC785;&#xACFC; &#xC0AD;&#xC81C; &#xB3D9;&#xC791;&#xC740; &#xC120;&#xD615;
          &#xD050;&#xC640; &#xAC19;&#xC9C0;&#xB9CC;, &#xD050;&#xC758; &#xC0C1;&#xD55C;&#xACFC;
          &#xD558;&#xD55C;&#xC774; &#xC11C;&#xB85C; &#xC5F0;&#xACB0;&#xB41C; &#xACE0;&#xB9AC;
          &#xBAA8;&#xC591;&#xC744; &#xD558;&#xACE0; &#xC788;&#xC5B4;, &#xC0AC;&#xC2E4;&#xC0C1;
          &#xD050;&#xC758; &#xD55C;&#xACC4;&#xAC00; &#xC5C6;&#xB294; &#xAC83;&#xACFC;
          &#xAC19;&#xB2E4;.
          <br />-&#xD658;&#xD615; &#xD050;&#xB97C; &#xC774;&#xC6A9;&#xD558;&#xBA74; rear
          &#xD3EC;&#xC778;&#xD130;&#xAC00; &#xC0C1;&#xD55C;&#xC5D0; &#xB3C4;&#xB2EC;&#xD558;&#xC5EC;
          &#xC0BD;&#xC785;&#xC774; &#xC911;&#xB2E8;&#xB418;&#xB294; &#xBB38;&#xC81C;&#xB97C;
          &#xD574;&#xACB0;&#xD560; &#xC218;&#xB294; &#xC788;&#xC9C0;&#xB9CC; &#xD050;&#xC758;
          &#xC6A9;&#xB7C9;&#xC744; &#xCD08;&#xACFC;&#xD558;&#xC5EC; &#xB370;&#xC774;&#xD0C0;
          &#xD56D;&#xBAA9;&#xC744; &#xC0BD;&#xC785;&#xD560; &#xC218;&#xB294; &#xC5C6;&#xB2E4;.
          <br
          />-front &#xD3EC;&#xC778;&#xD130;&#xC640; rear &#xD3EC;&#xC778;&#xD130;&#xAC00;
          &#xAC19;&#xC740; &#xACBD;&#xC6B0;&#xB97C; &#xD050; full &#xACFC; &#xD050;
          empty &#xC870;&#xAC74;&#xC73C;&#xB85C; &#xC0AC;&#xC6A9;&#xD558;&#xBA74;
          &#xB450; &#xAC00;&#xC9C0; &#xACBD;&#xC6B0;&#xB97C; &#xAD6C;&#xBCC4;&#xD560;
          &#xC218; &#xC5C6;&#xB2E4;.&#xC774;&#xAC83;&#xC744; &#xAD6C;&#xBCC4;&#xD558;&#xAE30;
          &#xC704;&#xD574; &#xD558;&#xB098;&#xC758; &#xC5EC;&#xC720; &#xACF5;&#xAC04;&#xC744;
          &#xB450;&#xACE0; &#xADF8; &#xACF5;&#xAC04;&#xC740; &#xC0AC;&#xC6A9;&#xD558;&#xC9C0;
          &#xBABB;&#xD558;&#xB3C4;&#xB85D; &#xD55C;&#xB2E4;.
          <br />3.&#xB9AC;&#xC2A4;&#xD2B8;
          <br />3.1.&#xC815;&#xC758;-&#xC5F0;&#xACB0; &#xB9AC;&#xC2A4;&#xD2B8;&#xB294;
          &#xC77C;&#xC815;&#xD55C; &#xC21C;&#xC11C;&#xB97C; &#xAC00;&#xC9C0;&#xB294;
          &#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xB4E4;&#xC744; &#xD45C;&#xD604;&#xD558;&#xB294;
          &#xBC29;&#xBC95;&#xC911;&#xC758; &#xD558;&#xB098;&#xC774;&#xB2E4;. &#xBC30;&#xC5F4;&#xACFC;
          &#xAC19;&#xC740; &#xC21C;&#xCC28;&#xC801; &#xD45C;&#xD604; &#xBC29;&#xBC95;&#xACFC;&#xB294;
          &#xB2EC;&#xB9AC; &#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xB4E4;&#xC758;
          &#xB17C;&#xB9AC;&#xC801;&#xC778; &#xC21C;&#xC11C;&#xB9CC; &#xC720;&#xC9C0;&#xB418;&#xACE0;
          &#xAE30;&#xC5B5;&#xC7A5;&#xC18C;&#xB0B4;&#xC5D0;&#xC11C;&#xB294; &#xAC01;
          &#xD56D;&#xBAA9;&#xB4E4;&#xC758; &#xC784;&#xC758;&#xC758; &#xC704;&#xCE58;&#xB97C;
          &#xAC00;&#xC9C0;&#xB3C4;&#xB85D; &#xD558;&#xB294; &#xC790;&#xB8CC;&#xAD6C;&#xC870;&#xC774;&#xB2E4;.
          <br
          />3.2.&#xAD6C;&#xC870;-&#xC5F0;&#xACB0; &#xB9AC;&#xC2A4;&#xD2B8;&#xC5D0;&#xC11C;
          &#xD558;&#xB098;&#xC758; &#xB370;&#xC774;&#xD0C0; &#xD56D;&#xBAA9;&#xC744;
          &#xC800;&#xC7A5;&#xD558;&#xB294; &#xB2E8;&#xC704;&#xB97C; &#xB178;&#xB4DC;(node)&#xB77C;&#xACE0;
          &#xD55C;&#xB2E4;. &#xD558;&#xB098;&#xC758; &#xB178;&#xB4DC;&#xB294; &#xB370;&#xC774;&#xD0C0;
          &#xAC12;&#xACFC;, &#xB2E4;&#xC74C; &#xD56D;&#xBAA9;&#xC774;&#xB098; &#xC774;&#xC804;
          &#xD56D;&#xBAA9;&#xC744; &#xAC00;&#xB9AC;&#xD0A4;&#xB294; &#xD3EC;&#xC778;&#xD130;&#xB85C;
          &#xAD6C;&#xC131;&#xB41C;&#xB2E4;.
          <br />4.&#xD2B8;&#xB9AC;
          <br />4.1.&#xC815;&#xC758;-&#xB300;&#xC0C1; &#xC815;&#xBCF4;&#xB97C; &#xACC4;&#xCE35;&#xC801;&#xC73C;&#xB85C;
          &#xAD6C;&#xC870;&#xD654;&#xC2DC;&#xD0A4;&#xACE0;&#xC790; &#xD560; &#xB54C;
          &#xC0AC;&#xC6A9;&#xD558;&#xB294; &#xC790;&#xB8CC;&#xAD6C;&#xC870;&#xAC00;
          &quot;&#xD2B8;&#xB9AC;&quot; &#xC774;&#xB2E4;.
          <br />4.2.&#xAD6C;&#xC870;
          <br />-&#xD2B8;&#xB9AC;&#xC5D0;&#xB294; &#xD558;&#xB098;&#xC758; &#xB8E8;&#xD2B8;(root)
          &#xB178;&#xB4DC;&#xAC00; &#xC788;&#xB2E4;.
          <br />-&#xB8E8;&#xD2B8;&#xB97C; &#xC81C;&#xC678;&#xD55C; &#xB098;&#xBA38;&#xC9C0;
          &#xB178;&#xB4DC;&#xB4E4;&#xC740; &#xC11C;&#xB85C; &#xC911;&#xBCF5;&#xB418;&#xC9C0;
          &#xC54A;&#xB294; &#xC5EC;&#xB7EC; &#xAC1C;&#xC758; &#xB178;&#xB4DC; &#xC9D1;&#xD569;&#xC73C;&#xB85C;
          &#xB098;&#xB258;&#xC5B4;&#xC9C4;&#xB2E4;.
          <br />-&#xAC01;&#xAC01;&#xC758; &#xB178;&#xB4DC; &#xC9D1;&#xD569;&#xB4E4;&#xC740;
          &#xC5ED;&#xC2DC; &#xD2B8;&#xB9AC;&#xAC00; &#xB41C;&#xB2E4;.
          <br />5.&#xD574;&#xC2F1;
          <br />5.1.&#xC815;&#xC758;-&#xC5EC;&#xB7EC;&#xAC1C;&#xC758; &#xBA85;&#xCE6D;(identifier)&#xB4E4;&#xC774;
          &#xBB34;&#xC791;&#xC704;&#xB85C; &#xB4E4;&#xC5B4;&#xC788;&#xB294; &#xD14C;&#xC774;&#xBE14;&#xC5D0;&#xC11C;
          &#xD2B9;&#xC815; &#xBA85;&#xCE6D;&#xC744; &#xCC3E;&#xACE0;&#xC790; &#xD558;&#xB294;
          &#xACBD;&#xC6B0;&#xC5D0; &#xC6D0;&#xD558;&#xB294; &#xD0A4;&#xAC12;&#xC744;
          &#xAC00;&#xC9C0;&#xB294; &#xD14C;&#xC774;&#xBE14; &#xD56D;&#xBAA9;&#xC744;
          &#xAC80;&#xC0C9;&#xD558;&#xAE30; &#xC704;&#xD574; &#xD2B9;&#xC815;&#xD55C;
          &#xBCC0;&#xD658; &#xD568;&#xC218;&#xB97C; &#xC774;&#xC6A9;&#xD558;&#xC5EC;
          &#xD0A4;&#xAC12;&#xC744; &#xD56D;&#xBAA9;&#xC758; &#xC8FC;&#xC18C;&#xB85C;
          &#xC9C1;&#xC811; &#xBC14;&#xAFD4;&#xC11C; &#xAC80;&#xC0C9;&#xD558;&#xB294;
          &#xBC29;&#xBC95;&#xC774;&#xB2E4;.
          <br />5.2.&#xC815;&#xC801;&#xD574;&#xC2F1;
          <br />-&#xC870;&#xD569; &#xAC00;&#xB2A5;&#xD55C; &#xBA85;&#xCE6D;&#xB4E4; &#xC911;&#xC5D0;
          &#xC2E4;&#xC81C;&#xB85C; &#xC874;&#xC7AC;&#xD558;&#xB294; &#xBA85;&#xCE6D;&#xB4E4;&#xC758;
          &#xC218;&#xB294; &#xB9E4;&#xC6B0; &#xC801;&#xAE30; &#xB54C;&#xBB38;&#xC5D0;
          &#xB300;&#xBD80;&#xBD84;&#xC758; &#xACF5;&#xAC04;&#xC740; &#xB0AD;&#xBE44;&#xB41C;&#xB2E4;.
          <br
          />-&#xBA85;&#xCE6D; &#xD14C;&#xC774;&#xBE14;&#xC758; &#xAE30;&#xC5B5;&#xACF5;&#xAC04;
          &#xB0AD;&#xBE44;&#xB97C; &#xB9C9;&#xAE30; &#xC704;&#xD574; &#xD574;&#xC2DC;
          &#xD14C;&#xC774;&#xBE14;&#xC744; &#xC0AC;&#xC6A9;&#xD55C;&#xB2E4;.
          <br />-&#xD574;&#xC2DC; &#xD14C;&#xC774;&#xBE14;&#xC740; b&#xAC1C;&#xC758; &#xBC84;&#xCF13;(bucket)&#xC73C;&#xB85C;
          &#xAD6C;&#xC131;&#xB418;&#xACE0;, &#xD558;&#xB098;&#xC758; &#xBC84;&#xCF13;&#xC740;
          s&#xAC1C;&#xC758; &#xC2AC;&#xB86F;(slot)&#xC73C;&#xB85C; &#xAD6C;&#xC131;&#xB41C;&#xB2E4;.
          &#xAC01;&#xAC01;&#xC758; &#xC2AC;&#xB86F;&#xC5D0;&#xB294; &#xBA85;&#xCE6D;
          &#xD14C;&#xC774;&#xBE14; &#xD56D;&#xBAA9;&#xCC98;&#xB7FC; &#xD558;&#xB098;&#xC758;
          &#xBA85;&#xCE6D;&#xC774; &#xC800;&#xC7A5;&#xB41C;&#xB2E4;.
          <br />5.3.&#xB3D9;&#xC801;&#xD574;&#xC2F1;
          <br />-&#xD56D;&#xBAA9;&#xACFC; &#xC0BD;&#xC785;&#xACFC; &#xC0AD;&#xC81C;&#xAC00;
          &#xBE48;&#xBC88;&#xD788; &#xBC1C;&#xC0DD;&#xD558;&#xB294; &#xC751;&#xC6A9;&#xC5D0;&#xB294;
          &#xC815;&#xC801; &#xD574;&#xC281;&#xC774; &#xC801;&#xD569;&#xCE58; &#xC801;&#xD569;&#xCE58;
          &#xBABB;&#xD558;&#xB2E4;. &#xACE0;&#xC815;&#xB41C; &#xD06C;&#xAE30;&#xC758;
          &#xD574;&#xC2DC; &#xD14C;&#xC774;&#xBE14;&#xC744; &#xC0AC;&#xC6A9;&#xD558;&#xB294;
          &#xC815;&#xC801; &#xD574;&#xC2F1;&#xC758; &#xACBD;&#xC6B0;, &#xC0BD;&#xC785;&#xC774;
          &#xB9CE;&#xC544;&#xC9C0;&#xBA74; &#xD14C;&#xC774;&#xBE14;&#xC774; &#xAC00;&#xB4DD;&#xCC28;&#xC11C;
          &#xC0AC;&#xC6A9;&#xC774; &#xBD88;&#xAC00;&#xB2A5;&#xD558;&#xACE0; &#xC0AD;&#xC81C;&#xAC00;
          &#xB9CE;&#xC544;&#xC9C0;&#xBA74; &#xB9CE;&#xC740; &#xACF5;&#xAC04;&#xC774;
          &#xC0AC;&#xC6A9;&#xB418;&#xC9C0; &#xC54A;&#xC73C;&#xBBC0;&#xB85C; &#xB0AD;&#xBE44;&#xAC00;
          &#xBC1C;&#xC0DD;&#xD55C;&#xB2E4;. &#xC774;&#xB7EC;&#xD55C; &#xC751;&#xC6A9;&#xC5D0;
          &#xC801;&#xD569;&#xD558;&#xB3C4;&#xB85D; &#xACE0;&#xC548;&#xB41C; &#xAC83;&#xC774;
          &#xB3D9;&#xC801; &#xD574;&#xC2F1;(dynamic hashing) &#xB610;&#xB294; &#xD655;&#xC7A5;&#xC131;
          &#xD574;&#xC2F1;(extendible hashing)&#xC774;&#xB2E4;.
          <br />-&#xB3D9;&#xC801; &#xD574;&#xC2F1;&#xC744; &#xC704;&#xD574;&#xC11C; &#xD574;&#xC2DC;&#xD14C;&#xC774;&#xBE14;
          &#xB300;&#xC2E0;&#xC5D0; &#xD2B8;&#xB77C;&#xC774;(trie)&#xB77C;&#xB294;
          &#xC790;&#xB8CC;&#xAD6C;&#xC870;&#xB97C; &#xC774;&#xC6A9;&#xD55C;&#xB2E4;.</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>