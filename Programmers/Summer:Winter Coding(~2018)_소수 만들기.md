2021.6.2

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12977)

### [문제 설명]

주어진 숫자 중 3개의 수를 더했을 때 소수가 되는 경우의 개수를 구하려고 합니다. 숫자들이 들어있는 배열 nums가 매개변수로 주어질 때, nums에 있는 숫자들 중 서로 다른 3개를 골라 더했을 때 소수가 되는 경우의 개수를 return 하도록 solution 함수를 완성해주세요.

### [제한사항]
nums에 들어있는 숫자의 개수는 3개 이상 50개 이하입니다.     
nums의 각 원소는 1 이상 1,000 이하의 자연수이며, 중복된 숫자가 들어있지 않습니다.


### [입출력]
|nums|	result|
|---|---|
|[1,2,3,4]|	1|
|[1,2,7,6,4]|	4|


#### 입출력 예 설명

```
입출력 예 #1
[1,2,4]를 이용해서 7을 만들 수 있습니다.

입출력 예 #2
[1,2,4]를 이용해서 7을 만들 수 있습니다.
[1,4,6]을 이용해서 11을 만들 수 있습니다.
[2,4,7]을 이용해서 13을 만들 수 있습니다.
[4,6,7]을 이용해서 17을 만들 수 있습니다.
```

<br>

# 처음 작성한 코드
```swift
import Foundation

func solution(_ nums:[Int]) -> Int {
    let combinationArray = makeCombination(arr: nums, count: 3)
    
    return combinationArray.filter { checkSumIsPrimeNum($0) }.count
}

func checkSumIsPrimeNum(_ nums: [Int]) -> Bool {
    let num = nums.reduce(0, +)
    
    for i in 2...Int(Double(num).squareRoot()) {
        if num % i == 0 {
            return false
        }
    }
    
    return true
}

func makeCombination(arr: [Int], count: Int) -> [[Int]] {
    var newArr = [[Int]]()
    
    for i in 0...arr.count - count {
        var a = [Int]()
        a.append(arr[i])
        
        for j in i + 1...arr.count - count + 1 {
            a.append(arr[j])
            
            for k in j + 1...arr.count - count + 2 {
                a.append(arr[k])
                newArr.append(a)
                a.remove(at: 2)
            }
            
            a.remove(at: 1)
        }
    }
    
    return newArr
}
```
- makeCombination 함수가 마음에 안든다. count가 변하더라도 동작하는 함수를 만들어 주고 싶다.

<br>

# 제출한 코드
```swift
import Foundation

func solution(_ nums:[Int]) -> Int {
    let combinationArray = makeCombination(arr: nums, count: 3)
    return combinationArray.filter { checkSumIsPrimeNum($0) }.count
}

func checkSumIsPrimeNum(_ nums: [Int]) -> Bool {
    let sum = nums.reduce(0, +)
    
    for i in 2...Int(Double(sum).squareRoot()) {
        if sum % i == 0 {
            return false
        }
    }
    
    return true
}

func makeCombination(arr: [Int], count: Int) -> [[Int]] {
    var newArr = [[Int]]()
    var a = [Int]()
    
    func makeArray(rangeStart: Int, rangeEnd: Int) {
        for i in rangeStart...rangeEnd {
            a.append(arr[i])

            if a.count == count {
                newArr.append(a)
            } else {
                makeArray(rangeStart: i + 1, rangeEnd: rangeEnd + 1)
            }
            
            a.remove(at: a.count - 1)
        }
    }

    makeArray(rangeStart: 0, rangeEnd: arr.count - count)
    return newArr
}

```
- 조합 배열을 만들지 않고도 해결할 수 있을 것 같다.

<br>

# 수정한 코드
```swift
import Foundation

func solution(_ nums:[Int]) -> Int {
    var currentArray = [Int]()
    let combinationCount = 3
    var primeCount = 0
    
    func makeArray(rangeStart: Int, rangeEnd: Int) {
        for i in rangeStart...rangeEnd {
            currentArray.append(nums[i])

            if currentArray.count == combinationCount {
                if checkIsPrime(currentArray.reduce(0, +)) {
                    primeCount += 1
                }
            } else {
                makeArray(rangeStart: i + 1, rangeEnd: rangeEnd + 1)
            }
            
            currentArray.remove(at: currentArray.count - 1)
        }
    }

    makeArray(rangeStart: 0, rangeEnd: nums.count - combinationCount)
    return primeCount
}

func checkIsPrime(_ num: Int) -> Bool {
    for i in 2...Int(Double(num).squareRoot()) {
        if num % i == 0 {
            return false
        }
    }
    
    return true
}
```


<br>
