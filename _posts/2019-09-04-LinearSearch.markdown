---
layout: post
title:  "LinearSearch"
date:   2019-09-04 21:34:00
categories: DataStructure
tags: LinearSearch
mathjax: true
---

* content
{:toc}

### 선형검색(LinearSearch)
요소가 직선 모양으로 늘어선 배열에서의 검색은 원하는 키 값을 갖는요소를 만날 때까지 맨앞부터 순서대로 요소를 검색하면 되는데, 이것을 선형 검색(linear search)이라 한다.  
</hr>
---
간단히 그림으로 살펴보자.

![trace](/img/linearSearch1.png)

이 경우는 검색에 성공한 경우다.

그런데 키 값과 같은 값을 가진 요소가 배열에 없을 수도 있다.

예를 들어 앞의 배열에서 5를 검색하면 배열에 5가 없기 때문에 검색에 실패한다.

이러한 검색 과정을 나타낸 것이 아래의 그림이다.

![trace](/img/linearSearch2.png)

이처럼 검색을 끝까지 수행해도 키 값과 같은 값의 요소를 만나지 못했다.

성공의 예와 실패의 예를 보면 배열 검색의 종료 조건은 2개임을 알 수 있으며 다음 조건중 하나라도 성립하면 검색을 종료한다.

> 1. 검색할 값을 발견하지 못하고 배열의 끝을 지나간 경우
> 2. 검색할 값과 같은 요소를 발견한 경우

배열의 요솟수가 n개일 때 조건 1, 2 를 판단하는 횟수는 평균 `n / 2 회` 이다.



---  

#### 코드
```java
import java.util.Scanner;

public class LinearSearch { // 선형검색 : 배열에서 순서대로 검색하는 유일한 방법.

    // 요솟수가 n인 배열 a에서 key와 같은 요소를 선형 검색합니다.
    static int linearSearch(int[] a, int n, int key) {
        for (int i = 0; i < n; i++) {
            if (a[i] == key)
                return i;
        }
        return -1;
    }

    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        System.out.print("요솟수 : ");
        int num = input.nextInt();
        int[] x = new int[num];               // 요솟수 num

        for (int i = 0; i < num; i++) {
            System.out.print("x[" + i + "] : ");
            x[i] = input.nextInt(10);
        }

        System.out.print("검색할 값 : ");       // 키 값을 입력
        int key = input.nextInt();

        int idx = linearSearch(x, num, key);  // 배열 x에서 키 값이 key인 요소를 검색

        if (idx == -1)
            System.out.println("그 값의 요소가 없습니다.");
        else
            System.out.println(key + "은(는) x[" + idx + "]");
    }
}
```
메서드 linearSearch는 배열 a의 처음부터 끝까지 n개의 요소를 대상으로 값이 key인 요소를 선형 검색하고 검색한 요소의 인덱스를 반환한다.

또한 값이 key인 요소가 여러 개 존재할 경우 반환값은 검색 과정에서 처음 발견한 요소의 인덱스가 되며,

값이 key인 요소가 존재하지 않으면 -1을 반환한다.

---
#### 위 코드 실행 결과  

![trace](/img/linearSearchResult.png)

---
### 보초법
선형검색은 반복할 때마다 다음의 종료 조건 1과 2를 모두 판단한다.

단순한 판단이라고 생각할 수 있지만 `티끌 모아 태산`이라는 말이 있듯이 종료 조건을 검사하는 비용을 무시할 수 없다.

이러한 비용을 반으로 줄이는 방법이 `보초법(sentinel method)`이다.

다음 그림은 보초법을 이용한 선형검색을 보여준다.

![trace](/img/linearSearch3.png)

이 그림에서 배열의 요소 a[0] ~ a[6]은 초기에 준비해 놓은 데이터이다.

검색하기 전에 검색하고자 하는 키 값을 배열 맨 끝 요소 a[7]에 저장한다.

이때 저장하는 값을 `보초(sentinel)`라고 한다.

> `a` : 2를 검색하기 위해 보초로 a[7]에 2를 저장
> `b` : 5를 검색하기 위해 보초로 a[7]에 5를 저장  

- 그러면 `b`처럼 원하는 값이 원래의 데이터에 존재하지 않아도 보초인 a[7]까지 검색하면 종료 조건 2가 성립한다.
- 이렇게 하면 원하는 키값을 찾지 못했을 때를 판단하는 종료 조건 1이 필요 없어진다.

```
보초는 반복문에서 종료 판단 횟수를 2회에서 1회로 줄이는 역할을 한다.
```

이 예제를 코드에 적용 해 보자

---
#### 코드
```java
import java.util.Scanner;

public class LinearSearch { // 선형검색 : 배열에서 순서대로 검색하는 유일한 방법.

    // 요솟수가 n인 배열 a에서 key와 같은 요소를 선형 검색합니다.
    static int linearSearch(int[] a, int n, int key) {
        int i;
        a[n] = key;                          // 보초를 배열 요소의 끝에 추가
        for (i = 0; a[i] != key; i++)
            ;
        return i == n ? -1 : i;              // i == n 이면 배열의 맨끝이므} - 1을 반환
    }

    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        System.out.print("요솟수 : ");
        int num = input.nextInt();
        int[] x = new int[num + 1];               // 요솟수 num + 1 : 보초값을 넣어주기 위해서

        for (int i = 0; i < num; i++) {
            System.out.print("x[" + i + "] : ");
            x[i] = input.nextInt(10);
        }

        System.out.print("검색할 값 : ");       // 키 값을 입력
        int key = input.nextInt();

        int idx = linearSearch(x, num, key);  // 배열 x에서 키 값이 ky인 요소를 검색

        if (idx == -1)
            System.out.println("그 값의 요소가 없습니다.");
        else
            System.out.println(key + "은(는) x[" + idx + "]");
    }
}
```

---
#### 위 코드의 실행 결과
![trace](/img/linearSearchResult.png)

---
## 참고  

* [Do it! 자료구조와 함께 배우는 알고리즘 입  ]()  
