# 개발 용어
개발 용어 정리와 개념 설명

## 호이스팅
> 호이스팅의 개념     
함수 안에 있는 선언들을 모두 해당 함수 유효 범위의 최상단으로 끌어올려 선언하는것을 말한다.

### 호이스팅이란
* 자바스크립트 함수는 실행 되기 전 함수 안에 필요한 변수들을 모두 모아서 **함수 유효 범위** 최상단으로 끌어올려서 선언한다.
* 자바스크립트 파서가 함수가 실행되기 전 함수 내부를 한 번 훑어서 존재하는 변수/함수선언에 대한 정보를 기억하고 있다가 할당한다.
* **함수 유효 범위** 함수 블록 {} 안에서 유효

### 호이스팅 대상자
* var 변수 선언과, 함수 선언문에서만 호이스팅이 일어난다.
* var 변수와 함수 선언문만 위로 끌어올려지고 **할당**을 끌어올려지지 않는다
* let, const 변수 선언과, 함수 표현식은 호이스팅이 발생되지 않는다.

### 호이스팅 예제
```js
function hoisting(){
  var a = inner();

  console.log(typeof a);
  console.log(a);

  function inner(){
    return 'inner value'
  }
  /** 내부 호이스팅 결과
   * var a;
   * function inner(){
   *  retunr 'inner value'
   * }
   * a = inner();
   * console.log(typeof a)
   * console.log(a)
   * 
   * */
}
for (var i = 0; i < 5; i++) setTimeout(() => console.log(i)) // for문 동기, setTimeout 비동기 - var i 가 전역변수로 선언되어서 for문 먼저 실행되면서 var i 값 5로 변경되고, 그다음 settimout이 실행된다.
for (var i = 0; i < 5; i++) setTimeout((i) => console.log(i), 0, i);
```
```js
a 
var a;
// undefined

b 
let b;
// VM263:1 Uncaught ReferenceError: b is not defined
```

-----

## 스코프
### 스코프란?
스코프는 우리말로 번역하면 `범위`라는 뜻이다.     
즉 변수에 접근할 수 있는 범위({})를 뜻한다. (유효범위)

### 스코프 타입
스코프에는 전역(global), 지역(local) 스코프가 있다.     
변수가 전역 스코프에 선언되어 있으면 어디서든 해당 변수에 접근 할 수 있다.     
지역 스코프는 해당 지역 범위에서 선언된 변수만 접근할 수 있으며, 다른 곳에서는 접근 할 수 없다.

-----

## 어휘 스코프 (Lexical Scope)
### 어휘 스코프란? 
함수를 호출 할 때, 호출한 위치가 아닌 선언 된 위치(스코프)에서 참조할 수 있는 변수를 사용하는 방식이다.       

함수를 어디서 선언하였는지에 따라 상위 스코프를 결정하는 것이다. 여기서 중요한 점은 함수를 호출 할 때가 아니라 **선언**에 따라 결정된다.     
코드가 적힌 순간 변수의 유효범위가 정해지는데 이것을 정적 유효범위 (정의된 시점에서의 유효범위)

### 어휘 스코프 예제
```js
var number = 1;
function a(){
  var number = 10;
  b();
}
function b(){
  console.log(number) // 선언한 순간 number의 유효범위는 전역 스코프로 정해짐
}
a(); // 1
b(); // 1
```
b() 함수 안의 number는 a() 함수 안의 지역변수 number가 아니라 전역변수 number를 가리킵니다.     
함수를 처음 선언하는 순간, 함수 내부의 변수는 자기 스코프로부터 가장 가까운 곳에(상위 스코프)에 있는 변수를 계속 참고하게 됩니다. 위의 예시에서는 b 함수 안의 number는 선언 시 가장 가까운 전역 변수 number를 참조하게 됩니다. 그래서 a 함수에서 b 함수를 호출해도 number 변수가 a 함수의 지역변수 number가 아니라 그대로 전역번수 number 값이 나옵니다.

-----

## 동적 스코프 (다이나믹 스코프)
함수 호출한 위치를 변수를 참조 할 스코프로 결정하는 방식

-----

## 자유변수
자유 변수라는 용어는 지역변수 나 해당 함수의 매개변수가 아닌 함수 에서 사용되는 변수를 나타냅니다.     
스코프 범위 (자기 스코프 제외) 에서 참조 할 수 있는 변수를 자유변수 (부모 스코프에서 참조 가능한 변수, 전역변수)

-----

## 일급 객체 함수 (first-class functions)
> 다른 객체들에 일반적으로 적용 가능한 연산을 모두 지원하는 객체를 가리킨다. 보통 함수에 매개변수로 넘기기, 수정하기, 변수에 대입하기와 같은 연산을 지원할 때 일급 객체 - 위키백과
일급 객체의 조건은 1. 변수에 할당할 수 있다.(함수 표현식) 
일급 객체 결과 1. 다른 함수를 인자로 전달 받는다. 2. 다른 함수의 결과로서 리턴 될 수 있다.
함수를 데이터(string, number, boolean, array, object...) 다루듯이 다룰 수 있다. 

-----

## 고계함수(고차함수) (higher-order-functions)
함수를 매개변수로 받거나 함수를 리턴하는 함수를 말한다.

### 일급 객체&고계함수 예제
```js
function sum(number){
  return number+number
}
function resultSum(f, number){
  return f(number);
}
const result = resultSum(sum, 10);
```

-----

## 클로저
일급 객체 함수의 개념을 이용하여 함수 스코프에 묶인 변수(자유변수)를 참조, 할당 하기 위한 일종의 기술이다. (자유변수랑 자유변수를 사용하는 함수를 묶는 기술)      
클로저 기술을 사용하는 함수도 클로저라고 칭한다. (자유변수를 참조하는 함수)
> 일급 객체 함수란? 함수에 매개변수로 넘기기, 수정하기, 변수에 대입하기와 같은 연산을 지원할 때 일급 객체라고 한다.

-----

## 의존성 주입 (DI)
### 의존성이란?
```js
class App {
  coffee;
  constructor(){
    this.coffee = new Coffee();
  }
  drinking(){
    this.coffee.drink();
  }
}
```

위 코드를 보면 `App` 클래스에서 `drinking` 함수를 호출하기 위해선 `Coffee` 클래스가 필요로 한다.     
이것을 **App 클래스는 Coffee 클래스의 의존성을 가진다** 라고 한다. 위와 같이 코드가 설계되었을 때 `Coffee` 클래스가 수정되었을 때 `App` 클래스도 함께 수정해줘야 하는 문제가 발생된다. 결합도(coupling) 즉 의존도가 높아지게 된다.     
또 Coffee 클래스의 상속을 받아 다른 클래스를 사용해야 한다면 `App` 클래스 안에서 직접 다른 클래스로 수정해야 한다.

### 의존성 주입 이용
> 하나의 객체가 다른 객체의 의존성을 제공하는 테크닉이다.

[TypeScript와 typedi로 의존성 주입 이해하기](https://medium.com/@HoseungJang/typescript%EC%99%80-typedi%EB%A1%9C-%EC%9D%98%EC%A1%B4%EC%84%B1-%EC%A3%BC%EC%9E%85-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-5d83ef1977f9)

**의존성**은 예를 들어 서비스로 사용할 수 있는 객체이다. 클라이언트가 어떤 서비스를 사용할 것인지 지정하는 대신, <U>클라이언트에게 무슨 서비스를 사용할 것인지를 말해주는 것.</U>     
**주입**은 의존성(서비스)를 사용하는 객체(클라이언트)로 전달하는 것     

의존성 주입의 의도는 객체의 생성과 사용을 분리하여 가독성과 코드 재사용을 높혀준다. 어떤 서비스를 호출하려는 클라이언트는 그 서비스가 어떻게 구성되었는지 알지 못해야 한다.

```js
class App {
  coffee;
  constructor(coffee){
    this.coffee = coffee;
  }
  drinking(){
    this.coffee.drink();
  }
}
```
위와 같이 의존하는(필요한) 클래스를 직접 생성하는 것이 아닌 생성자로 주입시켜서 객체 간의 결함도(의존도)를 줄이고 좀 더 유연한 코드로 작성할 수 있다.
**한 클래스를 수정했을 때, 다른 클래스로 수정해야하는 상황**을 막아줄 수 있다.
