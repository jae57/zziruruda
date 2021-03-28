---
layout: post
title: Framework
date: 2021-03-15 01:12:35 +0900
image: '/images/4.jpg'
tags: Study
featured: false
---
문서들 읽어보면 Cocoa, Cocoa Touch 도 프레임워크고, Cocoa Touch 프레임워크 내부에 속한 UIKit, Foundation 도 프레임워크라고 하네..

### Cocoa

- MacOS 에서 돌아가는 App 을 개발하기 위한 전용 프레임워크

### Cocoa Touch

- Cocoa 이후에 나온 프레임워크로 Cocoa를 본따서 만들었기 때문에 사용자의 눈에 보이는 foreground 화면을 말하는 window 개념 역시 함께 따라왔다.
- iOS 에서 돌아가는 App 을 개발하기 위한 전용 프레임워크
- iPhone, iPod Touch, iPad

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/637ad5f9-b6d1-476d-8894-85564696c004/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/637ad5f9-b6d1-476d-8894-85564696c004/Untitled.png)

### Foundation

기초 클래스를 모아두었다. 표준 값, Collection, 문자열, 유틸리티, 날짜 등의 클래스가 포함되어 있다.

### UIKit

화면 처리와 관련된 클래스가 포함되어 있다.

- Foundation 을 포함하므로 import UIKit 을 해주면 import Foundation 은 지워도 됨.