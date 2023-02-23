객체 리터럴을 사용하여 객체를 생성하는 방식과 생성자 함수를 사용하여 객체를 생성하는 방식과의 장단점!

## Object 생성자 함수

new 연산자와 함께 object 생성자 함수를 호출하면 빈 객체를 생성하여 반환한다. 빈 객체를 생성항 이후 프로퍼티 또는 메서드를 추가하여 객체를 완성할 수 있다.
```
// 빈 객체의 생성
const person = new Object();

// 프로퍼티 추가
person.name = 'Lee';
person.sayHello = function () {
	console.log('Hi! My name is ' + this.name);
};

console.log(person); // {name: "Lee", sayHello: f}
person.sayHello(); // Hi! My name is Lee
```
_**생성자 함수**_란 new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수를 말한다. 생성자 함수에 의해 생성된 객체를 인스턴스라 한다.

> 자바스크립트는 Object 생성자 함수 이외에도 String, Number, Boolean, Function, Array, Date, RehExp, promise 등의 빌트인 생성자 함수를 제공한다.

```
// String 생성자 함수에 의한 String 객체 생성
const strObj = new String('Lee');
console.log(typeof strObj); // object
console.log(strObj); // String {"Lee"}

// Number 생성자 함수에 의한 Number 객체 생성
const numObj = new Number(123);
console.log(typeof numObj); // object
console.log(numObj); // Number {123}

// Boolean 생성자 함수에 의한 Boolean 객체 생성
const boolObj = new Boolean(true);
console.log(typeof boolObj); // object
console.log(boolObj); // Boolean {true}

// Function 생성자 함수에 의한 Function 객체(함수) 생성
const func = new Function('x', 'return x * x');
console.log(typeof func); // function
console.log(func); // f anonymous(x)

// Array 생성자 함수에 의한 Array 객체(배열) 생성
const arr = new Array(1, 2, 3);
console.log(typeof arr); // object
console.log(arr); // [1, 2, 3]

//RegExp 생성자 함수에 의한 RegExp 객체(정규 표현식) 생성
const regExp = new RehExp(/ab+c/i);
console.log(typeof regExp); // object
console.log(regExp); // /ab+c/i

// Date 생성자 함수에 의한 Date 객체 생성
const date = new Date();
console.log(typeof date); // object
console.log(date); // (대한민국 표준시)
```
반드시 Object 생성자 함수를 사용해 빈 객체를 생성해야 하는 것은 아니다. 객체를 생성하는 방법은 객체 리터럴을 사용하는 것이 더 간편하다.

### 생성자 함수에 의한 객체 생성 방식의 장점
생성자 함수에 의한 객체 생성 방식은 마치 객체(인스턴스)를 생성하기 위한 템플릿(클래스)처럼 생성자 함수를 사용하여 프로퍼티 구조가 동일한 객체 여러 개를 간편하게 생성할 수 있다.
```
// 생성자 함수
function Circle(radius) {
	// 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
    this.radius = radius;
    this.getDiameter = function () {
    	return 2 * this.radius;
    };
}

// 인스턴스의 생성
const circle1 = new Circle(5); // 반지름이 5인 Circle 객체를 생성
const circle2 = new Circle(10); // 반지름이 10인 Circle 객체를 생성

console.log(circle1.getDiameter()); // 10
console.log(circle2.getDiameter()); // 20
```
#### this
> this는 객체 자신의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수다. this가 가리키는 값, 즉 this바인딩은 함수 호출 방식에 따라 동적으로 결정된다.
- 일반 함수로서 호출 => 전역 객체
- 메서드로서 호출 => 메서드를 호출한 객체(마침표 앞의 객체)
- 생성자 함수로서 호출 => 생성자 함수가 (미래에) 생성할 인스턴스
>>```
function foo() {
	console.log(this);
}
// 일반적인 함수로서 호출
// 전역 객체는 브라우저 환경에서는 window, Node.js 환격에서는 global을 가리킨다.
foo(); // window
const obj = { foo }; // ES6 프로퍼티 축약 표현
// 메서드로서 호출
obj.foo(); // obj
//생성자 함수로서 호출
const inst = new foo(); // inst
```