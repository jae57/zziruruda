---
layout: post
title: Swift 로 에러 핸들링을 해보자
date: 2020-11-14 14:29:55 +0900
image: '/images/1.jpg'
tags: Study
featured: false
---

다양한 에러 상황에서 사용자가 불편해하지 않도록  
어떤 이유로 프로그램이 실패했는지 개발자가 파악하기 쉽도록  
각각의 에러에 대해 올바르게 대응해보자

{% highlight swift %}
    @IBAction private func moveButtonClicked(_ sender: UIButton) {
        guard let input = URLInputField.text else { return }
        guard let inputURL = URL(string: input) else { return }
        let request = URLRequest(url: inputURL)
        webView.load(request)
    }
{% endhighlight %}

> 사용자 입장에서는 버튼을 눌렀지만 이유를 모르고 아무런 동작을 하지 않는 상황을 마주했을 때 당혹스럽지 않을까요?

> guard로 안전하게 언래핑하는 것도 중요하지만 언래핑이 실패했을 때에 대한 핸들링 또한 중요합니다.
>
> 현재의 구현으로는 URL이 유효하지 않아서 실패를 한 것인지
> 인터넷 상태 때문에 로드가 제대로 안 이루어지는지에 대해 원인 파악이 어려울 것 같습니다.
