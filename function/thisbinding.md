# this 바인딩



1. 객체의 메서드 호출 시 this 바인딩

   :  객체의 메서드는 객체의 프로퍼티가 함수인 것을 말하고 이 메서드를 호출할 때 this는 해당 메서드를 호출한 객체로 바인딩 된다. 

   ``` javascript
   // woonbi 객체 생성
   var woonbi = {
       name : 'woonbi',
       sayName : function () {
           console.log(this.name);
       }
   }
   
   // darong 객체 생성
   var darong = {
       name : 'darong'
   }
   
   // darong 객체에 sayName 프로퍼티 추가
   darong.sayName = woonbi.sayName; 
   
   // sayName() 메서드 호출
   woonbi.sayName();	// woonbi
   darong.sayName();	// darong
   ```

   

2. 함수 호출 시 this 바인딩 

   : 함수를 호출할 때 내부 코드에서 사용된 this는 전역 객체(window)에 바인딩된다. 

     ``` javascript
   var test = 'test';
   
   // 전역변수는 window 객체의 프로퍼티로 접근 가능
   console.log(window.test);	// test
   
   var sayFoo = function () {
       console.log(this.test);
   }
   
   sayFoo();  // test
     ```

   

3. 내부 함수를 호출했을 경우 this 바인딩

   : 내부 함수에서 this를 이용할 때에도 위의 함수 호출 시 this 바인딩과 똑같이 적용된다.

   ``` javascript
   [코드]
   var value = 200;
   
   var obj = {
       value:20,
       // func1 메서드
       func1: function() {
           this.value += 1; 
           console.log('func1() this.value : ' + this.value);
           
           // func2() 내부함수
           func2 = function() {
               this.value += 1; 
               console.log('func2() this.value : ' + this.value);
               
               // func3() 내부함수
               func3 = function() {
               this.value += 1; 
               console.log('func3() this.value : ' + this.value);
               }
   			func3();
           }	
   		func2();
       }
   };
   obj.func1();
   ```

   ``` javascript
   [실행결과]
   func1() this.value : 21
   func2() this.value : 201
   func3() this.value : 202
   ```

   func1()은 프로퍼티의 메서드이므로 this는 호출한 객체를 가리키므로 func1()의 this.value는 20이된다. 그 다음 func2()는 func1()의 내부 함수이므로 this.value는 func1()의 value값이라고 생각할 것이다. func3()도 마찬가지이다. 하지만, 내부함수인 func2(), func3()는 함수이므로 이를 호출할 때는 함수 호출로 취급된다.  

   그렇다면 부모 함수의 this가 가리키는 객체에 접근하려면 어떻게 해야할까?  부모함수의 this를 다른 변수에 저장하는 방법을 이용하면된다! 보통 이런 변수의 이름을 that이라고 사용한다. 

   ``` javascript
   [코드]
   var value = 200;
   
   var obj = {
       value:20,
       // func1 메서드
       func1: function() {
           var that = this; 	// func1()의 this의 값을 that 변수에 저장!!! 
           
           this.value += 1; 
           console.log('func1() this.value : ' + this.value);
           
           // func2() 내부함수
           func2 = function() {
               that.value += 1; 
               console.log('func2() this.value : ' + that.value);
               
               // func3() 내부함수
               func3 = function() {
               that.value += 1; 
               console.log('func3() this.value : ' + that.value);
               }
   			func3();
           }	
   		func2();
       }
   };
   obj.func1();
   ```

   ``` javascript
   [실행결과]
   func1() this.value : 21
   func2() this.value : 22
   func3() this.value : 23
   ```

   

4. 생성자 함수 호출 시 this 바인딩

   : 자바스크립트에서는 기존 함수에 new 연산자를 붙여 호출하면 그 함수는 생성자 함수로 동작한다. 

   ```  javascript
   // 생성자 함수 정의
   var Person = function(name, age) {
       this.name = name;
       this.age = age;       
   }
   
   // woonbi 객체 생성
   var woonbi = new Person('woonbi', 13);
   
   ```

   생성자 함수로  호출되면 함수의 코드가 실행되기전에 빈객체를 생성하고 그 생성한 객체에 this 바인딩이 된다.  그리고 그 this로 바인딩된 객체가 리턴된다. 

   

5. apply와 call메서드를 이용한 명시적 this 바인딩

   : function.apply(thisArg, array) 와 같이 사용한다. 

   thisArg는 this바인딩이 되는 객체이고 array는 함수를 호출할 때 넘겨주는 인자값이다. 

   ``` javascript
   function Person(name, age){
       this.name = name;
       this.age = age;
   }
   
   var foo = {};
   
   Person.apply(foo, ['woonbi', 13]);
   ```

   

   
