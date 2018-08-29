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

   

