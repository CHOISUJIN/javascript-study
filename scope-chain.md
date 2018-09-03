# 스코프 체인

 스코프 체인이란 함수가 중첩함수일때 하위함수가 참조하는 상위함수의 변수등을 참조하는 것을 말한다. 

```javascript
var a = 1; 

function outerFunc() {
    var b = 2; 
    function innerFunc() {
        var c = 3; 
        
        console.log("a : " + a);
        console.log("b : " + b);
        console.log("c : " + c);
    }
    return innerFunc();
}

outerFunc();
```



