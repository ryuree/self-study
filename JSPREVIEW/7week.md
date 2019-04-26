#7주차
## Function
- 어떤 작업을 수행하기 위해 필요한 Statement의 집합(코드블럭)
- 여러번 재사용 가능
- 동일한 작업 시에 같은 코드를 반복해서 쓰는게 아니라 함수를 만들어 사용하면 효율적
### 함수 정의
- 함수 선언문
- 함수 표현식
- Function 생성자

#### 함수선언문 ( Function declaration )
- 함수명 생략 불가능
- 매개변수 : 괄호로 감싸고 콤마로 구분, 타입 기술x(함수 안에서 타입체크의 필요성)
- 함수가 실행되는 Statement의 집합은 {}(중괄호)로 감싸고 return으로 반환
```js
function square(number) {
  return number * number;
}
```

#### 함수표현식
- 무명으로 표현가능(함수명 생략하는것이 일반적)
- 변수, 자료구조(객체,배열 등) 안에 저장가능
- 함수 파라미터로 전달
- 반환값 사용 가능
```js
var foo = function multiply(a, b) {
  return a * b;
};


var bar = function(a, b) {
  return a * b;
};

console.log(foo(10, 5)); // 50
console.log(multiply(10, 5)); // Uncaught ReferenceError: multiply is not defined
```

- 함수는 일급객체라서 변수에 할당 가능 : 이 변수는 함수 명이 아니라 할당된 함수를 가리키는 참조값을 저장가능(호출시 함수명이 아니라 변수 호출해야함)
- 함수가 할당된 변수 외에 기명함수 함수명으로 호출하면 에러발생(외부 코드에서 접근 불가능)

#### Function 생성자 함수
- 함수선언문과 함수표현식 : 리터럴 방식으로 정의
- 내장함수 Function생성자 함수를 생성하는 것을 단순화 한 Short-hand(축약법)
```js
var square = new Function('number', 'return number * number');
console.log(square(10)); // 100
```
- 일반적으로 잘 사용하지 않음

## Closure
- 독립적인 (자유)변수를 가리키는 함수
- 클로저 안에 정의되는 함수는 만들어진 환경을 기억

```js
function getClosure() {
  var text = 'variable 1';
  return function() {
    return text;
  };
}

var closure = getClosure();
console.log(closure()); // 'variable 1'
```
- getClosure()은 함수를 반환, 이때 반환된 함수를 클로저라고 함
- 클로저 안에 변수를 넣어 직접 접근하는 것을 막을 수 있음(은닉)
- 클로저는 각자의 환경을 가짐 === 메모리가 소모됨
- 클로저 사용이 끝나면 참조를 제거하는 것이 좋음
 
## Call & Apply & Bind
### Call
```js
fun.call(thisArg[, arg1[, arg2[, ...]]])
```
- parameters : fun -> 가져다쓸 메소드 ;; thisArg ->this로 사용될 객체;; arg1,arg2,.. -> 메소드에 전달할 인자 목록
- call()을 사용하면 this는 thisArg를 가리키지만 전달하지않으면 전역객체
- this를 특정값으로 지정가능

### Apply
```js
fun.apply(thisArg[, argsArray])
```
- parameters : fun -> 가져다쓸 메소드 ;; thisArg -> 현재 객체로 사용될 객체;; argsArray -> 함수에 전달할 인수 집합, 배열로 전달(call은 인수로,apply는 배열로)
- 메소드를 호출하는 주체는 함수, this를 특정 객체에 바인딩 할 뿐 본질적인 기능은 함수 호출

### Bind
- 원하는 Function 에 인자로 넘긴 this가 바인딩된 새로운 함수를 리턴
- default parameters 를 가진 함수 생성 가능
- call, apply는 즉시 함수를 호출 / bind는 나중에 실행될 함수를 호출하기 위한 올바른 컨텍스트를 갖는 함수를 반환
- 비동기 콜백/이벤트에서 유지 관리
- 특정함수에 대해 원본 함수와 동일한 본문을 갖는 바인딩된 함수를 생성
```js
function Button(content) { 
  this.content = content;
};
 
Button.prototype.click = function() {
  document.write(this.content + ' clicked');
};
 
var myButton = new Button('OK');
myButton.click(); // OK clicked
 
var looseClick = myButton.click;
looseClick(); // undefined clicked
 
var boundClick = myButton.click.bind(myButton);
boundClick(); // OK clicked
```
- 9행 에서 만든 객체는 10행에서 실행했을때 정상출력
- 12행에서 looseClick에 담고 실행하면, 12행에서 이미 이벤트가 종료되어 undefined
- bind 메소드를 사용하면 원본 함수와 동일한 본문을 가지는 함수를 만들어, 16행에서 실행했을경우 정상 출력
- bind를 사용할 경우 나중에 인자값을 추가 가능하며 이인자는 원래 함수의 매개변수로 전달
- 모든 추가된 매개변수는 바인딩된 매개변수 다음에 전달

[참고]
- https://poiemaweb.com/js-function
- https://hyunseob.github.io/2016/08/30/javascript-closure/
- https://poiemaweb.com/js-closure
- https://jundol.kr/9
- https://ibrahimovic.tistory.com/29
- https://poiemaweb.com/js-this
- https://blog.weirdx.io/post/3214
- https://jess2.tistory.com/118