[문제](https://school.programmers.co.kr/learn/courses/30/lessons/60058)

```swift
import Foundation

var result = ""

func solution(_ p:String) -> String {
    if correct(string: p) {
        return p
    }
    else{
        result = againFromFirst(string: p)
    }
    
    return result
}

func againFromFirst(string: String) -> String {
    if string == "" {
        return ""
    }
    var temp = balance(string: string)
    print(temp)
    if correct(string: temp[0]) {
        return temp[0] + againFromFirst(string: temp[1])
    }
    else {
        temp[0].removeLast()
        temp[0].removeFirst()
        return "(" + againFromFirst(string: temp[1]) + ")" + change(string: temp[0])
    }
}

func balance(string: String) -> [String] {
    var result: [String] = []
    var str = ""
    var count = 0
    for s in 0..<string.count {
        if string[string.index(string.startIndex, offsetBy: s)] == "(" {
            count += 1
            str += "("
        }
        else if string[string.index(string.startIndex, offsetBy: s)] == ")" {
            count -= 1
            str += ")"
        }
        
        if count == 0 && str != "" {
            result.append(str)
            let start = string.index(string.startIndex, offsetBy: s + 1)
            let end = string.endIndex
            let range = start..<end
            result.append(string[range].description)
            return result
        }
    }
    return result
}

func correct(string: String) -> Bool {
    var count = 1
    if string.first?.description != "(" || string.last?.description != ")" {
        return false
    }
    for i in 1..<string.count - 1 {
        if string[string.index(string.startIndex, offsetBy: i)].description == "(" {
            count += 1
        }
        else {
            count -= 1
        }
        if count < 0 {
            return false
        }
    }
    return true
}

func change(string: String) -> String {
    var temp = ""
    for i in string {
        if i.description == "(" {
            temp += ")"
        }
        else {
            temp += "("
        }
    }
    return temp
}
```
