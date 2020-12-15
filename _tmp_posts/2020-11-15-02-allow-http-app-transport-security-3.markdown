---
layout: post
title: URL 이동 안될 때
date: 2020-11-15 02:29:55 +0900
image: '/images/3.jpg'
tags: Blog
featured: false
---

guard 문으로 내가 의도한 정상적인 동작이 아닌 경우 else 로 빼서 return 시켜버리는데
이때 사용자에게 어떤 에러가 발생하여 프로그램이 종료된 건지 알리거나 어떤 동작을 해주는 등 
에러핸들링이 필요하다

[Swift 공식문서] Error Handling
https://docs.swift.org/swift-book/LanguageGuide/ErrorHandling.html

### 에러의 표현
Swift 에서 에러는 Error 프로토콜을 준수하는 타입의 값으로 표현된다

### 에러의 그룹화
Swift 의 열거형을 활용하면 
에러를 그룹화(Grouping)할 수 있고, 추가적인 정보도 제공해줄 수 있다.

### 에러의 발생
예상치 못한 동작이 발생하거나 일반적인 실행흐름이 계속될 수 없다고 판단되면
throw 문을 이용해 에러를 발생시킨다.

### 에러의 처리
에러가 발생했을 때, 적절히 에러를 처리해줘야하는 경우가 있다
문제를 해결하거나, 다른 대안을 시도하도록 유도하거나, 사용자에게 실패를 알리는 등 에러가 발생했을 때의 핸들링을 해줘야한다

Swift 에는 에러를 처리하는 4가지 방법이 있다


