# 3주차
##  JavaScript Standard built-in Objects(표준내장객체)
- *표준 내장객체와 전역객체를 헷갈리지 않는다
- 전역범위의 여러 객체 
- 전역객체는 전역범위에서  this(엄격모드를 사용하지않을때), 지원하는 환경에선 globalThis를 사용해 접근 할 수 있음
- 완전히 새로운 사용자 정의객체 생성 가능
- 내장객체에 일부를 수정하여 사용자 정의 객체 생성 가능==> 사용자정의객체 
- (ex)배열의 확장
```js
var arr = new Array('Seoul', 'New York', 'Ladarkh', 'Pusan', 'Tsukuba');
function getRandomValueFromArray(arr){

  // arr 안에 있는 값들을 임의로 출력...
  // 정수 출력....

  var index = Math.floor( arr.length * Math.random() );  // floor 소수점 숫자를 제거..
  return arr[index];
}
console.log(getRandomValueFromArray(arr));
```
#### 전역범위
전역객체와 전역객체가 상속한 속성으로 이루어짐

### 항목별 표준 객체
1. 값 속성
간단한 값을 반환, 속성이나 메서드를 가지고 있지 않음
- Infinity
- NaN
- undefined
- null(리터럴)
- globalThis

2. 함수속성
객체에 붙지 않고 전역으로 호출하는 함수, 반환값을 호출자에게 바로 반환
- eval()
- uneval()
- isFinite()
- isNaN()
- parseFloat()
- parseInt()
- decodeURI()
- decodeURIComponent()
- encodeURI()
- encodeURIComponent()
- escape() 
- unescape() 

3. 기초객체
다른 모든객체에 기반이되는 기초,기본객체.일반객체, 함수, 오류를 나타내는 객체 포함
- Object
- Function
- Boolean
- Symbol
- Error
- EvalError
- InternalError
- RangeError
- ReferenceError
- SyntaxError
- TypeError
- URIError

4. 숫자 및 날짜
숫자, 날짜,수학계산 기본 객체
- Number
- Math
- Date

5. 텍스트 처리
문자열을 나타내는 객체, 조작방법 제공
- String
- RegExp

6. 인텍스 있는 컬렉션
인덱스 값으로 정렬된 데이터 컬렉션, 배열(형식배열 포함), 배열형 객체 포함
- Array
- Int8Array
- Uint8Array
- Uint8ClampedArray
- Int16Array
- Uint16Array
- Int32Array
- Uint32Array
- Float32Array
- Float64Array

7. 키 있는 컬렉션
키를 사용하는 컬렉션, 삽입순서로 순회할 수 있는 요소 포함
- Map
- Set
- WeakMap
- WeakSet

8. 구조화된 데이터
구조화된 데이터 버퍼 및 JSON을 사용하여 작성한 데이터와 상호작용
- ArrayBuffer
- SharedArrayBuffer 
- Atomics 
- DataView
- JSON

9 제어 추상화 객체섹션
- Promise
- Generator
- GeneratorFunction
- AsyncFunction 

10.리플렉션섹션
- Reflect
- Proxy

11. 국제화섹션
ECMAScript 코어에 추가된 언어 구분 기능
- Intl
- Intl.Collator
- Intl.DateTimeFormat
- Intl.ListFormat
- Intl.NumberFormat
- Intl.PluralRules
- Intl.RelativeTimeFormat
- WebAssembly섹션
- WebAssembly
- WebAssembly.Module
- WebAssembly.Instance
- WebAssembly.Memory
- WebAssembly.Table
- WebAssembly.CompileError
- WebAssembly.LinkError
- WebAssembly.RuntimeError

12. 기타섹션
- arguments


## JavaScript에서의 Object
- 자바스크립트는 프로토타입기반 객체 지향 언어 임
- 함수, 데이터, 변수 모두 객체
- 모든것을 객체를 통해 참조하여 값으로 처리 가능
- 가장 기본적인 형채를 가지고 있는 객체, 아무것도 상속받지않는 순수한 객체
- 값을 저장하는 가장 기본적인 단위
- 모든 객체는 Object객체를 상속
- 모든 객체는 Object객체의 프로퍼티를 가지고 있음
- Object 객체를 확장 -> 모든 객체 접근 가능 API 만들수 있음 but, 모든 객체에 영향을 줄 수있는 리스크.
- 코어객체, 내장객체, 네이티브 객체로 구분
- 특별히 선언 또는 정의하지 않고 바로 이용 가능

#### 호스트객체(host object)
- 실행 환경마다 다르게 덧붙여 존재
- 주로 웹브라우저 확장에 사용
- 클라이언트 측 웹브라우저 가동시 자동으로 생성되는 전역객체, 동적접근 가능

#### 프로토타입 객체(부모 객체)
- 객체 지향 상속 개념 : 모든 객체는 자신의 부모 역할을 하는 프로토 타입 객체를 가르키는 프로퍼티를 갖고 있음
- 정의 하지 안더라도 사용가능
- 생성된 인스턴스가 부모로부터 프로토타입 객체를 상속 받고 있음

#### 프로토 타입 체인
- JS 내의 모든 객체는 부모객체와 연결
- 내부프로퍼티 [[Prototype]],__proto__를 가지고 있음
- 어떤 객체의 __proto__ 프로퍼티는 그객체에게 상속해준 부모 객체를 가리킴

### 객체의 활용 
1. 객체의 형태
- 각 다른 형태 데이터 => 이름(키), 값에 의해 한쌍으로 묶은 복합 데이터
2. 객체의 생성, 저장, 접근
- 생성 : '객체 리터럴', '생성자(Consructor)'로 생성가능
- 저장 : 변수, 프로퍼티등 다양한 곳에 저장 가능
- 접근 : 점 접근(.), 대괄호접근([])에 의해 내부객체 접근 가능
3. 객체 길이 확인
- Object.keys(객체명).length
4. 객체 내 프로퍼티의 열거 방법
- for/in 문
- Object.keys 메소드
- Object.getOwnPropertyNames 메소드




[참고]
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects,https://bravesuccess.tistory.com/20,https://codinghub.tistory.com/46,http://www.ktword.co.kr/abbr_view.php?nav=&m_temp1=1455&id=658