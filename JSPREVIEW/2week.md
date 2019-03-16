#1주차 예습 숙제

## 값,식,문

### 값(value)
- 값은 프로그램에 의해 조작될 수 있는 대상.
- 기본타입과 참조타입으로 나눠져 있음
- 기본타입 == 원시값(Primitive value)
- 참조타입 == 객체 (Object)
- 리터럴 표기법으로 생성할 수 있음
- 자바스크립트는 다른 언어와 달리 변수에 할당된 값의 타입에 의해 동적으로 변수의 타입이 결정됨(동적타이핑)
```js
// 숫자 리터럴
10.50
1001
// 문자열 리터럴
'Hello'
"World"
// 불리언 리터럴
true
false
// null 리터럴
null
// undefined 리터럴
undefined
// 객체 리터럴
{ name: 'Lee', gender: 'male' }
// 배열 리터럴
[ 1, 2, 3 ]
// 정규표현식 리터럴
/ab+c/
// 함수 리터럴
function() {}
```
- 원시값들은 다양한 연산자의 값이 될수 있음
- 리터럴은 연산에 의해 하나의 값이 될 수 있음
```js
//산술 연산
11+10
```
### 식(expression)
- 식은 하나의 값이다.
- 값, 변수, 객체의 프로퍼티 , 배열, 함수호출, 메소드호출, 피연산자와 연산자의 조합을 모두 식이라 함
- 식은 다른 식의 일부가 되어 좀더 복잡한 식을 구성 할 수 있음
```js
// 표현식
5             // 5
5 * 10        // 50
5 * 10 > 10   // true
(5 * 10 > 10) && (5 * 10 < 100)  // true
```

### 문(statement)
- 리터럴, 연산자(Operator),표현식(Expression),키워드(Keyword) 등으로 구성
- 세미콜론(;)으로 끝남
```js
var x = 5;
var y = 6;
var z = x + y;

window.alert(z);
```
- 코드블록으로 그룹화 가능 => 함께 실행되어지는 문을 정의하기 위해
```js
// 함수
function myFunction(x, y) {
  return x + y;
}

// if 문
if(x > 0) {
  // do something
}

// for 문
for (var i = 0; i < 10; i++) {
  // do something
}
```
- 문은 일반적으로 위에서 아래로 실행
- 조건문(if,switch)/반복문(while,for)으로 흐름제어(control flow) 가능
- 함수호출로 변경 가능
- 블록 유효범위(block-level scope)를 생성하지않음
- 함수단위 유효범위(function-level scope) 생성
```js
var time = 10;
var greeting;

if (time < 10) {
  greeting = 'Good morning';
} else if (time < 20) {
  greeting = 'Good day';
} else {
  greeting = 'Good evening';
}

window.alert(greeting);
```

## Primitive Type & Reference type 차이점 및 이해
- Primitive Type(원시타입) = 숫자(number), 불린(boolean),null,undefined,문자열(string)
- Reference type(참조타입) = 객체(object), 배열(array), 함수(function)

### Primitive Type(원시타입)
1. 데이터
- 변수에 할당될 때 메모리 상에 고정된 크기로 저장, 원시 데이터 값 보관
- 변수선언, 초기화, 할당시 값이 저장된 메모리영역에 직접적으로 접근
- 변수에 새값이 할당되면 메모리 블럭에 저장된 값을 바로 변경

2. 데이터 복사
- 각 변수간 원시 타입데이터를 복사 할 경우 데이터 값이 복사 됨
```js
var x = 100;
var y = x;
x = 99;
y; // 100;
```
### Reference type(참조타입)
1. 데이터
- 크기가 정해져 있지 않고 변수에 할당될 때 값이 직접 해당 변수에 저장 될 수 없음
- 변수에는 데이터에 대한 참조만 저장
- 변수의 값이 저장된 힙(Heap) 메모리의 주소 값을 저장
- 변수의 값이 저장된 메모리 블럭의 주소를 가지고 있음

2. 데이터 복사
- 각 변수간 참조 타입데이터를 복사 할 경우 데이터의 참조가 복사 됨
```js
var x = {count: 100};    // 참조 타입 선언
var y = x;
x.count = 99;
y.count;    // 99, 'x'와 'y'는 동일한 참조를 담고 있으며, 따라서 동일한 객체를 가리킴
```

즉, 원시데이터는 값을 넘겨주고 Object는 Reference, 메모리 주소를 넘겨줌.

## Truthy & Falsy 차이점 및 이해
- Truthy : Boolean에서 True로 처리되는 값
- Falsy : Boolean에서 False로 처리되는 값
- true,false를 진리값이라고 하며, 프로그래밍에서 참,거짓을 나타내기 위해 사용
- boolean 타입이 와야하는 자리에 다른 타입의 값이 와도 에러가 나지 않고 실행 됨

- undefined, null,0,-0,NaN,''(빈문자열)은 제어문의 조건식과 같이 불리언 값으로 평가되어야 할 컨텍스트에서 false로 평가되는 falsy값임
- falsy값 이외의 값은 제어문의 조건식과 같이 불리언 값으로 평가되어야 할 컨텍스트에서 모두 True로 평가되는 Truthy값임
- truthy와 falsy 를 활용하면 짧은 코드작성 가능,but 코드의 의미가 불분명해지거나 논리적인 결함이 생길수 있기 때문에 주의

[참조]
https://poiemaweb.com/js-syntax-basics,
https://weicomes.tistory.com/133,
https://poiemaweb.com/js-type-coercion,
https://helloworldjavascript.net/pages/150-boolean.html