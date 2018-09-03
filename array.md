# 자바스크립트 배열(Array)



### 배열의 특징

1. 같은 배열에 있는 요소의 데이터 타입이 다를 수 있다. 
2. 배열의 크기를 지정하지 않아도 된다.



### 배열의 생성방법과 접근방법

1. 배열 리터럴([])

   ```javascript
   // 배열 리터럴을 이용해 4개의 요소를 가진 배열 생성
   var fruitArr = ['lemon', 'strawberry', 'watermelon', 'grape'];
   
   // 배열의 인덱스값을 이용해 접근 (배열의 첫번째 요소의 인덱스는 0부터 시작)
   console.log(fruitArr[0]);   // lemon
   console.log(fruitArr[1]);   // strawberry
   console.log(fruitArr[2]);   // watermelon
   
   ```

   

2. Array() 생성자 함수 

   : 생성자 함수를 호출할 때 인자 개수에 따라 동작이 달라지므로 주의해야함! 

- 호출된 인자가 1개 : 호출된 인자를 length로 갖는 빈 배열 생성
- 호출된 인자가 여러개 : 호출된 인자를 요소를 갖는 배열 생성

```javascript
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

```javascript
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



### 유사 배열 객체란?

자바스크립트의 모든 배열은 lenght 프로퍼티가 존재한다.  length 프로퍼티는 배열내의 가장 큰 인덱스에 1을 더한값이다.  그런데 여기서 객체에 length 프로퍼티가 있으면 어떻게 될까? 자바스크립트에선 객체인데 length 프로퍼티를 가진 객체를 **유사 배열 객체**라고 한다.  
그렇다면 유사 배열 객체는 배열의 표준 메서드인 push()를 사용할 수 있을까?  아래 코드로 확인해보자! 

```javascript 
var arr = ['abc']; 
var obj = {
    name: 'woonbi',
    length: 1
}

arr.push('def');
console.log(arr);     // ['abc', 'def']

obj.push('darong');   // Uncaught TypeError: obj.push is not a function
```

 arr 배열의 경우 push() 메소드를 사용해 'def' 원소를 추가했지만, 유사 배열 객체인 obj는 오류가 발생했다.  그럼 어떻게 해야 유사 배열 객체는 배열의 메소드를 사용할 수 있을까?? 
바로 **apply() 메서드**를 이용하면 된다! 

```javascript
var obj = {
    name: 'woonbi',
    length: 1
}

Array.prototype.push.apply(obj, ['darong']);
console.log(obj);   // {1: "darong", name: "woonbi", length: 2}
```



