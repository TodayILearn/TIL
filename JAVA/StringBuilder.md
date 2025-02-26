#StringBuilder

## 1. StringBuilder를 사용하는 이유

`String`을 **불변(immutable)** 객체라고 한다. 
즉, String 객체는 한 번 생성되면 변경할 수 없다. 문자열을 + 연산자를 사용하여 연결하면, 연결할 때마다 새로운 문자열 객체가 생성되고, 이전에 있던 문자열은 JVM의 GC가 처리하게 된다.

따라서, String 객체와 String 객체를 더하는 행위는 메모리 할당과 메모리 해제를 발생시키며 더하는 연산이 많아진다면 성능적으로 좋지 않다.

**StringBuilder가 등장하게 된 배경:**

위와 같은 문제점을 해결하기 위해 `StringBuilder`가 등장하게 되었다. StringBuilder는 String과 다르게 **mutable**한 성질을 가지고 있다. 즉, 값이 변할 수 있다는 것이다.
`StringBuilder`는 String과 기존의 데이터를를 수정하는 방식을 사용하기 때문에 속도도 빠르며 상대적으로 부하가 적다.

### StringBuffer vs StringBuilder
 `StringBuffer`는 **thread-safe**하도록 설계되어 멀티 스레드 환경에서 안전하게 문자열을 조작할 수 있다는 장점이 있었습니다. 하지만 `StringBuffer`의 thread-safe 기능은 **동기화(synchronized) 처리**를 포함하며, 이는 싱글 스레드 환경에서는 불필요한 성능 오버헤드를 발생시키는 문제점이 있다.

대부분의 Java 프로그램은 싱글 스레드 환경에서 실행되거나, 문자열 조작이 특정 스레드 내에서만 이루어지는 경우가 많다. 이러한 상황에서 `StringBuffer`의 thread-safe 기능은 오히려 성능 저하의 원인이 된다.

따라서, **싱글 스레드 환경에서의 문자열 처리 성능을 향상**시키기 위해 `StringBuilder`가 도입되었고, `StringBuilder`는 `StringBuffer`에서 thread-safe 기능을 제거하여 동기화 오버헤드를 없애고, **더욱 빠른 성능**을 제공한다.

### 2. StringBuilder의 주요 특징 및 메서드

*   **Mutable (변경 가능):** `StringBuilder` 객체는 생성 후에도 내용을 변경할 수 있습니다.
*   **Not Thread-safe (스레드 안전 X):** `StringBuilder`는 동기화 처리가 되어 있지 않아 thread-safe하지 않습니다. **싱글 스레드 환경에서 사용**하는 것이 권장됩니다.
*   **높은 성능 (싱글 스레드):** 동기화 오버헤드가 없어 `StringBuffer`에 비해 싱글 스레드 환경에서 더 빠른 성능을 제공합니다.
*   **주요 메서드 (StringBuffer와 거의 동일):**

    *   **`append(String str)`:** 문자열을 `StringBuilder` 객체 뒤에 추가합니다.
    *   **`insert(int offset, String str)`:** 특정 위치(`offset`)에 문자열을 삽입합니다.
    *   **`delete(int start, int end)`:** 특정 범위(`start`부터 `end` 이전까지)의 문자들을 삭제합니다.
    *   **`replace(int start, int end, String str)`:** 특정 범위의 문자들을 주어진 문자열로 치환합니다.
    *   **`substring(int start)` / `substring(int start, int end)`:** 부분 문자열을 추출합니다. (새로운 `String` 객체 반환)
    *   **`reverse()`:** 문자열의 순서를 뒤집습니다.
    *   **`length()`:** 문자열의 길이를 반환합니다.
    *   **`capacity()`:** 현재 할당된 buffer의 크기를 반환합니다.
    *   **`toString()`:** `StringBuilder` 객체의 내용을 `String` 객체로 변환하여 반환합니다.

### 3. StringBuilder 사용 예제 코드

```java
public class StringBuilderExample {
    public static void main(String[] args) {
        // StringBuilder 객체 생성
        StringBuilder sb = new StringBuilder("Hello");
        System.out.println("Initial StringBuilder: " + sb); // Hello

        // append() 메서드 사용
        sb.append(" World");
        System.out.println("After append: " + sb); // Hello World

        // insert() 메서드 사용
        sb.insert(5, ",");
        System.out.println("After insert: " + sb); // Hello, World

        // delete() 메서드 사용
        sb.delete(5, 7); // ", " 삭제
        System.out.println("After delete: " + sb); // Hello World

        // replace() 메서드 사용
        sb.replace(0, 5, "Hi");
        System.out.println("After replace: " + sb); // Hi World

        // reverse() 메서드 사용
        sb.reverse();
        System.out.println("After reverse: " + sb); // dlroW iH

        // toString() 메서드 사용 (String으로 변환)
        String result = sb.toString();
        System.out.println("ToString: " + result); // dlroW iH
    }
}
```
## 느낀점
1. 문자열 변경이 별로 없다면 String 사용
2. 문자열 변경이 잦고, 멀티쓰레드 환경이면 StringBuffer 사용 권장
2. 문자열 변경이 잦고, 멀티쓰레드 환경 아니면 StringBuilder 사용 권장