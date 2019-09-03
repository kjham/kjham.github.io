---
layout: post
title: 'Java의 객체 생성과 파괴 (작성중)'
author: kjham.ham
date: 2019-09-03 00:00
tags: [swtech,java,effectivejava]
---

다음 사항을 관리하는 방법에 대해 설명합니다.  
+ 객체를 만들어야 할 때와 만들지 말아야 할 때를 구분하는 방법  
+ 올바른 객체 생성 방법과 불필요한 생성을 피하는 방법  
+ 제때 파괴됨을 보장하고 파괴 전에 수행해야 할 정리 작업

# 생성자 대신 정적 팩터리 메서드를 고려하라  

클래스는 클라이언트에 public 생성자 대신 정직 팩토리 메서드를 제공할 수 있다.  
장점은 다음과 같다.  

## 1. 이름을 가질 수 있다.  
`BigInteger(int, int, Random)`와 `BigInteger.probablePrime` 중 `값이 소수인 BigInteger를 반환`의 의미를 더 갖고 있는가 ?  
클래스를 설명하는 문서를 참고하지 않다고 쉽게 의미부여를 할 수 있다.  

## 2. 호출될 때마다 인스턴스를 새로 생성하지는 않아도 된다.  
인스턴스를 미리 만들거나 새로 생성한 인스턴스를 캐싱하여 재활용하는 식의 불필요한 객체 생성을 피할 수 있다.  
`플라이웨이트 패턴(Flyweight Pattern)`도 이와 비슷한 기법이라 할 수 있다.  
언제 어느 인스턴스가 살아있게 하는지 통제가 가능하며 `인스턴스 통제 클래스`라 부른다.  
인스턴스를 통제하면 `싱글턴`으로 만들 수 있고, `인스턴스화 불가`로도 만들 수 있다.  
또한 불변 값 클래스에서 동치인 인스턴스가 단 하나뿐임을 보장할 수 있다.  
