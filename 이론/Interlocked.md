## Interlocked
- C#에서 여러 쓰레드가 동시에 공유 변수에 접근할 때 발생할 수 있는 Race Condition을 방지하기 위해 사용되는 클래스이다.
- 이 클래스는 **원자적(Atomic)** 으로 수행되는 연산을 제공합니다.
  - 원자적 연산은 더 이상 쪼갤 수 없는 하나의 단위로 수행되는 연산을 말한다.
  - 연산이 시작되면 중간에 다른 쓰레드가 개입할 수 없고 연산이 끝난 뒤에야 다른 쓰레드가 그 변수에 접근할 수 있다.

### 주요 메서드
- `Increment(ref int location)`: 변수를 원자적으로 1만큼 증가시킨다.
```C#
int counter = 0;
Interlocked.Increment(ref counter);  // counter 값을 원자적으로 1 증가
```

- `Decrement(ref int location)`: 변수를 원자적으로 1만큼 감소시킨다.
```C#
int counter = 10;
Interlocked.Decrement(ref counter);  // counter 값을 원자적으로 1 감소
```

- `Exchange(ref int location, int value)`: 변수의 값을 원자적으로 새 값으로 교체하고 이전 값을 반환한다.
```C#
int oldValue = Interlocked.Exchange(ref counter, 100);  // counter에 100을 설정하고 이전 값을 반환
```

- `CompareExchange(ref int location, int value, int comparand)`: 현재 값이 기대한 값과 같으면 새 값으로 교체하고 그렇지 않으면 아무 작업도 하지 않는다. 이는 비교 후 교환(Compare and Swap) 패턴을 지원한다.
```C#
int result = Interlocked.CompareExchange(ref counter, 100, 50); 
// counter가 50이면 100으로 설정, 아니면 기존 값 유지
```

- `Add(ref int location, int value)`: 변수에 특정 값을 더한다. 더하는 연산도 원자적으로 수행된다.
```C#
int counter = 0;
Interlocked.Add(ref counter, 10);  // counter에 10을 원자적으로 더함
```

### 특징
- lock과 같은 동기화 기법보단 가볍고(경량화된 원자적 연산) 간단하고 효율적인 처리가 가능하다.
- 단순한 연산에만 적합하다. (복잡한 연산, 여러 단계의 작업엔 lock과 같은 강력한 동기화 기법 필요)
