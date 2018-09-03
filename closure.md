# 클로저

클로저란 자바스크립트의 스코프 체인을 이용해 생명 주기가 끝난 외부함수의 변수를 참조하는 것을 말한다.  좀 더 설명을 하자면 내부함수는 외부함수의 지역변수에 접근이 가능한데 외부함수의 실행이 끝난 이후에 내부함수가 외부함수 변수에 접근 할 수 있는다. 이것을 클로저라고 한다.  클로저의 전형적인 패턴은 아래의 코드와 같다!

```javascript
function outerFunc() {
    var a = 1; 
    
    var innerFunc = function() {
        console.log(a);
    }
    
    return innerFunc;
}

var inner = outerFunc();
inner(); 
```



