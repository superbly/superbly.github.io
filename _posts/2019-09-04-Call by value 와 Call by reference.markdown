---
layout: post
title:  "Call by value, Call by reference?"
date:   2019-09-04 16:56:00
categories: java
tags: java
mathjax: true
---

* content
{:toc}

### Call by value
* 메소드 호출 시에 사용되는 인자의 메모리에 저장되어 있는 값(value)을 복사하여 보낸다.
* 예를 들어 `int a = 3`이라는 문구가 있으면 메소드에서 인자값을 받을 때 a 자체의 주소를 받는게 아니라 a의 값인 3을 받아 처리하는 방식이다.

### Call by reference
* 메소드 호출 시에사용되는 메모리에 저장되어있는 주소(Address)를 복사하여 보낸다.
* 값이 아니라 인자 그 자체에 주소 값을 보낸다.  


---
자바에서 C언어와 같은 포인터는 존재 하지 않는다. 즉 직접 메모리에 접근하는 것은 불가하다

그러나, 동작 자체는 C의 포인터와 유사하게 동작하는 변수들이 있는 이를 reference 변수라 하며,

대표적으로 배열(Array)와 클래스(Class)들이 있다.

자바에서 메소드를 호출시 기본형(Primitive type)을 넘겨주면 Call by value 이며,

reference 변수를 메소드로 주고 받을때는 Call by Reference가 발생한다.  

여기 간단한 예제가 있다.
```java
public class ReferenceCall {

    public static void main(String[] args) {

        //   Call by Value : 값에 의한 호출
        //   메소드 호출하는측의 원본은 변화가 없다.
        //   자바에선 일반적인 primitive 변수를 매개변수로 주고 받을때
        //   Call by value 가 발생한다.

        System.out.println("== Call by Value : 값에 의한 호출 ==");
        int n = 100;
        add(n);
        System.out.println("메소드 add(int) 호출후 원본값: " + n);
        System.out.println();

        //   Call by Reference : 참조에 의한 호출
        //   메소드 호출하는측의 원본에 영향을 받는다 (원본값의 변화 발생)
        //   자바에선 일반적인 reference 변수를 주고 받을때
        //   Call by value 가 발생한다.
        //   자바의 대표적인 reference 변수 2가지 : 배열, 클래스

        System.out.println("== Call by Reference : 참조에 의한 호출 ==");
        int[] array = {1, 2, 3, 4, 5};
        add(array);        // 배열이름을 매개변수로 넘김은 Call by Reference 이다
        System.out.print("메소드 add(int []) 호출후 원본값: ");
        for (int i = 0; i < array.length; i++) {
            System.out.print(array[i] + " ");
        }
        System.out.println();
        System.out.println();

        Numeric numericObj = new Numeric();
        numericObj.num = 100;
        add(numericObj);
        System.out.println("메소드 add(Numeric) 호출후 원본값: " + numericObj.num);
        System.out.println();


        // 그러나!
        // 레퍼런스 변수가 아닌 그 '값'을 매개변수로 넘긴 경우는
        // Call by Reference 가 아닌 Call by Value 이다
        System.out.println("== '레퍼런스 변수'가 아닌 '레퍼런스의 값'을 매개변수로 호출한 경우 ==");

        add(array[0]);
        System.out.println("메소드 add(int) 호출후 원본값: " + array[0]);
        System.out.println();

        add(numericObj.num);
        System.out.println("메소드 add(int) 호출후 원본값: " + numericObj.num);
        System.out.println();

    } // end main()


    public static void add(int intArg) {
        intArg = intArg + 1;
        System.out.println("메소드 add(int) 결과: " + intArg);
    } // end add()

    public static void add(int[] arrArg) {
        System.out.print("메소드 add(int []) 결과: ");
        for (int i = 0; i < arrArg.length; i++) {
            arrArg[i] = arrArg[i] + 1;
            System.out.print(arrArg[i] + " ");
        }
        System.out.println();
    } // end add()

    public static void add(Numeric numericArg) {
        numericArg.num += 1;
        System.out.println("메소드 add(Numeric) 결과: " + numericArg.num);
    } // end add()
} // end class


class Numeric {
    public int num;
} // end class Numeric

```


위 코드 실행 결과  

![trace](/img/result.png)





---



## 참고  

* [자바에서 Call by value, Call by Reference](https://bitsoul.tistory.com/8)
* [자바의 아규먼트 전달 방식](https://brunch.co.kr/@kd4/2)  
