---
layout: post
title: UILabel 에 취소선 스타일 적용하기
date: 2021-01-15 18:29:55 +0900
image: "/images/11(iOS).png"
tags: Post iOS Label Style
featured: false
---

<p align="center">
  <img src="/images/12-1.png">
</p>

> **취소선(strikeout, strikethrough)**은 글자 중앙에 수평선이 있는 타이포그래피적인 표현
주로 실수했거나 제거할 문자를 표시하기 위해 사용된다. - 위키백과

{% highlight swift %}
   @IBOutlet weak var taskLabel: UILabel!

   taskLabel.attributedText = NSAttributedString(string: "취소선이 적용된 문자열",
        attributes: [.strikethroughStyle: 1])
{% endhighlight %}
