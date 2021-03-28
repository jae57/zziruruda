---
layout: post
title: 숫자 세자리 수 마다 콤마 넣어서 가격 표시하기
date: 2021-02-04 03:27:55 +0900
image: "/images/11(iOS).png"
tags: Post iOS Int Extension
featured: false
---

해결법1
{% highlight swift %}
   extension Int {
    func withCommas() -> String {
        let numberFormatter: NumberFormatter = NumberFormatter()
        numberFormatter.numberStyle = .decimal
        return numberFormatter.string(from: NSNumber(value: self))!
    }
  }
{% endhighlight %}

해결법2
{% highlight swift %}
extension NumberFormatter {
    static let withComma: NumberFormatter = {
        let formatter = NumberFormatter()
        formatter.numberStyle = .decimal
        return formatter
    }()
}
{% endhighlight %}

해결법2 의 사용 례
{% highlight swift %}
private func updateScore() {
    guard let scoreString = NumberFormatter.withComma.string(from: NSNumber(value: score)) else {
        return
    }
    scoreLabel.text = "\(scoreString)점"
}
{% endhighlight %}