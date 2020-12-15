---
layout: post
title: Collection 의 indices 와 index(after:) 의 차이
date: 2020-11-22 16:53:55 +0900
image: '/images/6(swift).png'
tags: Post Swift
featured: false
---

Swift Collection 의 instance property 중 indices 에 대해

![indices discussion]({{site.baseurl}}/images/6-1.png)
*indices discussion* 

indices 속성은 collection 자체에 strong reference를 가질 수 있으므로
collection 의 indices를 돌면서 collection 을 수정하게 된다면, 
strong reference에 의해 예상치못한 copy 가 발생할 수 있다

{% highlight swift %}
var myCollection = [10,20,30,40,50]

// 컴파일 시에 해당 collection 에 수정이 가해지는 코드가 있다고 판단되면
// myCollection.indices 수행 시 따로 복사본으로 들고 있도록 한다는 뜻인가?
for index in myCollection.indices {
    print(index)
    myCollection[index] /= 5
    myCollection.append(myCollection[index]+100) 
    // 값을 수정하거나 요소를 추가하는 등 collection 에 변경이 생기면 예상치 못한 copy 가 일어날 수 있음
}

print(myCollection)
{% endhighlight %}

👇 실행 결과

{% highlight markdown %}
0
1
2
3
4
[2, 4, 6, 8, 10, 102, 104, 106, 108, 110]
{% endhighlight %}

따라서 의도에 맞게 쓸 수 있도록 index(after:) 속성도 제공한다

{% highlight swift %}
var myCollection = [10,20,30,40,50]
var index = myCollection.startIndex

while index != myCollection.endIndex {
    print(index)
    myCollection[index] /= 5
    myCollection.append(myCollection[index]+100)
    index = myCollection.index(after: index)
}

print(myCollection)
{% endhighlight %}

👇 실행 결과

{% highlight markdown %}
0
1
2
3
4
5
6
... 무한루프에 빠진다
{% endhighlight %}