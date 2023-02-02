# Class

## 생성자 함수와 클래스

* JS는 프로토타입 기반의 객체 지향 언어이다.
  * 클래스가 원래 없었다!
  * 하지만 타 언어에서 유입돼서 들어오는 사람들(C, JAVA)을 위해 ES6부터 클래스 도입
* 사실 클래스는 함수
  * 기존 프로토타입 기반 패턴을 클래스 기반 패턴처럼 사용할 수 있도록 하는 문법적 설탕이라 볼 수 있음
* 클래스와 생성자 함수의 차이점
  * 클래스는 new 연산자 없이 호출하면 에러
  * 클래스는 상속을 지원하는 extends와 super 키워드 제공
  * 클래스는 호이스팅이 발생하지 않는 것처럼 동작
  * 클래스 내에는 암묵적으로 strict mode 적용, 해제 불가
  * 클래스의 constructor, prototype method, static method 모두 프로퍼티 어트리뷰트 [[enumerable]] 값이 false → 열거 불가
* 클래스는 생성자 함수보다 좀 더 견고하고 명료
  * 특히 extends, super는 상속 관계 구현을 더욱 간결하고 명료하게 표현
* 따라서 클래스를 단순한 문법적 설탕보다는 새로운 객체 생성 매커니즘으로 보는 것이 좀 더 합당



## 클래스 정의

```JS
// 일반적인 방식
class Person {}

// 표현식으로도 가능하긴 함
const Person = class Person {};
const Person = class MyClass {};
```

* 클래스를 표현식으로 정의 가능 = 값으로 사용할 수 있는 일급 객체
* 클래스가 일급 객체로써 가지는 특징
  * 무명의 리터럴로 생성 가능, 즉 런타임에 생성 가능
  * 변수나 자료구조에 저장 가능
  * 함수 매개변수 전달 가능
  * 함수의 반환값으로 사용 가능
* 클래스 몸체에 정의할 수 있는 메서드는 `constructor(생성자)`, `prototype method`, `static method` 세 가지

```js
class Person {
  // 생성자
  constructor(name) {
    // 인스턴스 생성 및 초기화
    this.name = name;  // name property is public
  }
  
  // prototype method
  sayHi() {
    console.log(`hi! I'm ${this.name}`);
  }
  
  // static method
  static sayHello() {
    console.log('hi?');
  }
}

// create instance
const me = new Person('kong');

// refer property of instance
console.log(me.name);  // kong
// call prototype method
me.sayHi(); // hi! I'm kong
// call static method
Person.sayHello();  // hi?
```

* 이걸 생성자 함수로 만들면?

```js
const Person = (function() {
  function Person(name) {
    this.name = name;
  }
  
  Person.prototype.sayHi = function() {
    console.log(`hi! I'm ${this.name}`)
  }
  
  Person.sayHello = function () {
    console.log('hi?')
  }
  
  return Person;
}());
```

* 토막지식
  * 클래스가 호이스팅 안된다고 했는데 사실 됨 ㅎㅎ
  * 이게 어케되는거냐면 클래스는 let, const 처럼 호이스팅 되는 거임
  * TDZ 때메 호이스팅 안되는 것처럼 보이는거임
  * var, let, const, function, function*, class 키워드 사용해서 선언된 모든 식별자는 호이스팅 되는 거임
  * 모든 선언문은 런타임 이전에 먼저 실행되기 때문



* prototype method
  * 클래스 몸체에서 정의한 메서드는 생성자 함수와 다르게 기본적으로 프로토타입 메서드가 됨
  * 인스턴스는 프로토타입 체인의 일원이 됨
  * 인스턴스는 프로토타입 메서드를 상속받아 사용
* static method
  * 인스턴스를 생성하지 않아도 호출 가능한 메서드
  * 메서드에 `static` 키워드 붙이면 정적 메서드가 됨
  * 클래스에 바인딩
    * 클래스는 함수 객체로 평가되므로 자신의 프로퍼티나 메서드 소유 가능
    * 클래스 정의가 평가되는 시점에 함수 객체가 됨
    * 인스턴스와 달리 별다른 생성과정 불필요
    * 따라서 정적 메서드는 클래스 정의 이후 인스턴스 생성하지 않아도 호출 가능
  * 정적 메서드는 인스턴스로 호출 불가
    * 정적 메서드가 바인딩된 클래스는 인스턴스의 프로토타입 체인상에 존재하지 않기 때문
* prototype/static method 차이점
  * 자신이 속해 있는 프로토타입 체인이 다름 (인스턴스/클래스)
  * 정적 메서드는 클래스로 호출/프로토타입 메서드는 인스턴스로 호출
  * 정적 메서드는 인스턴스 프로퍼티 참조 불가/프로토타입 메서드는 가능
* 인스턴스를 만들지 않고 정적 메서드를 호출할 때 **의미가 명확한 경우**가 있음
  * 정적 팩토리 메서드
  * 



* private 필드 정의 제안
  * JS에서 캡슐화를 구현하는 방법
  * private 필드 선두에 `#`을 붙임
  * 참조할 때도 `#`붙여야함
  * 클래스 내부에서만 참조 가능
  * 반드시 클래스 몸체에 정의해야 함



## 상속

* 프로토타입 기반 상속과 다른 개념
* 프로토타입 기반 상속은 프로토타입 체인을 통해 다른 객체의 자산을 상속받는 개념
* 상속에 의한 클래스 확장은 기존 클래스를 상속받아 새로운 클래스를 확장extends하여 정의하는 것

```js
class Animal {
  constructor(age, weight) {
    this.age = age;
    this.wieght = weight;
  }
  
  eat() { return 'eat'; }
  move() { return 'move'; }
}

// 상속
class Bird extends Animal {
  fly() { return 'fly'; }
}

const bird = new Bird(1, 5);

console.log(bird);  // Bird {age: 1, weight: 5}
console.log(bird instanceof Bird); true
console.log(bird instanceof Animal); true

console.log(bird.eat());  // eat
console.log(bird.move()); // move
console.log(bird.fly());  // fly
```

* 상속을 통해 확장된 클래스: 서브 클래스
* 서브 클래스에 상속된 클래스: 수퍼 클래스



* `super` 키워드

  * 함수처럼 호출할 수도, this와 같이 식별자처럼 참조도 가능한 특수한 키워드

    * 호출하면 - 수퍼클래스의 constructor를 호출
    * 참조하면 - 수퍼클래스의 메서드 호출 가능

  * 서브클래스에서 constructor 생략하면 암묵적으로

    ```js
    constructor(...args) { super(...args); }
    ```

    * 이게 실행됨

  * 주의사항

    * 서브클래스에서 constructor 생략 안하면 반드시 super 호출해줘야함
    * 서브클래스에서 super 호출 이전에 this 참조 불가
    * super는 반드시 서브클래스의 constructor에서만 호출

  * 참조방식은 `super.sayHi()`이런식으로다가