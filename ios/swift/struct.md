# struct
- 변수들을 `property`라 함.
- 함수들을 `method`
- 값 타입
- 대부분의 타입은 구조체로 이루어져 있음.

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

