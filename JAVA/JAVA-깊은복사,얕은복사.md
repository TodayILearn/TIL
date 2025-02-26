# TIL: Java의 얕은복사(Shallow Copy)와 깊은복사(Deep Copy)

## 개념 요약

- **얕은복사(Shallow Copy)**: 객체의 참조값만 복사되어 원본과 복사본이 같은 메모리 주소를 가리킴
- **깊은복사(Deep Copy)**: 객체의 실제 값을 새로운 메모리 공간에 복사하여 원본과 복사본이 독립적으로 존재함

### 얕은복사(Shallow Copy)

- 단순 대입 연산자(`=`)를 사용하면 얕은복사가 발생
- 원본 객체와 복사된 객체가 동일한 메모리를 참조
- 한쪽 객체의 값을 변경하면 다른 쪽도 함께 변경됨
- 예시:

```java
//생성자 얕은복사
void shallowCopy() {
    Person person = new Person("강동훈", 22);
    Person copyPerson = person;

    copyPerson.setName("강동석");
    copyPerson.setAge(28);
```

```java
ArrayList<String> copied = original; // 얕은복사
int[] copied = original; // 배열의 얕은복사
```

### 깊은복사(Deep Copy)

- 객체의 데이터 자체를 새로운 메모리 공간에 복사
- 원본과 복사본이 서로 독립적으로 존재
- 한쪽 객체의 값을 변경해도 다른 쪽에 영향을 주지 않음

### 컬렉션의 깊은복사

- `생성자`를 이용한 복사

```java
ArrayList<String> copied = new ArrayList<>(original);
```

- 복잡한 객체의 경우

  - `clone() 메소드 오버라이드`
  - `직렬화(Serialization)` 활용
  - `복사 생성자` 구현

## 배열의 깊은복사 방법

- `for 루프` 사용

```java
int[] copied = new int[original.length];
for (int i = 0; i < original.length; i++) {
    copied[i] = original[i];
}
```

- `clone()메소드` 사용

```java
int[] copied = original.clone();
```

- `System.arraycopy() 메소드` 사용

```java
int[] copied = new int[original.length];
System.arraycopy(original, 0, copied, 0, original.length);
```

- `Arrays.copyOf() 메소드` 사용

```java
int[] copied = Arrays.copyOf(original, original.length);
```

## 다차원 배열의 깊은복사

- 단순 clone()은 1차원 깊은복사만 수행
- 다차원 배열은 각 차원마다 복사 필요

```java
int[][] copied = new int[original.length][];
for (int i = 0; i < original.length; i++) {
    copied[i] = original[i].clone();
}
```

# 발견한 문제점

- 프로젝트 중 다차원 배열 데이터가 의도치 않게 변경되는 문제 발생
- 원인 분석 결과, clone()만 사용하여 얕은복사가 수행되고 있었음
- 객체 배열에서 참조 타입의 요소들이 제대로 복사되지 않는 문제 발견

# 해결 방법

- 각 차원별로 명시적인 복사 로직 구현
- 복잡한 객체의 경우 clone() 메소드를 오버라이드하여 깊은복사 구현
- 컬렉션의 경우 스트림 API를 활용한 깊은복사 적용

```java
List<MyObject> copied = original.stream()
    .map(obj -> obj.clone())
    .collect(Collectors.toList());
```

# 생각해볼 점

- 성능과 메모리 사용의 트레이드오프: 깊은복사는 메모리를 더 사용하지만 안전성 확보
- 불변(immutable) 객체 활용을 통한 복사 문제 회피 가능성 검토
- 어떤 상황에서 얕은복사가 더 효율적인지 고려하기
- 프레임워크나 라이브러리의 복사 메커니즘에 대한 이해 필요
- 향후 객체 설계 시 복사 방식을 명확히 문서화하는 습관 들이기
