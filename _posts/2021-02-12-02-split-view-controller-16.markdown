---
layout: post
title: SplitViewController 알아보기
date: 2021-02-12 02:12:35 +0900
image: '/images/11(iOS).png'
tags: Study
featured: false
---

<p align="center"><img src="/images/post16/01.png"></p>

공식문서 📑 <br/>
https://developer.apple.com/documentation/uikit/uisplitviewcontroller

💡 Split View Controller 는 navigation stack에 push 할 수 없다.<br/>
다른 view controller 의 child로 install 될 수는 있지만 이것 역시 대부분의 경우 추천하지 않음.

- iOS 14 이후로 column-style 레이아웃을 지원한다. iOS 14 이전에는 Double Column 만 지원했다.

<p align="center"><img src="/images/post16/02.png"></p>

{% highlight swift %}
init(style: .doubleColumn)
두 개의 child view controllers 를 관리하고, primary 와 secondary columns 에 위치한다.

init(style: .tripleColumn)
세 개의 child view controllers 를 관리하고, 
primary, supplementary 그리고 secondary columns 에 위치한다.
{% endhighlight %}

TODO: 기본으로 navi감싸져있고 접근에 관해서 정리