# 호이스팅이란?

> 호이스팅(Hoisting)은 JavaScript에서 `변수와 함수의 선언이 스코프(scope)의 최상단으로 끌어올려지는 현상`을 말한다. 이는 코드가 실행되기 전에 JavaScript 엔진이 변수와 함수 선언을 메모리에 먼저 저장하기 때문에 발생함.
> 단, `선언만 끌어올려지고 할당은 원래 위치에 그대로 남아 있음.`

## 호이스팅의 특징

- var로 선언된 변수와 함수 선언식(function declaration)은 호이스팅이 발생함.

- let과 const로 선언된 변수는 호이스팅이 되지만, **TDZ(Temporal Dead Zone)**라는 개념 때문에 선언 전에 접근하면 에러가 발생함.

## 호이스팅의 예시

1. 변수 호이스팅 (var)

```
console.log(x); // undefined
var x = 10;
console.log(x); // 10
```

    - var x; (선언)이 스코프의 최상단으로 끌어올려집니다.

    - console.log(x);는 x가 선언되었지만 값이 할당되지 않았기 때문에 undefined를 출력합니다.

    - x = 10; (할당)이 원래 위치에서 실행됩니다.

    - 두 번째 console.log(x);는 10을 출력합니다.

2. 함수 호이스팅 (함수 선언식)

```
foo(); // "Hello, World!"
function foo() {
    console.log("Hello, World!");
}
```

    - 함수 선언식 function foo()가 스코프의 최상단으로 끌어올려집니다.

    - foo()를 선언 전에 호출해도 정상적으로 동작합니다.

3. 함수 표현식과 호이스팅

```
bar(); // TypeError: bar is not a function
var bar = function() {
    console.log("Hello, World!");
};
```

    - var bar; (선언)이 스코프의 최상단으로 끌어올려집니다.

    - bar();를 호출할 때 bar는 undefined이기 때문에 함수로 호출할 수 없어 에러가 발생합니다.

4. let과 const 호이스팅

```
console.log(y); // ReferenceError: Cannot access 'y' before initialization
let y = 10;
```

    - let y; (선언)이 스코프의 최상단으로 끌어올려지지만, **TDZ(Temporal Dead Zone)**에 들어갑니다.

    - console.log(y);는 TDZ에 있는 y에 접근하려고 하기 때문에 에러가 발생합니다.

## 호이스팅의 문제점

- 예기치 않은 동작: 변수나 함수가 선언되기 전에 사용될 수 있어 코드의 가독성과 예측 가능성이 떨어짐.

  > 예: var로 선언된 변수가 undefined로 초기화되어 예상치 못한 결과를 초래할 수 있음.

- 디버깅 어려움: 호이스팅으로 인해 발생한 오류는 찾기 어려울 수 있음.

- 스코프 혼란: var는 함수 스코프를 가지기 때문에 블록({}) 내에서 선언된 변수가 블록 외부에서도 접근 가능함.

## 해결법

1. let과 const 사용 : let과 const는 블록 스코프를 가지며, TDZ로 인해 선언 전에 접근하면 에러가 발생함.

```
console.log(z); // ReferenceError: Cannot access 'z' before initialization
let z = 20;
```

2. 함수 표현식 사용: 함수 표현식을 사용하면 호이스팅의 영향을 받지 않음.

```
const baz = function() {
    console.log("Hello, World!");
};
baz(); // "Hello, World!"
```

## 느낀점

> let과 const를 사용하고, 함수 표현식을 활용하며, 코드 스타일을 개선하는 것이 호이스팅으로 인한 문제를 해결하는 좋은 방법입니다.
