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
    

# Modern Java ( -> java8 )
- 함수형 패러다임 도입
- 여러가지 프로그래밍 모델 도입
- 쉬운 동시성 도입
- 모듈성 강화
- 개발자 편의 API 추가

## 함수형
- 함수를 일급 시민에 포함
- 익명 클래스의 번거로움을 람다로 간편하게, 메서드 참조로 재사용
- 코드 블록을 주입하고 조합할 수 있게 됨
- 스트림 기반, 병렬처리와 조합
- 주요 패키지 클래스
    - Consumer, Supplier, Function, Predicate...
    - Operator
    - @FunctionallInterface
    - java.util.function
- 주요 인터페이스와 용례 - 함수형이 적합한 곳 vs 아닌 곳
- Predicate - test 메서드, true/false 반환
    - 조합 - and, or, not, negate
    - Us Case: 필터, 실행 결과만 확인할 때, stream.filter
- Function - apply 메서드, 인자와 리턴 존재, 여러 용도로 사용
    - 조합 - andThen, compose
    - Use Case - 범용적, stream.map

## 람다, 메서드 참조
- 람다 - 익 명함수, 익명 클래스 대체
- 메서드 참조 - 메서드나 생성자 참조하기 (`::`)

## 스트림
- 컬렉션 + 함수형, 데이터 처리 연산을 지원하도록 소스에서 추출된 연속된 요소
- 내부 순환(외부순환=for, while...), VM 니가 알아서 해라
- SQL처럼 선언형 스타일로 데이터 처리
- 쉽게 병렬처리 적용 - parallelStream 메서드
- 주요 패키지, 클래스, 메서드
    - java.util.stream, BaseStream, Stream
    - map(), filter(), reduce(), min()....
    - C.stream(), C.parallelStream()...
