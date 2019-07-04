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

스택트레이스를 읽고 문제를 해결하는 능력은 생산성을 엄청나게 늘려준다는 것을 알게되었다.

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


















## 마크다운 사용법    
## 텍스트    
기본텍스트 : 기본텍스트  
하이라이트 : `하이라이트`  

## 링크    
나의 [페이스북][facebook] 바로 가기.  
페이스북 텍스트를 클릭하면 페이스북 주소와 바로 연결된다.  

[facebook]: http://facebook.com/seob3126

## 코드   
```java
String text = "Hello Seob";

System.out.println(text);
```
---
