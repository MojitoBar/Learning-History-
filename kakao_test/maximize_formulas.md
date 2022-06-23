[문제](https://programmers.co.kr/learn/courses/30/lessons/67257)

```swift
func 수식최대화(_ expression:String) -> Int64 {
    // 일단 숫자와 부호로 나누기
    let numArr = expression.components(separatedBy: ["*", "+", "-"])
    let signArr = expression.components(separatedBy: ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"]).filter { $0 != "" }
    
    // 부호 배열
    let arr: [[String]] = [["*", "+", "-"], ["*", "-", "+"], ["+", "*", "-"],
                           ["-", "+", "*"], ["-", "*", "+"], ["+", "-", "*"],]
    
    var maxValue: Int64 = 0
    
    // 우선순위가 정해진 부호 3개를 반복하면서
    for i in arr {
        var copyNum = numArr
        var copySign = signArr
        for j in i {
            // 부호가 아직 있으면 계산
            while copySign.contains(j) {
                let index = Int(exactly: copySign.firstIndex(of: j)!)!
                copySign.remove(at: index)
                
                if j == "-" {
                    let temp = Int(copyNum[index])! - Int(copyNum[index + 1])!
                    
                    copyNum.remove(at: index + 1)
                    copyNum.remove(at: index)
                    copyNum.insert(temp.description, at: index)
                    print(copyNum)
                }
                else if j == "+" {
                    let temp = Int(copyNum[index])! + Int(copyNum[index + 1])!
                    
                    copyNum.remove(at: index + 1)
                    copyNum.remove(at: index)
                    copyNum.insert(temp.description, at: index)
                    print(copyNum)
                }
                else if j == "*" {
                    let temp = Int(copyNum[index])! * Int(copyNum[index + 1])!
                    
                    copyNum.remove(at: index + 1)
                    copyNum.remove(at: index)
                    copyNum.insert(temp.description, at: index)
                    print(copyNum)
                }
            }
        }
        maxValue = max(maxValue, Int64(abs(Int(copyNum[0])!)))
    }
    // 부호가 없어질 때까지 반복
    
    return maxValue
}
```
