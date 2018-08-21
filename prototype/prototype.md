# prototype

: 모든 함수는 객체로서 prototype 프로퍼티를 가지고 있다.  함수를 생성할 때 함수 자신과 연결된 객체를 동시에 생성하는데 이 생성된 객체가 prototype 객체다. 생성된 prototype 객체는 constructor 프로퍼티를 가지고 있고 함수의 prototype 프로퍼티와 생성된 객체(prototype 객체)의 constructor 프로퍼티는 서로 참조하게 된다.

![prototype](/javascript=study/prototype/images/prototype1.PNG)



1. prototype 프로퍼티과  [[Prototype]] 프로퍼티 구분하기

   **[[Prototype]] 프로퍼티**는 객체에서 자신의 부모 역할을 하는 객체를 가리킨다. **prototype 프로퍼티**는 함수가 생성될 때 함수 자신과 연결된 객체(=prototype 객체)가 생성되는데 이 객체를 가리킨다.  이 **prototype 객체**는 함수가 생성자로 사용될 때 생성된 객체의 **[[Prototype]] 프로퍼티**로 연결된다. 

   

   아래 코드를 실행해보면 Dog 생성자 함수의 prototype 프로퍼티와 Dog 생성자 함수로 생성된 darong 객체의 [[Prototype]] 프로퍼티가 같은 prototype객체를 가리키고 있는 걸 알 수 있다!

    

   ~~~ javascript
   // Dog 생성자 함수
   function Dog (name) {
       this.name = name;
   }
   
   // darong 객체 생성
   var darong = new Dog('darong');
   
   console.dir(Dog);
   console.dir(darong);
   ~~~

   

   ![prototype2](/images/prototype2.PNG)

   

![prototype](/images/prototype3.PNG)

















