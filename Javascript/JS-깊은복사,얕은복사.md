# 깊은 복사(Deep Copy)와 얕은 복사(Shallow Copy) in JavaScript

**깊은 복사(Deep Copy)** 와 **얕은 복사(Shallow Copy)** 는 객체를 복사하는 방식에 따라 데이터가 어떻게 복사되는지를 설명하는 개념

---

## 📌 얕은 복사(Shallow Copy)

**얕은 복사**는 원본 객체의 **참조(주소)만 복사**하는 방식입니다. 즉, 복사된 객체와 원본 객체가 **같은 메모리 주소를 공유**합니다.

### 🔹 특징

- **1차원 객체(primitive types)에서는 새로운 객체가 생성됨**.
- **중첩된 객체(nested objects)에서는 원본과 복사된 객체가 참조를 공유**.
- **복사된 객체를 변경하면 원본에도 영향을 줄 수 있음**.

### 🔹 얕은 복사 방법

#### ✅ `Object.assign()`

```javascript
const obj1 = { a: 1, b: 2, c: { d: 3 } };
const obj2 = Object.assign({}, obj1);

obj2.a = 100; // 원본에 영향 없음
obj2.c.d = 999; // 중첩 객체는 참조 공유

console.log(obj1); // { a: 1, b: 2, c: { d: 999 } }
console.log(obj2); // { a: 100, b: 2, c: { d: 999 } }
```

#### ✅ 전개 연산자 (`...`)

```javascript
const obj1 = { a: 1, b: 2, c: { d: 3 } };
const obj2 = { ...obj1 };

obj2.c.d = 999; // 중첩 객체는 참조 공유

console.log(obj1); // { a: 1, b: 2, c: { d: 999 } }
console.log(obj2); // { a: 1, b: 2, c: { d: 999 } }
```

📌 `Object.assign()`이나 `...` 연산자는 1차원 객체는 복사하지만, 중첩 객체는 여전히 참조를 공유함.

---

## 📌 깊은 복사(Deep Copy)

**깊은 복사**는 원본 객체의 **모든 데이터와 중첩 객체까지 완전히 새로운 메모리 공간에 복사**하는 방식입니다.

### 🔹 특징

- **원본 객체와 독립적인 새로운 객체가 생성됨**.
- **중첩 객체를 포함한 모든 데이터를 새로운 메모리 공간에 저장**.
- **복사된 객체를 변경해도 원본 객체에는 영향이 없음**.

### 🔹 깊은 복사 방법

#### ✅ `JSON.parse(JSON.stringify())`

```javascript
const obj1 = { a: 1, b: 2, c: { d: 3 } };
const obj2 = JSON.parse(JSON.stringify(obj1));

obj2.c.d = 999; // 원본 객체는 영향 없음

console.log(obj1); // { a: 1, b: 2, c: { d: 3 } }
console.log(obj2); // { a: 1, b: 2, c: { d: 999 } }
```

#### ✅ `structuredClone()`

```javascript
const obj1 = { a: 1, b: 2, c: { d: 3 } };
const obj2 = structuredClone(obj1);

obj2.c.d = 999;

console.log(obj1); // { a: 1, b: 2, c: { d: 3 } }
console.log(obj2); // { a: 1, b: 2, c: { d: 999 } }
```

#### ✅ `lodash.cloneDeep()`

```javascript
const _ = require("lodash");

const obj1 = { a: 1, b: 2, c: { d: 3 } };
const obj2 = _.cloneDeep(obj1);

obj2.c.d = 999;

console.log(obj1); // { a: 1, b: 2, c: { d: 3 } }
console.log(obj2); // { a: 1, b: 2, c: { d: 999 } }
```

---

## 📌 얕은 복사 vs 깊은 복사 비교

| 비교 항목      | 얕은 복사 (Shallow Copy) | 깊은 복사 (Deep Copy)                 |
| -------------- | ------------------------ | ------------------------------------- |
| 복사 대상      | 최상위 객체만 복사       | 최상위 객체 + 내부 객체까지 모두 복사 |
| 참조 방식      | 원본 객체의 참조 공유    | 새로운 메모리 공간에 독립적 복사      |
| 중첩 객체 변경 | 원본 객체에 영향을 줌    | 원본 객체에 영향을 주지 않음          |
| 속도           | 빠름                     | 상대적으로 느림                       |
| 메모리 사용량  | 적음                     | 많음                                  |

---

# 느낀점

> 중첩 객체가 없는 단순 리스트나 딕셔너리 복사 시 메모리를 절약하고 빠른 복사가 필요할 때 얕은복사 사용
> 중첩된 객체를 포함한 복사본이 필요할 때나 원본 객체와 독립적인 복사본을 만들어야 할 때 깊은복사 사용이 용이할 듯하다.
