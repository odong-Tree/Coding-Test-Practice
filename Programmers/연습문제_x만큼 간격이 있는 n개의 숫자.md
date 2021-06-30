210630

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12954)

### [문제 설명]

함수 solution은 정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴해야 합니다. 다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해주세요.

### [제한 조건]
- x는 -10000000 이상, 10000000 이하인 정수입니다.
- n은 1000 이하인 자연수입니다.

### [입출력 예]
|x	|n	|answer|
|---|---|---|
|2|	5	|[2,4,6,8,10]|
|4	|3	|[4,8,12]|
|-4|	2|	[-4, -8]|

<br>

# 제출한 코드 
```swift
func solution(_ x:Int, _ n:Int) -> [Int64] {
    var answer = [Int64]()
    
    for i in 1 ... n {
        answer.append(Int64(x * i))
    }
    
    return answer
}
```

<br>

# 다른 사람이 제출한 코드
```swift
func solution(_ x:Int, _ n:Int) -> [Int64] {
    return Array(1...n).map { Int64($0 * x) }
}

```