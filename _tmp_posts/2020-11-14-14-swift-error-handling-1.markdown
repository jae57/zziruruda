---
layout: post
title: Swift 로 에러 핸들링을 해보자
date: 2020-11-14 14:29:55 +0900
image: '/images/1.jpg'
tags: Study
featured: true
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




guard 문으로 내가 의도한 정상적인 동작이 아닌 경우 else 로 빼서 return 시켜버리는데
이때 사용자에게 어떤 에러가 발생하여 프로그램이 종료된 건지 알리거나 어떤 동작을 해주는 등 
에러핸들링이 필요하다

[Swift 공식문서] Error Handling
https://docs.swift.org/swift-book/LanguageGuide/ErrorHandling.html

### 에러의 표현
Swift 에서 에러는 Error 프로토콜을 준수하는 타입의 값으로 표현된다
{% highlight swift %}
struct MyError: Error {
    var x: Int
    var y: Int
    var z: Int
}
{% endhighlight %}

### 에러의 그룹화
Swift 의 열거형을 활용하면 
에러를 그룹화(Grouping)할 수 있고, 추가적인 정보도 제공해줄 수 있다.

{% highlight swift %}
enum TestError : Error {
    case outOfRange
    case invalidInput(testNum: Int)
}

enum VendingMachineError: Error {
    case invalidSelection // 유효하지 않은 선택
    case insufficientFunds(coinsNeeded: Int) // 자금 부족 - 필요한 동전 개수
    case outOfStock // 품절
}
{% endhighlight %}


{% highlight swift %}
enum TestError : Error {
    case outOfRange
    case invalidInput(testNum: Int)
}
{% endhighlight %}

### 에러의 발생
예상치 못한 동작이 발생하거나 일반적인 실행흐름이 계속될 수 없다고 판단되면
throw 문을 이용해 에러를 발생시킨다.

### 에러의 처리
에러가 발생했을 때, 적절히 에러를 처리해줘야하는 경우가 있다
문제를 해결하거나, 다른 대안을 시도하도록 유도하거나, 사용자에게 실패를 알리는 등 에러가 발생했을 때의 핸들링을 해줘야한다

Swift 에는 에러를 처리하는 4가지 방법이 있다
1. 함수에서 발생한 오류를 해당 함수를 호출한 코드에 알리기 (throw, throws)
2. do-catch 구문을 이용하여 오류를 처리하기 (try)
3. 옵셔널 값으로 오류를 처리하기 (try?)
4. 오류가 발생하지 않을 것이라고 확신하기 (try!)

에러 던지고 처리하기

던지기
{% highlight swift %}
class MyObject {
    func printNumber(_ number: Int) throws -> Int { // 오류 발생 가능성이 있는 메서드 제목 옆에 throws
        var text = ""
        guard number > 0 else { 
            throw TestError.outOfRange // 오류가 발생하는 구간에 throw
        }
        return text
    }
}
{% endhighlight %}

던진 에러 처리하기
에러 메시지 출력 #1
{% highlight swift %}
let myObject = MyObject()
do {
    let resultNumber = try myObject.printNumber(-20) // 오류가 발생하는 메서드를 호출할 때는 반드시 try를 써줍니다
    // 오류가 발생할 수 있는 메서드를 한번 호출해보겠다는 선언!
}
{% endhighlight %}

에러 메시지 출력 #2
{% highlight swift %}
let myObject = MyObject()
do {
    let resultNumber = try myObject.printNumber(-20) // 오류가 발생하는 메서드를 호출할 때는 try를 써줍니다
    // 오류가 발생할 수 있는 메서드를 한번 호출해보겠다는 선언!
} catch { // 실제로 오류가 발생하면 처리
    print(error)
}
{% endhighlight %}

=> 똑같이 동작함

에러를 특정지어서 처리 #1
{% highlight swift %}
let myObject = MyObject()
do {
    let resultNumber = try myObject.printNumber(-20) // 오류가 발생하는 메서드를 호출할 때는 try를 써줍니다
    // 오류가 발생할 수 있는 메서드를 한번 호출해보겠다는 선언!
} catch { // 실제로 오류가 발생하면 처리
    print(error)
} catch TestError.outOfRange { // 에러를 특정지어 처리해줄 수도 있습니다
    print("양수가 아님!")
}
{% endhighlight %}

에러를 특정지어서 처리 #2 - switch 문 활용
{% highlight swift %}
let myObject = MyObject()
do {
    let resultNumber = try myObject.printNumber(-20) // 오류가 발생하는 메서드를 호출할 때는 try를 써줍니다
    // 오류가 발생할 수 있는 메서드를 한번 호출해보겠다는 선언!
} catch { // 실제로 오류가 발생하면 처리
    switch error {
        case TestError.outOfRange:
            print("ㅇㅇㅇ")
        case TestError.invalidInput(let number):
            print("ssss")
    }
}
{% endhighlight %}



try는 try? try! 로도 쓸수 있다
try? 를 쓰게되면 오류 발생시 nil 이 리턴되고 지나감
try! 를 쓰게되면 오류 발생시 Runtime Error 를 뿜고 강제종료됨

{% highlight swift %}
let myObject = MyObject()
let resultNumber = try? myObject.printNumber(-20) // resultNumber 는 옵셔널 타입
let resultNumber = try! myObject.printNumber(-20)
{% endhighlight %}

{% highlight swift %}
let myObject = MyObject()
let resultNumber = try? myObject.printNumber(-20) // resultNumber 는 옵셔널 타입
let resultNumber = try! myObject.printNumber(-20)
{% endhighlight %}

++ rethrows 라는 것도 있음
자신의 매개변수로 전달받은 함수가 오류를 던지는 경우,
rethrows 를 통해 다시 던질 수 있다

{% highlight swift %}
func someThrowingFunction() throws {
    enum SomeError: Error {
        case justSomeError
    }

    throw SomeError.justSomeError
}

func someFunction(callback: () throws -> Void) rethrows {
    try callback()
}

do {
    try someFunction(callback: someThrowingFunction)
} catch {
    print(error)
}
{% endhighlight %}

rethrows 키워드를 사용한 함수는 스스로 오류를 던지지 못함
즉, 자신 내부에 직접적으로 throw 구문을 사용할 수 없음
그러나 내부에 do-catch문이 있다면 해당 catch문 안에서는 throw 구문 사용가능

++ defer
defer 구문은 현재 코드 블록을 나가기 전에 꼭 실행해야할 코드를 작성해 줄 수 있는 문법인데
오류가 발생하여 코드 블록을 빠져나갈 때도 defer 구문은 반드시 실행된다

예를 들면, 파일을 읽으려다가 에러발생시 파일을 정상적으로 닫아주어 메모리에서 해제해주는 작업등을 
defer 구문에 넣어줄 수 있다

( 참고, defer 문은 스택구조처럼 실행이 되어서 나중에 작성한 것(-같은 뎁스에서)이 가장 먼저 실행된다 )

### 참고

https://medium.com/@twih1203/swift-%EC%98%88%EC%99%B8%EC%B2%98%EB%A6%AC-throws-do-catch-try-%ED%95%98%EA%B8%B0-c0f320e61f62

