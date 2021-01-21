# struct

* 변수들을 `property`라 함.
* 함수들을 `method`
* 값 타입
* 대부분의 타입은 구조체로 이루어져 있음.

## 예제

```swift
import UIKit

struct Sample {
    var mutableProperty: Int = 100
    let immutableProperty: Int = 100

    // 타입 프로퍼티
    static var typeProperty: Int = 100

    func instanceMethod(){
        print("i method")
    }

    static func typeMethod() {
        print("type method")
    }
}

var mutable: Sample = Sample()

mutable.mutableProperty = 200
// 프로퍼티가 let, 변경 불가능
// mutable.immutableProperty = 200

let immutable: Sample = Sample()

// 구초제 자체를 let으로 선언해서 프로퍼티 값 변경 불가능
//immutable.mutableProperty = 200
// immutable.immutableProperty = 200

// java에서 클래스 변수, 클래스 메소드를
// swift -> 타입 프로퍼티, 타입 메소드라 함.
Sample.typeProperty = 300
Sample.typeMethod()

// 인스턴스로 타입 프로퍼티 메소드 호출 불가
// mutable.typeProperty = 400
// mutable.typeMethod()
```

# class

* 참조 타입\(주소가 전달 됨\)

## 예제

```swift
import UIKit

class Sample {
    var mutableProperty: Int = 100
    let immutableProperty: Int = 100

    // 타입 프로퍼티
    static var typeProperty: Int = 100

    func instanceMethod(){
        print("i method")
    }

    // 상속시 재정의 불가
    static func typeMethod() {
        print("type method")
    }

    // 상속시 재정의 가능
    class func classMethod() {
        print("type method - class")
    }

}

var mutable: Sample = Sample()

mutable.mutableProperty = 200
// mutable.immutableProperty = 200

let immutable: Sample = Sample()

// 구조체와 다르게 인스턴스가 let으로 선언 되어도 프로퍼티 변경가능
immutable.mutableProperty = 200
// immutable.immutableProperty = 200

// java에서 클래스 변수, 클래스 메소드를
// swift -> 타입 프로퍼티, 타입 메소드라 함.
Sample.typeProperty = 300
Sample.typeMethod()

// 인스턴스로 타입 프로퍼티 메소드 호출 불가
// mutable.typeProperty = 400
// mutable.typeMethod()
```

# enum

* 다른 언어에 비해 강력한 기능들이 많음.

## 예제

```swift
import UIKit

enum Weekday {
    case mon
    case tue
    case wed
    case thu, fri, sat, sun
}

var day: Weekday = Weekday.mon
print(day)      // mon

// day 타입이 Weekday 이기 때문에 축약으로 case 만 써도 됨.
day = .tue
print(day)      // tue

// 모든 열거형이 오면 defalut를 안해줘도 됨.
switch day {
case .mon, .tue, .wed, .thu:
    print("평일")             // 출력
case Weekday.fri:
    print("불금")
case .sat, .sun:
    print("주말!")
}

// c언어 처럼 정수 값을 가질 수도 있음
enum Fruit: Int {
    case apple = 0
    case grape = 1
    case peach     // 자동으로 2가 할당 됨.
}

print("apple = \(Fruit.apple)")             // apple
// rawValue -> 원시값
print("apple = \(Fruit.apple.rawValue)")    // 0
print("grape = \(Fruit.grape.rawValue)")    // 1
print("peach = \(Fruit.peach.rawValue)")    // 2

enum School: String {
    case primary = "초딩"
    case middle = "중딩"
    case high
}

print("middle = \(School.middle.rawValue)")     // 중딩
// rawValue가 없으면 case 출력
print("high = \(School.high.rawValue)")         // high

// rawValue를 통해 초기할 수 있음.
// 옵셔널 타입이어야 함. 없을 수도 있기 때문
//let apple: Fruit = Fruit(rawValue: 0)
let apple: Fruit? = Fruit(rawValue: 0)
print(apple!.rawValue)      // 0

if let orange: Fruit = Fruit(rawValue: 5) {
    print("orange = \(orange)")
}
else {
    print("no orange")      // 출력
}

// 열거형 안에는 메서드도 추가 가능

enum AppleProduct {
    case iphone
    case ipad
    case imac
    case macbook
    case airpod

    func printKorean() {
        switch self {
        case .iphone:
            print("아이폰")
        case .ipad:
            print("아이패드")
        case .imac:
            print("아이맥")
        case .macbook:
            print("맥북")
        case .airpod:
            print("에어팟")
        }
    }
}

AppleProduct.ipad.printKorean()     // 아이패드
AppleProduct.imac.printKorean()     // 아이맥
```

# class VS struct/enum
## 차이점
- 클래스는 참조 타입이라서 메모리 주소를 전달함.
    - 단일 상속 가능
    - 애플 프레임워크 대부분은 클래스를 사용
- 구조체와 열거형은 값 타입이라서 값을 복사하여 전달함.
    - swift의 기본 자료형은 모두 구조체
    - swift는 구조체 열거형 사용을 선호
- 구조체/클래스 사용은 개발자의 선택

## 예제
```swift
import UIKit

struct ValueType {
    var property = 1
}

class ReferenceType {
    var property = 1
}

var first = ValueType()
// 새로 값이 복사 됨.
// 다른 곳을 참조하게 됨.
var second = first
second.property = 2

print(first.property)       // 1
print(second.property)      // 2

print("===================")

var third = ReferenceType()
// 주소 값이 복사가 되어 같은 곳을 참조함.
var fourth = third

fourth.property = 2

print(third.property)       // 2
print(fourth.property)      // 2
```