# 스코프

자바스크립트의 유효범위(스코프)는 함수단위로 설정된다.  아래의 코드를 보면 알 수 있다. 

```javascrip
var a = 1; 

function func1() {
    if(true) {
        var b = 3; 
    }
    
    return b;
}

console.log(func());    // 3 
```

대부분의 다른 언어들은 { , }안에 선언된 변수는 그 블록이 끝나는 순간 사라지기 때문에 블록 밖에서는 접근할 수 없다.  하지만 자바스크립트의 스코프는 함수단위로 설정되기 때문에   func1() 의 if문 블록 밖에서 안에 있는 변수 b에 접근이 가능한 것이다. 