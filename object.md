# 자바스크립트 객체(Object)



### 객체의 생성방법

1. 객체 리터럴({})

   : "프로퍼티명 " : "값" 형태로 표기

   ```javascript
   // 객체 리터럴 방식으로 객체 생성
   var woonbi = {
       name : 'woonbi',
       age : 13
   }
   ```

   

2. Object() 생성자 함수 

   ```javascript
   // Object() 생성자 함수를 이용해 객체 생성
   var woonbi = new Object();
   
   // woonbi 객체에 프로퍼티 추가
   woonbi.name = 'woonbi';
   wonnbi.age = 13;
   
   ```

