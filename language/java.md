## lombok

- @Builder
    - 객체 생성할 때 파라미터 순서 상관 안써도 된다.

## Optional
- 존재할수도 있지만 안 할 수도 있는 객체 즉 null이 될 수 있는 객체를 감싸고 있는 래퍼 클래스이다. (Java8에서 추가)
- 효과
    - NPE를 유발할 수 있는 null을 직접 다루지 않아도 됨
    - 수고롭게 null 체크를 직접하지 않아도 됨
    - 명시적으로 해당 변수가 null일 수도 있다는 것을 표현할 수 있음

### 선언하기
```java
Optional<Order> maybeOrder;
Optional<Member> optMember;
```
- 변수명은 클래스 이름을 사용하기도 하지만 `maybe`나 `opt`같은 접두어를 붙여서 Optional 타입의 변수라는 것을 좀 더 명확히 나타내기도 함

### 생성하기
- `Optional.empty()`
    - null을 담고 있는 . 한마디로 비어있는 Optional 객체를 얻어옴, 싱글턴 인스턴스
- `Optional.of(value)`
    - null이 아닌 객체를 담고 있는 Optional 객체를 생성, null이 넘어올 경우, NPE를 던지기 때문에 주의해야 함
- `Optional.ofNullable(value)`
    - null인지 아닌지 확신할 수 없는 객체를 담고 있는 Optional 객체를 생성
    - 위의 두개의 메소드를 합쳐놓은 메소드라고 생각하면 됨 다만 null이 넘어올 경우 NPE를 던지지 않고 비어 있는 Optional 객체를 얻어옴

### 객체 접근하기
- `get()`
    - Optional로 감싼 객체를 반환함
    - 비어있는 Optional 객체에 대해서 `NoSuchElementException`을 던짐
- `orElse(T other)`
    - 비어있는 Optional 객체에 대해서, 넘어온 인자를 반환
- `orElseGet(Supplier<? extends T> other)`
    - 비어있는 Optional객체에 대해서, 넘어온 함수형 인자를 통해 생성된 객체를 반환, `orElse()`의 게으른 버전
    - 비어있는 경우에만 함수가 호출되기 때문에 `orElse(T other)` 대비 성능상 이점을 기대할 수 있음
- `orElseThrow(Supplier<? extends X> exceptionSupplier)`
    - 비어있는 Optional객체에 대해서, 넘어온 함수형 인자를 통해 생성된 예외를 던짐
    