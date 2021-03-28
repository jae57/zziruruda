---
layout: post
title: SplitViewController 알아보기
date: 2021-02-12 02:12:35 +0900
image: '/images/11(iOS).png'
tags: Study
featured: false
---
### UISplitViewController

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0d5331e8-38ff-4dbe-8355-ae32818ff871/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0d5331e8-38ff-4dbe-8355-ae32818ff871/Untitled.png)

공식문서 📑

[https://developer.apple.com/documentation/uikit/uisplitviewcontroller](https://developer.apple.com/documentation/uikit/uisplitviewcontroller)

Split View Controller 는 navigation stack에 push 할 수 없다. 다른 view controller 의 child로 install 될 수는 있지만 이것 역시 대부분의 경우 추천하지 않음.

- iOS 14 이후로 column-style 레이아웃을 지원한다. iOS 14 이전에는 Double Column 만 지원했다.
init(stye: .doubleColumn) : 두 개의 child view controllers 를 관리하고, primary 와 secondary columns 에 위치한다.
init(style: .tripleColumn) : 세 개의 child view controllers 를 관리하고, primary, supplementary 그리고 secondary columns 에 위치한다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/94389b30-36aa-4a62-8d26-28c53a5c0e54/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/94389b30-36aa-4a62-8d26-28c53a5c0e54/Untitled.png)

기본으로 navi감싸져있고 접근에 관해서 정리왜 안해써!

스토리보드 같은데 보면 restore identifier 같은게 있는데 이게 다 복구 시에 쓰이는 id 라고 봐도 될지?

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5592c639-407f-45dd-b1c4-0c24b933a748/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5592c639-407f-45dd-b1c4-0c24b933a748/Untitled.png)