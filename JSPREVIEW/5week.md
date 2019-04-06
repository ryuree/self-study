# 5주차
## Class
- 몸통(바디) === {} ,메소드만 정의 가능 / 프로퍼티(인스턴스필드,멤버변수?) 선언하면 에러발생
- 호이스팅 되지않음(선언문 이전에 참조하면 에러)
- 
```js
//클래스 선언방법 예시

class Polygon {
    constructor(height, width) {
        this.height = height;
        this.width = width;
    }//생성자
}
```
- 생성자 : 객체를 생성하고 초기화하는 메소드, class에서 한번만 쓸 수 있음(생략가능/생략하면 클래스에 constructor() {}(빈객체)를 포함한 것과 동일하게 동작)
- 선언과 초기화는 무조건 constructor안에서
- 인스턴스를 통해 외부에서 언제나 참조가능(public)
- 생성자에서 super키워드로 상위 클래스 생성자메소드 호출 가능

### getter
- 접근할때마다 프로퍼티값을 조작하는 행위가 필요할때
- get키워드 사용
- 호출x, 참조형식이며 참조 할때 메소드 호출함
- 무조건 반환하는 값이 있어야 함
```js
class Polygon {
    constructor(height, width) {
        this.height = height;
        this.width = width;
    }//생성자
	
	get thisWidth(){
		return this.width;
	}
}
```

### setter
- 프로퍼티에 값을 할당 할때, 값을 조작하는 행위가 필요할때 사용
- set 키워드 사용
- 프로퍼티 이름처럼 사용, 호출이 아니라 할당하는 형식, 할당할때 메소드 호출x
```js
class Polygon {
    constructor(height, width) {
        this.height = height;
        this.width = width;
    }//생성자
	
	get thisWidth(){
		return this.width;
	}
	
	set thisHeight(){
		return this.width += this.width
	}
}
```

### 정적 메소드
- 정적 메소드는 클래스의 인스턴스가 아닌 클래스 이름으로 호출
- 인스턴스 생성 안해도 호출 가능
- this사용 불가능(정적메소드 내부에서 this는 자기 자신을 가리킴)
```js
class Polygon {
    constructor(height, width) {
        this.height = height;
        this.width = width;
    }//생성자
	
	static staticMethod() {
		return 'staticMethod';
	}

	get thisWidth(){
		return this.width;
	}
	
	set thisHeight(){
		return this.width += this.width
	}
}
```
### 상속
- 유사한 코드가 있으면, 상속을 이용 그대로 사용하고 다른점만 구현하면 됨
#### extends
- 부모(base)클래스에서 자식(sub) 클래스를 정의할때 사용
```js
//예시
//부모
class Circle {
  constructor(radius) {
    this.radius = radius; // 반지름
  }

  // 원의 지름
  getDiameter() {
    return 2 * this.radius;
  }

  // 원의 둘레
  getPerimeter() {
    return 2 * Math.PI * this.radius;
  }

  // 원의 넓이
  getArea() {
    return Math.PI * Math.pow(this.radius, 2);
  }
}

//자식
class Cylinder extends Circle {
  constructor(radius, height) {
    super(radius);
    this.height = height;
  }

  getArea() {
    // (원통의 높이 * 원의 둘레) + (2 * 원의 넓이)
    return (this.height * super.getPerimeter()) + (2 * super.getArea());
  }

  // 원통의 부피
  getVolume() {
    return super.getArea() * this.height;
  }
}
```

#### super
- 부모클래스를 참조,부모클래스의 constructor를 호출할때 사용
- 자식클래스에서 super()호출 안하면, this참조 에러 발생
```js
//부모
class Circle {
  constructor(radius) {
    this.radius = radius; // 반지름
  }

  // 원의 지름
  getDiameter() {
    return 2 * this.radius;
  }

  // 원의 둘레
  getPerimeter() {
    return 2 * Math.PI * this.radius;
  }

  // 원의 넓이
  getArea() {
    return Math.PI * Math.pow(this.radius, 2);
  }
}

//자식
class Cylinder extends Circle {
  constructor(radius, height) {
    // ① super 메소드는 부모 클래스의 인스턴스를 생성
    super(radius);
    this.height = height;
  }

  getArea() {
    // (원통의 높이 * 원의 둘레) + (2 * 원의 넓이)
    // ② super 키워드는 부모 클래스(Base Class)에 대한 참조
    return (this.height * super.getPerimeter()) + (2 * super.getArea());
  }

  // 원통의 부피
  getVolume() {
    // ② super 키워드는 부모 클래스(Base Class)에 대한 참조
    return super.getArea() * this.height;
  }
}
```
#### static,prototype 상속
- 자식클래스 static메소드안에서도 super로 부모클래스 static메소드 호출 가능
- 프로토타입 체인 때문에 참조 가능
- 일반메소드 내부에서는  super()사용해도 부모의 static메소드 호출 불가능 == 자식의 인스턴스는 프로토타입체인때문에 정적메소드 참조불가능
```js
class Parent {
  static staticMethod() {
    return 'Hello';
  }
}

class Child extends Parent {
  static staticMethod() {
    return `${super.staticMethod()} wolrd`;
  }

  prototypeMethod() {
    return `${super.staticMethod()} wolrd`;
  }
}

console.log(Parent.staticMethod()); // 'Hello'
console.log(Child.staticMethod());  // 'Hello wolrd'
console.log(new Child().prototypeMethod()); // TypeError: (intermediate value).staticMethod is not a function
```

[참고]
- https://beomy.tistory.com/15
- https://poiemaweb.com/es6-class