2021.6.22

[문제 링크]()

### [문제 설명]
어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.    
예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.    
문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.


### [제한 조건]
- number는 1자리 이상, 1,000,000자리 이하인 숫자입니다.
- k는 1 이상 number의 자릿수 미만인 자연수입니다.


### [입출력 예]
|number|	k|	return|
|---|---|---|
|"1924"	|2|	"94"|
|"1231234"	|3	|"3234"|
|"4177252841"|	4|	"775841"|

<br>

# 처음 제출한 코드
```swift
import Foundation

func solution(_ number:String, _ k:Int) -> String {
    let combinationCount = number.count - k
    var currentString = ""
    var combinationArray = [String]()
    
    func makeCombination(start: Int, end: Int) {
        for i in start ... end {
            let char = number[number.index(number.startIndex, offsetBy: i)]
            currentString += String(char)
            
            if currentString.count == combinationCount {
                combinationArray.append(currentString)
            } else {
                makeCombination(start: i + 1, end: end + 1)
            }
            
            currentString.removeLast()
        }
    }
    
    makeCombination(start: 0, end: number.count - combinationCount)
    
    return String(combinationArray.map { Int($0)! }.max()!)
}


```

![image](https://user-images.githubusercontent.com/73867548/122878637-ef552800-d372-11eb-8f1e-ae2a3ad5c1c8.jpeg)

- 음.. 다른 풀이를 생각해보자. 