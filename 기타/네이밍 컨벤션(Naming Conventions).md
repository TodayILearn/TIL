# 다양한 네이밍 컨벤션 (Naming Conventions)

가독성과 일관성을 위해 지켜야함.

## 1. 케밥 케이스 (Kebab Case)

- **형식:** 단어를 하이픈(-)으로 연결
- **사용처:** URL, 파일명, CSS 클래스명, HTML 속성 등
- **특징:** 소문자만 사용, 공백 대신 하이픈 사용
- **예시:** `my-profile-page`, `button-primary`

## 2. 카멜 케이스 (Camel Case)

- **형식:** 첫 단어는 소문자로 시작, 이후 각 단어의 첫 글자는 대문자로 표기
- **사용처:** JavaScript 변수명, 함수명, 객체 속성명 등
- **특징:** 첫 글자는 소문자, 단어 구분은 대문자로
- **예시:** `userName`, `getUserData()`

## 3. 파스칼 케이스 (Pascal Case)

- **형식:** 각 단어의 첫 글자를 대문자로 표기
- **사용처:** 클래스명, 타입명, 생성자 함수 등 (Java, C#, TypeScript 등)
- **특징:** 첫 글자도 대문자로 시작
- **예시:** `UserProfile`, `OrderDetails`

## 4. 스네이크 케이스 (Snake Case)

- **형식:** 단어를 언더스코어(\_)로 연결
- **사용처:** 데이터베이스 컬럼명, 파일명, 상수명 등 (Python, Ruby 등)
- **특징:** 소문자 또는 대문자로 사용 (예: `SCREAMING_SNAKE_CASE`)
- **예시:** `user_id`, `file_name`

## 5. 스크리밍 스네이크 케이스 (Screaming Snake Case)

- **형식:** 스네이크 케이스와 동일하지만 모든 글자를 대문자로 표기
- **사용처:** 상수(constant) 정의 시 (예: JavaScript, Python 등)
- **특징:** 대문자만 사용, 단어 구분은 언더스코어
- **예시:** `MAX_LIMIT`, `DEFAULT_CONFIG`

## 6. 플랫 케이스 (Flat Case)

- **형식:** 모든 단어를 소문자로 연결 (공백이나 구분자 없음)
- **사용처:** 간단한 변수명이나 파일명 등
- **특징:** 가독성이 떨어질 수 있음
- **예시:** `userprofile`, `configsettings`

## 7. 코브라 케이스 (Cobra Case)

- **형식:** 단어를 점(.)으로 연결
- **사용처:** 파일 확장자, 패키지명 등
- **특징:** 점을 사용해 단어 구분
- **예시:** `com.example.app`, `org.python.module`

## 8. 트레인 케이스 (Train Case)

- **형식:** 각 단어의 첫 글자를 대문자로 표기하고 하이픈(-)으로 연결
- **사용처:** 파일명, 헤더명 등
- **특징:** 파스칼 케이스와 유사하지만 하이픈 사용
- **예시:** `User-Guide.pdf`, `API-Documentation`

## 9. 헝가리안 표기법 (Hungarian Notation)

- **형식:** 변수명 앞에 데이터 타입을 나타내는 접두사 추가
- **사용처:** C, C++ 등에서 변수명에 타입 정보를 포함할 때
- **특징:** 타입 정보를 명시적으로 표현
- **예시:** `int iAge`, `char* szName`

## 요약

| 케이스 이름                             | 예시                        | 주요 사용처                            | 실제 예시 |
| --------------------------------------- | --------------------------- | -------------------------------------- | --------- |
| **케밥 케이스** (Kebab Case)            | URL, CSS 클래스명           | `my-profile-page`                      |
| **카멜 케이스** (Camel Case)            | JavaScript 변수명, 함수명   | `userName`, `getUserData()`            |
| **파스칼 케이스** (Pascal Case)         | 클래스명, 타입명            | `UserProfile`, `OrderDetails`          |
| **스네이크 케이스** (Snake Case)        | 데이터베이스 컬럼명, 상수명 | `user_id`, `file_name`                 |
| **스크리밍 스네이크 케이스**            | 상수 정의                   | `MAX_LIMIT`, `DEFAULT_CONFIG`          |
| **플랫 케이스** (Flat Case)             | 간단한 변수명               | `userprofile`, `configsettings`        |
| **코브라 케이스** (Cobra Case)          | 파일 확장자, 패키지명       | `com.example.app`, `org.python.module` |
| **트레인 케이스** (Train Case)          | 파일명, 헤더명              | `User-Guide.pdf`, `API-Documentation`  |
| **헝가리안 표기법**(Hungarian Notation) | C, C++ 변수명               | `int iAge`, `char* szName`             |
