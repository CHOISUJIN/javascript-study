# 자바스크립트 객체(Object)와 배열(Array)



### 객체의 생성방법

1. 객체 리터럴({})

   : "프로퍼티명 " : "값" 형태로 표기

   ~~~ javascript
   // 객체 리터럴 방식으로 객체 생성
   var woonbi = {
       name : 'woonbi',
       age  : 13
   }
   
   ~~~

   

2. Object() 생성자 함수 

   ~~~ javascript
   // Object() 생성자 함수를 이용해 객체 생성
   var woonbi = new Object();
   
   // woonbi 객체에 프로퍼티 추가
   woonbi.name = 'woonbi';
   wonnbi.age = 13;
   
   ~~~

3. 생성자 함수를 이용한 객체 생성

   ``` javascript
   // 생성자 함수
   function Person(name) { 
   	this.name = name;
   }
   
   var sujin = new Person('sujin'); 
   ```

   

### 객체 프로퍼티 접근방법

1.  대괄호 표기법이나 마침표 표기법으로 접근 할 수 있음.

   ``` javascript
   // 객체 리터럴 방식으로 객체 생성
   var woonbi = {
       name : 'woonbi'
   }
   
   // 객체 프로퍼티 동적으로 생성
   woonbi.age = 13;
   console.log(woonbi.age);		// 13
   
   // 객체 프로퍼티 읽기
   console.log(woonbi.name); 		// woonbi
   console.log(woonbi['name']);	// woonbi
   
   // 객체 프로퍼티 값 변경
   woonbi.age = 15; 
   console.log(woonbi.age);		// 15
   
   // 객체 프로퍼티 삭제
   console.log(woonbi.age);		// 15
   delete woonbi.name;				
   console.log(woonbi.age);		// undefined
   
   ```

   ** 자바스크립트는 프로퍼티에 값을 할당할 때 프로퍼티가 있으면 값 변경, 없으면 프로퍼티 추가 후 값을 할당함!! 위의 프로퍼티 동적생성과 값 변경 예를 보면 알 수 있음 

   





---



### 배열의 특징

1.  같은 배열에 있는 요소의 데이터 타입이 다를 수 있다. 
2.  배열의 크기를 지정하지 않아도 된다.



### 배열의 생성방법과 접근방법

1. 배열 리터럴([])

   ``` javascript
   // 배열 리터럴을 이용해 4개의 요소를 가진 배열 생성
   var fruitArr = ['lemon', 'strawberry', 'watermelon', 'grape'];
   
   // 배열의 인덱스값을 이용해 접근 (배열의 첫번째 요소의 인덱스는 0부터 시작)
   console.log(fruitArr[0]);   // lemon
   console.log(fruitArr[1]);   // strawberry
   console.log(fruitArr[2]);   // watermelon
   
   ```

   

2.  Array() 생성자 함수 

   : 생성자 함수를 호출할 때 인자 개수에 따라 동작이 달라지므로 주의해야함! 

   - 호출된 인자가 1개 : 호출된 인자를 length로 갖는 빈 배열 생성
   - 호출된 인자가 여러개 : 호출된 인자를 요소를 갖는 배열 생성

   ``` javascript
   // Array() 생성자 함수를 이용해 4개의 요소를 가진 배열 생성
   // 호출된 인자1개
   var colorArr = new Array(5);
   console.log(colorArr);			// [empty x 5]
   console.log(colorArr.length);	 // 5
   
   // 호출된 인자 여러개
   var fruitArr = new Array('lemon', 'strawberry', 'watermelon', 'grape');
   console.log(fruitArr);			// ['lemon', 'strawberry', 'watermelon', 'grape'];
   console.log(fruitArr.length);	 // 4
   
   
   // 배열의 인덱스값을 이용해 접근 (배열의 첫번째 요소의 인덱스는 0부터 시작)
   console.log(fruitArr[0]);   // lemon
   console.log(fruitArr[1]);   // strawberry
   console.log(fruitArr[2]);   // watermelon
   
   ```



### 배열에 동적으로 요소 추가하기

: 값을 순차적으로 넣지 않아도 된다.  아래 코드 처럼 아무 위치에나 값을 넣을 수 있고 데이터 타입이 일치하지 않아도 된다.

``` javascript
// 배열 리터럴을 이용해 빈 배열 생성
var Arr = []; 	

// 동적으로 요소 추가
Arr[1] = true;
Arr[5] = '가나다';
Arr[77] = 123;
Arr[100] = 1;

console.log(Arr);  // [empty, true, empty × 3, "가나다", empty × 71, 123, empty × 22, 1]
console.log(Arr.length); // 101 (배열의 length는 가장 큰 인덱스+1 )

```



