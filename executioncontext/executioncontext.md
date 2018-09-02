# 실행 컨텍스트

실행 컨텍스트는 추상적인 개념으로 자바스크립트 코드 블록이 실행되는 환경이다.

실행 컨텍스트가 실행되는 과정을 아래 코드를 이용해  설명을 할 것이다.

``` javascript
function func1(param1, param2) {
    var a = 10;
    var b = 20;
    
    function innerfunc() {
        return a+b;
    }
    
    return a + b + innerfunc();
}

func1(2,3);
```



1. func1() 함수가 호출되면 실행컨텍스트가 생성된다

   ![context1](images/context1.png)

   

2.  함수 내부의 정보를 담는 객체가 생성된다. 이를 활성객체 또는 변수객체라고 부른다.

    ![context1](images/context2.png)



3. argument 객체를 생성하고 활성객체의 argument 프로퍼티로 그 객체를 참조한다. 

   ![context1](images/context4.png)



4. 현재 컨텍스트의 유효범위를 나타내는 스코프 정보를 생성한다.  스코프 정보는 리스트 형태로 생성되고 이 [[scope]] 프로퍼티로 리스트를 참조할 수 있다.  현재의 컨텍스트에서 변수를 접근할 때 현재 컨텍스트에서 해당 변수를 찾지 못하면 [[scope]] 프로퍼티로 상위 실행 컨텍스트의 변수에 접근이 가능하다

   ![context1](images/context5.png)



5.  현재 컨텍스트 내부에서 사용되는 변수(func1() 함수의 내부에서 사용되는 변수)들이 생성된다.  여기서 중요한 점은 이 부분에선 변수와 함수를 메모리에 생성만 하고 초기화는 하지않는다는 점이다. 그래서 변수 a와 b에는 undefined라는 값이 할당된다.  그 후 변수객체가 생성이 완료되면 초기화가 진행된다.  이러한 **변수의 생성과 초기화의 작업이 분리되어 진행되기 때문에 함수호이스팅이 발생하는 것**이다!! 

    ![context1](images/context3.png)

   

6. 마지막으로 this 키워드를 사용하는 값이 할당된다. this 가 참조하는 객체가 없으면 전역 객체를 참조한다. 

   ![context1](images/context6.png)





# 스코프

자바스크립트의 유효범위(스코프)는 함수단위로 설정된다.  아래의 코드를 보면 알 수 있다. 

``` javascrip
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





# 스코프 체인

 스코프 체인이란 함수가 중첩함수일때 하위함수가 참조하는 상위함수의 변수등을 참조하는 것을 말한다. 

``` javascript
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





# 클로저

클로저란 자바스크립트의 스코프 체인을 이용해 생명 주기가 끝난 외부함수의 변수를 참조하는 것을 말한다.  좀 더 설명을 하자면 내부함수는 외부함수의 지역변수에 접근이 가능한데 외부함수의 실행이 끝난 이후에 내부함수가 외부함수 변수에 접근 할 수 있는다. 이것을 클로저라고 한다.  클로저의 전형적인 패턴은 아래의 코드와 같다!

 ``` javascript
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







