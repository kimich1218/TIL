# 싱글톤 패턴
### 정의
싱글톤 패턴은 객체지향 프로그래밍에서 단 하나의 유일한 인스턴스만 가지도록 하는 패턴이다. 직접적으로 생성자를 호출 할 수 없으며 인스턴스가 하나만 존재하도록 보장한다. 그렇다면 왜 이러한 패턴이 만들어지게 된 것일까?

커넥션 풀, 스레드 풀과 같이 인스턴스를 여러 개 만들면 자원을 사용하지 않을 시 불필요한 자원을 만들게 된다. 이러한 문제점을 해결하기 위해 전역으로 단 하나의 인스턴스만을 생성하고 공유할 수 있도록 이러한 싱글톤 패턴을 사용하는 것이다.

#### 장점
- 유일한 인스턴스: 클래스에서 유일하게 단 하나의 인스턴스 가지므로 객체를 일관되게 유지 할 수 있다.
- 메모리 절약: 단 하나의 인스턴스를 가지는 것은 메모리를 절약하게 된다. 여러 번 호출하더라도 메모리를 점유하지 않게 된다.
- 지연 초기화: 인스턴스가 실행되는 시점에 실행하여 생성하는데 초기 비용을 줄일 수 있다.

#### 단점
- 결함도 증가: 전역에서 하나의 인스턴스에 접근하여 사용하기 때문에 의존 할 경우 결합도가 증가할 수 있다.
- 상태 관리의 어려움: 전역에서 여러 객체가 하나의 인스턴스를 사용하게 되므로 상태가 예상과빗나게 변경될 수 있다.
- 전역에서 접근 가능: 무분별한 사용이 될 수 있다.

### 구현 방법
```java
public class Singleton {
    private static Singleton singleton;

    private Singleton() {}

    public static Singleton getInstance() {
        if (singleton == null) {
            singleton = new Singleton();
        }
        return singleton;
    }
}
```
- singleton은 정적 참조 변수이다.
- 외부에서 객체를 생성할 수 없도록 private으로 선언한다.
- `getInstance()`를 통해서 인스턴스를 생성할 수 있다.
- `getInstance()`를 실행 할 때 초기화한다.

하지만 쓰레드로부터 안전하지 않다는 단점이 있다.
다음은 이를 확인하기 위한 테스트코드이다.
```java
@Test
public void 싱글톤은_안전하지않다() {

    Singleton[] singleton = new Singleton[10];

    ExecutorService service = Executors.newFixedThreadPool(10);

    for (int i = 0; i < 10; i++) {
        final int num = i;
        service.submit(() -> {
            singleton[num] = Singleton.getInstance();
        });
    }

    service.shutdown();

    for(Singleton s : singleton) {
        System.out.println(s.toString());
    }
}

```
![](https://github-production-user-asset-6210df.s3.amazonaws.com/82080962/393696820-9a8618c2-19a9-4bb7-b8d0-5c8689fb768c.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20241209%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20241209T040825Z&X-Amz-Expires=300&X-Amz-Signature=19bdd2d2227247a4573f09efdb24715798818722a440a9b0f270982b4dd17f64&X-Amz-SignedHeaders=host)
이와 같이 싱글톤 패턴으로 객체를 생성하였지만 다른 주소 값을 확인 할 수 있다.
이러한 단점을 막기 위한 여러가지 싱글톤 패턴이 있다.
- synchronized 키워드 사용
    - `@sychronized`를 통해서 `getInstance()`에 하나의 스레드만 접근하도록 하는 방법이다.
    - `Lock`을 진행하기 때문에 성능 저하가 발생할 수 있다.
- eager initialization
    - 변수 선언과 동시에 싱글톤을 초기화하는 것이다.
    - 미리 생성하기 때문에 비용이 커지고 리소스를 사용하지 않으면 자원 낭비가 되는 단점이 있다.
- Doubledchecked locking
    - 참조 주소 객체에 `volatile`와 해당 if문에 `synchronized `를 사용하는 것이다.
    - `Lock`과 `volatile`를 사용하기 때문에 성능 저하가 발생한다.
- Bill Pugh Solution 
  - `private static inner class`를 사용하여 싱글톤 패턴을 구현한 것이다.
- classLoader에 의해 로드 될 때 `synchronized`가 내부적으로 실행된다.





#개발/기타