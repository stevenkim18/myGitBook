# optional

# 옵셔널
## 정의
값이 있을 수도 있고 없을 수도 있음.

## 옵셔널은 왜 있을까?
- nil의 가능성을 명시적으로 표현하기 위해서
- 다른 언어(대표적으로 c 계열 )에서는 일반 변수에도 `null` 이 들어수 있음.
    - 그 변수를 참조하려고 하면 오류가 발생하는데
    - swift는 옵셔널을 만들어서 미연에 방지하고자 하기 위함.

## 기본 선언
- 기본 형식은
```swift
let optionlValue: Optional<Int> = nil
```
- 하지만 거의 줄여서 변수 뒤에`?`사용
```swift
let optionalValue: Int? = nil
```

## 암시적 추출 옵셔널
- 변수 뒤에 `!` 를 붙여서 선언
```swift
var optionalValue: Int! = 100
```
- 기본 변수처럼 사용 가능
- `nil`이 그 옵셔널을 접근하려고 하면 오류 발생
```swift
optionalValue = nil

// 오류!
optionalValue = optionalValue + 1
```

## 일반 옵셔널
- 일반 변수 처럼 사용 불가

# Optional Unwrapping
- 옵셔널의 값을 추출함.
- 여러가지 방법이 있음.

## 옵셔널 바인딩
- nil을 채크하고 안전하게 추출하는 방법

### if-let
```swift
var myName: String? = nil

if let name: String = myName {
    print(name)
}
else {
    print("nil")
}

```
- `if-let` 을 사용해서 옵셔널이 `nil`인지 아닌지를 확인하고 `nil`이 아니면 그 값을 사용.

```swift
if let name = myName, let friend = yourName {
    print("both name not nil")
}
```
- 여러개의 옵셔널을 확인 가능
- 모두 `nil` 아니여야 사용 가능

## 옵셔널 강제추출
```swift
var optionalValue: Int? = 100

print(optionalValue!)

optionalValue = nil

// error!
print(optionalValue!)
```
- 일반 옵셔널을 `!` 를 사용해서 강제 추출 할 수 있음
    - 그 대신 `nil` 값일 때는 에러 발생 가능
- 처음 부터 선언을 `!`로 해도 되지만
    - 역시 `nil`이 들어 있을 때는 에러 발생
    - 그래서 강제 추출을 하지 않는 것이 좋음.

# 참고
## 옵셔널 개녕을 정리 잘한 글
https://zeddios.tistory.com/16