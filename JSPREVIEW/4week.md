# 4주차

## Prototype
- JAVA,C++과 같은 클래스 기반 객체 지향 프로그램언어와 달리 Javascript는 프로토타입 기반 객체지향 언어
- 자바스크립트의 모든 객체는 자신의 부모 역할을 담당하는 객체와 연결
- 부모객체의 프로퍼티 또는 메소드를 상속 받아 사용가능(객체 지향 상속개념과 비슷)
- 이런 부모 객체를 Prototype 객체, 프로토타입이라고 함
- Prototype 객체는 생성자 함수에 의해 생성된 각각의 객체에 공유 프로퍼티를 제공하기 위해 사용
```js
var student = {
  name: 'Lee',
  score: 90
};

// student에는 hasOwnProperty 메소드가 없지만 아래 구문은 동작한다.
console.log(student.hasOwnProperty('name')); // true

console.dir(student);
```
- 자바스크립트의 모든 객체는 [[Prototype]]이라는 인터널 슬롯(internal slot)을 가지고있음
- [[Prototype]]의 값은 null 또는 객체이며 상속을 구현하는데 사용
- [[Prototype]] 객체의 데이터 프로퍼티는 get 액세스를 위해 상속되어 자식 객체의 프로퍼티처럼 사용할 수 있음(set엑세스는 허용하지 않음)
- [[Prototype]]의 값은 Prototype(프로토타입) 객체이며 __proto__ accessor property로 접근 가능
- __proto__ 프로퍼티에 접근하면 내부적으로 Object.getPrototypeOf가 호출되어 프로토타입 객체를 반환
- 객체를 생성할 때 프로토타입은 결정
- 결정된 프로토타입 객체는 다른 임의의 객체로 변경 가능 --> 부모 객체인 프로토타입을 동적으로 변경할 수 있다는 것을 의미

###[[Prototype]] vs prototype프로퍼티
-함수도 객체이므로 [[Prototype]] 인터널 슬롯을 가지고 있지만, 일반 객체와 달리 prototype프로퍼티도 소유
**주의해야 할 것은 prototype 프로퍼티는 프로토타입 객체를 가리키는 [[Prototype]] 인터널 슬롯은 다르다는 것이다. prototype 프로퍼티와 [[Prototype]]은 모두 프로토타입 객체를 가리키지만 관점의 차이가 있다.
```js
function Person(name) {
  this.name = name;
}

var foo = new Person('Lee');

console.dir(Person); // prototype 프로퍼티가 있다.
console.dir(foo);    // prototype 프로퍼티가 없다.
```
#### [[Prototype]]
- 함수를 포함한 모든 객체가 가지고 있는 인터널 슬롯
- 객체의 입장에서 자신의 부모 역할을 하는 프로토타입 객체를 가키리고, 함수 객체의 경우 Function.prototype를 가리킴
```js
console.log(Person.__proto__ === Function.prototype);
```
#### prototype 프로퍼티
- 함수 객체만 가지고 있는 프로퍼티
- 함수 객체가 생성자로 사용될 때 이 함수를 통해 생성될 객체의 부모 역할을 하는 객체(프로토타입 객체)
```js
console.log(Person.prototype === foo.__proto__);
```

### 프로토타입 체인
- 자바스크립트는 특정 객체의 프로퍼티나 메소드에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티 또는 메소드가 없다면 [[Prototype]]이 가리키는 링크를 따라 자신의 부모 역할을 하는 프로토타입 객체의 프로퍼티나 메소드를 차례대로 검색
```js
var student = {
  name: 'Lee',
  score: 90
}

// Object.prototype.hasOwnProperty()
console.log(student.hasOwnProperty('name')); // true
```
#### 객체 리터럴 방식으로 생성된 객체의 프로토타입 체인
- 객체 생성방법 : 1. 객체 리터럴 2. 생성자함수 3. Object() 생성자 함수
- 객체 리터럴 방식으로 생성된 객체는 결국 내장 함수(Built-in)인 Object() 생성자 함수로 객체를 생성하는 것을 단순화시킨 것
- Object() 생성자 함수는 물론 함수이므로, 일반객체와 달리 Prototype프로퍼티가 있음
- prototype 프로퍼티는 함수 객체가 생성자로 사용될 때 이 함수를 통해 생성된 객체의 부모 역할을 하는 객체, 즉 프로토타입 객체를 가리킴
- [[Prototype]]은 객체의 입장에서 자신의 부모 역할을 하는 객체, 즉 프로토타입 객체를 가리킨다.
```js
var person = {
  name: 'Lee',
  gender: 'male',
  sayHello: function(){
    console.log('Hi! my name is ' + this.name);
  }
};

console.dir(person);

console.log(person.__proto__ === Object.prototype);   // ① true
console.log(Object.prototype.constructor === Object); // ② true
console.log(Object.__proto__ === Function.prototype); // ③ true
console.log(Function.prototype.__proto__ === Object.prototype); // ④ true
```
** 결론적으로 객체 리터럴을 사용하여 객체를 생성한 경우, 그 객체의 프로토타입 객체는 Object.prototype이다. **

#### 생성자 함수로 생성된 객체의 프로토타입 체인
- 함수 정의 방법 : 1. 함수선언식  2. 함수 표현식  3. function() 생성자 함수
- 3가지 함수 정의 방식은 Function() 생성자 함수를 통해 함수 객체를 생성
- 어떠한 방식으로 함수 객체를 생성하여도 모든 함수 객체의 prototype 객체는 Function.prototype
- 생성자 함수도 함수 객체이므로 생성자 함수의 prototype 객체는 Function.prototype
- 객체 리터럴 방식이나 생성자 함수 방식이나 결국은 모든 객체의 부모 객체인 Object.prototype 객체에서 프로토타입 체인이 끝나기 때문에 Object.prototype 객체를 프로토타입 체인의 종점(End of prototype chain) 이라고함

### 객체의 확장
- 프로토타입 객체도 객체이므로 일반 객체와 같이 프로퍼티를 추가/삭제가능 
- 추가/삭제된 프로퍼티는 즉시 프로토타입 체인에 반영
```js
function Person(name) {
  this.name = name;
}

var foo = new Person('Lee');

Person.prototype.sayHello = function(){
  console.log('Hi! my name is ' + this.name);
};

foo.sayHello();
```
### 원시 타입(Primitive data type)의 확장
- 자바스크립트에서 원시 타입(숫자, 문자열, boolean, null, undefined)을 제외한 모든것은 객체
```js
var str = 'test';
console.log(typeof str);                 // string
console.log(str.constructor === String); // true
console.dir(str);                        // test

var strObj = new String('test');
console.log(typeof strObj);                 // object
console.log(strObj.constructor === String); // true
console.dir(strObj);
// {0: "t", 1: "e", 2: "s", 3: "t", length: 4, __proto__: String, [[PrimitiveValue]]: "test" }

console.log(str.toUpperCase());    // TEST
console.log(strObj.toUpperCase()); // TEST
```
- 원시 타입으로 프로퍼티나 메소드를 호출할 때 원시 타입과 연관된 객체로 일시적으로 변환되어 프로토타입 객체를 공유
- 원시 타입은 객체가 아니므로 프로퍼티나 메소드를 직접 추가할 수 없음
```js
var str = 'test';

// 에러가 발생하지 않음
str.myMethod = function () {
  console.log('str.myMethod');
};

str.myMethod(); // Uncaught TypeError: str.myMethod is not a function
```
### 프로토타입 객체의 변경
- 프로토타입 객체 변경 시점 이전에 생성된 객체 기존 프로토타입 객체를 [[Prototype]]에 바인딩
- 프로토타입 객체 변경 시점 이후에 생성된 객체 변경된 프로토타입 객체를 [[Prototype]]에 바인딩
```js
function Person(name) {
  this.name = name;
}

var foo = new Person('Lee');

// 프로토타입 객체의 변경
Person.prototype = { gender: 'male' };

var bar = new Person('Kim');

console.log(foo.gender); // undefined
console.log(bar.gender); // 'male'

console.log(foo.constructor); // ① Person(name)
console.log(bar.constructor); // ② Object()
```
### 프로토타입 체인 동작 조건
- 객체의 프로퍼티를 참조하는 경우, 해당 객체에 프로퍼티가 없는 경우, 프로토타입 체인이 동작
- 객체의 프로퍼티에 값을 할당하는 경우, 프로토타입 체인이 동작하지 않음
- 객체에 해당 프로퍼티가 있는 경우, 값을 재할당하고 해당 프로퍼티가 없는 경우는 해당 객체에 프로퍼티를 동적으로 추가하기 때문
```js
function Person(name) {
  this.name = name;
}

Person.prototype.gender = 'male'; // ①

var foo = new Person('Lee');
var bar = new Person('Kim');

console.log(foo.gender); // ① 'male'
console.log(bar.gender); // ① 'male'

// 1. foo 객체에 gender 프로퍼티가 없으면 프로퍼티 동적 추가
// 2. foo 객체에 gender 프로퍼티가 있으면 해당 프로퍼티에 값 할당
foo.gender = 'female';   // ②

console.log(foo.gender); // ② 'female'
console.log(bar.gender); // ① 'male'
```



## Constructor & new

### Constructor
- 프로토타입 객체는 constructor 프로퍼티를 가지며, constructor 프로퍼티는 객체 입장에서 자신을 생성한 객체를 가리킴
- 인스턴스를 생성하고 클래스 프로퍼티를 초기화하기 위한 특수한 메소드
- constructor는 클래스 내에 한 개만 존재할 수 있으며 만약 클래스가 2개 이상의 constructor를 포함하면 문법 에러(SyntaxError)가 발생
-  인스턴스를 생성할 때 new 연산자와 함께 호출한 것이 바로 constructor이며 constructor의 파라미터에 전달한 값은 클래스 프로퍼티에 할당
- constructor는 생략 가능
- constructor는 인스턴스의 생성과 동시에 클래스 프로퍼티의 생성과 초기화를 실행
```js
function Person(name) {
  this.name = name;
}

var foo = new Person('Lee');

// Person() 생성자 함수에 의해 생성된 객체를 생성한 객체는 Person() 생성자 함수
console.log(Person.prototype.constructor === Person);

// foo 객체를 생성한 객체는 Person() 생성자 함수
console.log(foo.constructor === Person);

// Person() 생성자 함수를 생성한 객체는 Function() 생성자 함수
console.log(Person.constructor === Function);
``` 
### new
- 사용자 정의 객체 타입 또는 내장 객체 타입의 인스턴스를 생성
```js
function Car(make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;
}

var car1 = new Car('Eagle', 'Talon TSi', 1993);

console.log(car1.make);
// expected output: "Eagle"
```
- 일정한 형식이 정해진것이 아닌 정의한 함수에 new키워드를 붙여 변수에 호출하면 그자체로 생성자의 역할을 함
- 생성자함수와 일반함수의 구분은 명확치 않음
- 구분하기위해 생성자 함수의 첫 글자는 항상 대문자로 사용(권장)
- 생성자 함수 동작 방법
```
1. 먼저 빈 객체 생성, this를 이 객체에 바인딩(new키워드를 사용하지 않을 경우에 this는 전역객체인 window에 바인딩됨). 또한 생성한 객체의 프로토타입 객체를 (__proto__)자신의 생성자의 프로토타입 프로퍼티로 설정
2. 생성자 내부에 this키워드로 정의된 프로퍼티들을 객체 내에 동적으로 생성
3. 생성자 내부에 return문에 따로 없으면, 생성한 객체 리턴. this키워드를 리턴해도 생성한 객체 반환(new키워드를 사용하지 않았고//즉, 함수로 사용하였고 //, return문을 명시하지 않았을 경우 undefined가 반환)
```

## OOP & Instance
### OOP (객체지향 프로그래밍)
- 프로그램 내에서 표현하고자 하는 실 세계(real world)의 일들을 객체를 사용해서 모델링 하고, 객체를 사용하지 않으면 불가능 혹은 무지 어려웠을 일들을 쉽게 처리하는 방법을 제공한다는 것
- 객체 인스턴스는 클래스를 통해서 만들 수 있음(객체는 클래스에 정의된 데이터와 함수를 가지고 있음)
- 상속(Inheritance), 캡슐화(Encapsulation), 다형성(Polymorphism) 
- 구현 방법중 하나
- 프로그래밍 언어를 명령어의 집합이 아닌 객체의 집합으로 보자는 관점에서 시작하여 "객체들간의 메시지 전달" 로서 프로그래밍 하는 것일 뿐 그 이상 그 이하도 아님
- 절차지향적인 언어의 문제점중 하나인 파급효과를 줄이기 위해 변수와 메소드를 객체라는 모듈로 묶어 버리고 그 모듈안에 있는 변수/메소드의 사용범위를 모듈 내부에서만 사용하거나 (private) 그 모듈 그 모듈 상속한 모듈에서만 사용 가능하거나 (protected) 모든 모듈이 사용 가능하게 (public) 설정하는데 목적

### Instance
- 비슷한 성질을 가진 여러개의 객체를 만들기 위해서 생성자 함수, Constructor를 만들어 찍어내듯이 사용하는데 이렇게 생성된 객체를 말함
- 기본적으로 생성된 인스턴스는 원래의 객체인 클래스나 프로토타입이 가지고 있는 프로퍼티(property)와 메소드(method)를 모두 상속
- 상속을 통해 객체가 가지고 있는 프로퍼티와 메소드를 인스턴스에서도 동일하게 사용이 가능
```js
// 객체를 만들기 위한 생성자함수(Class)를 생성함
Shirt = function(color) {
   this.color = color;
}


var Shirt1 = new Shirt('Yellow');
// 위 과정을 통해 Shirt1이란 인스턴스가 생성됨

var Shirt2 = new Shirt('white');
var Shirt3 = new Shirt('blue');
...
// 수 많은 인스턴스를 생성할 수 있음
```

[참고]
https://poiemaweb.com/js-prototype,https://poiemaweb.com/es6-class+,https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/new,https://hsp1116.tistory.com/10,https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Object-oriented_JS,https://okky.kr/article/205078,https://webisfree.com/2016-04-20/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5%EC%96%B8%EC%96%B4%EC%97%90%EC%84%9C-%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4(instance)%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80