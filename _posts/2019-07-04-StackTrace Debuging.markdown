---
layout: post
title:  "스택트레이스로 디버깅하기"
date:   2019-07-04 15:00:00
categories: Debug
tags: StackTrace
mathjax: true
---

* content
{:toc}

## 스택트레이스로 디버깅하기  
처음 자바를 접할 때 에러가 발생하면 여러줄의 트레이스를 읽으려 하지않고 그저 복사해서 구글에 붙혀넣어서 문제를 해결하려고 하였고 구글로도 어렵다고
느낄 때에는 여러 개발자 커뮤니티에 수많은 질문을 올렸었다.

하지만 의미없는 질문과 검색의 비용은 생각보다 높다.

- 남들이 이해할 수 있도록 질문글을 작성하는데 시간이 오래 걸린다.
- 답변이 달릴 때까지의 시간이 오래 걸린다.
- 똑같은 문제가 발생했을 경우 같은 실수를 반복한다.

`스택트레이스를 읽고 문제를 해결하는 능력은 생산성을 엄청나게 늘려준다는 것을 알게되었다.`

---
```java
public class StackTraceTest
{
    public static void main(String[] args) {
        one();
    }

    public static void one() {
        two();
    }

    public static void two() {
        three();
    }

    public static void three() {
        Integer.parseInt("superbly");
    }
}
```
위 코드의 스택트레이스
![ex_screenshot](/img/trace.png)

Exception in thread "쓰레드이름" 예외클래스경로.예외클래스이름 : 예외 메시지

at 예외발생한클래스경로.클래스이름.메소드이름(클래스이름 : 예외발생한라인번호)

스택트레이스는 이렇게 구성되어 있다.

또한 잘 살펴보면

at ... three()

at ... two()

at ... one()

at ... main() 이렇게 되어있는 부분이 있는데

이것은 메소드를 호출한 순서에 따라 스택트레이스가 찍힌다는 뜻이다.

---
### 스택트레이스 읽는 순서  

Exception in thread "main" java.lang.`NumberFormatException: For input string: "superbly"`  
	at java.base/java.lang.NumberFormatException.forInputString(NumberFormatException.java:65)  
	at java.base/java.lang.Integer.parseInt(Integer.java:652)  
	at java.base/java.lang.Integer.parseInt(Integer.java:770)  
	at StackTraceTest.three(StackTraceTest.java:22)  
	at StackTraceTest.two(StackTraceTest.java:17)  
	at StackTraceTest.one(StackTraceTest.java:12)  
	at StackTraceTest.main(StackTraceTest.java:7)  

1. 예외메시지
    - 클래스를 만들 때 예외를 쉽게 찾을 수 있도록 예외메시지에서 명확하게 에러상황을 설명해줄때가 많기 때문에 예외메시지만 보고서 에러를 해결하는 경우가 많다.
    - ex) Exception in thread "main" java.lang.`NumberFormatException: For input string: "superbly"`  
    - 그 다음으로 `java.lang.NumberFormatException` 이 클래스가 무슨 클래스이며 어떤 경우에 이러한 예외가 발생하는지 알아 볼 필요가 있다.  

2. 예외 클래스  


---
















### 참고  
[신입개발자가 혼자 공부하는 방법]: https://okky.kr/article/597494
