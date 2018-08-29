# 함수



### 특징

1. 변수 또는 프로퍼티 값으로 할당할 수 있음.

   ``` javascript
   // 변수에 함수를 할당
   var foo = 100; 
   var abc = function () {
       return 200;
   }
   
   console.log(abc());  // 200;
   
   // 프로퍼티에 함수를 할당
   var obj = {}; 
   obj.abc = function () {
       return 200;
   }
   
   console.log(obj.abc());  // 200;
   ```

   

2. 함수를 인자로 전달할 수 있음.

   ``` javascript
   // 함수 표현식으로 함수를 생성
   var abc = function(func) {
       func(); // 인자로 넘어온 함수를 호출함.
   }
   
   abc(function() {
      console.log('abc() 함수 실행');
   });
   ```

   

### 함수 정의 방법













### 함수의 표준 프로퍼티

1. name

   : 함수의 이름

   

2. caller

   : 자신을 호출한 함수명으로 호출한 함수가 없는 경우 null

   

3. length 

   : 함수가 실행될 때 기대되는 인자의 개수

   

4. arguments

   : 함수를 호출할 때 전달되는 인자 값으로 함수가 호출된 상태가 아니면 null !
   자바스크립트는 함수를 호출할 때 함수의 형식에 맞춰 인자를 넘기지 않아도 오류가 발생하지 않는데 호출된 인자의 개수를 확인하고 동작을 다르게 해야할 경우가 있다. 이럴때에 arguments객체를 활용하면 된다.

   ``` javascript
   // 인자가 2개인 func함수 정의 
   // 보통의 프로그램에선 인자의 값을 맞춰서 넘기지 않으면 오류가 발생하지만
   // 자바스크립트에선 아무 문제없음!! 
   function func(arg1, arg2){
       console.log(arg1, arg2);
   }
   
   func();				// undefined undefined
   func(1);			// 1 undefined 
   func(1,2);			// 1 2
   func(1,2,3);		// 1 2    => 초과된 인수는 무시함.
   
   // argument객체활용
   function sum() {
       var result = 0;
       
       for(var i=0; i < arguments.length; i++){
           result += arguments[i];
       }
       return result;
   }
   
    console.log(sum(1,3,4,5));
    console.log(sum(1,3,4,5,7,8,9));
   ```

   

   

5. [[Prototype]] 링크

   : 자신의 부모역할을 하는 프로토타입 객체를 가리킴

   

6. prototype

   : 함수가 생성될 때  construnctor프로퍼티와 [[Prototype]] 프로퍼티가 있는 프로토타입 객체가 생성되는데 prototype 프로퍼티는 이 프로토타입 객체를 가리킴

   

7. call과 apply 

   :  [this 바인딩](thisbinding.md)에서 설명

    

### 함수 호이스팅

호이스팅이란 변수를 선언하고 초기화 했을 때 변수의 선언부분이 최상단으로 끌어올려지는 것을 말한다.  함수표현식과 함수선언식으로 생성한 함수를 보면 알 수 있다. 

1. 함수 선언문으로 함수 생성

   ``` javascript
   [코드]
   add(5,3);
   
   // 함수 선언문으로 정의한 add함수
   function add(x, y){
       return a+b;
   }
   
   add(3,4);
   ```

   ``` javascript
   [실행결과]
   8
   7
   ```

2. 함수 표현식으로 함수 생성

   ``` javascript
   [코드]
   add(1,2);
   
   // 함수 표현식으로 정의한 add함수
   var add = function (x, y){
       return x+y;
   };
   
   add(3,4); 
   ```

   ``` javascript
   [실행결과]
   Uncaught TypeError: add is not a function
   7
   ```

   

위 코드에서 알 수 있듯이 함수 선언문으로 생성한 함수는 함수 식 자체가 위로 올라가 add() 함수를 선언하기 전에 호출한 add(5,3)이 정상적으로 실행되었다. 

반대로 함수 표현식으로 생성한 함수는 변수의 선언만 위로 끌어올려지고 초기화 부분은 그대로 있기 때문에 add(1,2)를 호출한 시점에는 아직 add() 함수가 생성되기 전이므로 오류가 발생한다! 



### 함수 스코프(scope)와 스코프 체이닝

``` javascript
function parent() {
    var a = 10; 
    var b = 20; 
    
    function child() {
        var b = 30; 
        
        console.log(a);
        console.log(b);
    }
    
    child();
}

parent();
child();
```

위의 코드를 실행하면 어떤 결과가 나올까?  child() 함수에 a라는 변수가 선언되어있지 않기 때문에 오류가 발생한다고 생각할 수도 있다. 하지만 실행결과는 아래와 같다.

``` java
[실행결과]

10
30
Uncaught ReferenceError: child is not defined

```

child() 함수에는 a라는 변수가 선언되어있지 않은데 child() 함수가 호출됐을 때 10이출력된다.  그 이유는 parent() 함수의 변수 a의 값에 접근했기때문이다.  그리고 변수 b는 child() 함수에 선언되어있기때문에 parent()의 변수 a가 아닌 child() 함수의 변수 b의 값이 바로 출력된다.

이 처럼 **내부함수(child)는 자신을 둘러싼 외부함수(parent) 변수에 접근이 가능하다.** 이것이 가능한 이유는 바로 자바스크립트의 **스코프 체이닝** 때문이다.  

스코프체이닝에 대해선 [스코프체이닝](scope.md)을 참고! 



### 함수리턴

1.  일반 함수, 메서드는 리턴값을 지정하지 않으면 undefined값이 리턴된다

   ``` javascript
   [코드]
   var func = function() {
       console.log('리턴값이 없는 함수');
   }
   
   console.log(func());
   ```

   ``` javascript
   [실행결과]
   리턴값이 없는 함수
   undefined
   ```

   

2. 생성자 함수에서 리턴값을 지정하지 않으면 생성된 객체가 리턴된다. 

   만약 이 생성자 함수에 다른 객체를 리턴한다면 어떻게 될지 아래 코드에서 확인해보자.

   ``` javascript
   [코드1] 다른객체를 리턴
   
   function Person(name,age){
       this.name = name;
       this.age = age;
       
       // 다른 객체 반환
       return {name : 'sujin', age : 26};
   }
   
   var rowoon = new Person ('rowoon', 29);
   console.log(rowoon);
   
   [코드2] 기본타입을 리턴
   
   function Person(name,age){
       this.name = name;
       this.age = age;
       
       // 숫자 리턴
       return 100;
   }
   
   var rowoon = new Person ('rowoon', 29);
   console.log(rowoon);
   ```

   ``` javascript
   [코드1 실행결과]
   {name: "sujin", age: 26}
   
   [코드2 실행결과]
   Person {name: "rowoon", age: 29}
   ```

   위 코드에서 알 수 있듯이 생성자 함수의 리턴값을  다른 객체로 지정하면 지정된 객체가 리턴되고 숫자나 불린 문자열등을 리턴할 경우에는 이러한 리턴값을 무시하고 this로 바인딩된 객체가 리턴된다.















