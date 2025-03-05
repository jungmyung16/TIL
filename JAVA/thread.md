## 1. Thread란?

- **프로그램**: 실행 가능한 코드의 집합
- **프로세스**: 실행 중인 프로그램 (독립된 메모리 공간 할당)
- **스레드(Thread)**: 프로세스 내에서 실행되는 작은 작업 단위 (한 프로세스는 여러 스레드를 가질 수 있음)
- **멀티스레드(Multithreading)**: 여러 개의 스레드를 동시에 실행하여 성능을 향상시키는 기법
- **쉽게 정리하면**: 프로세스는 "음식점", 스레드는 "직원" (직원이 많을수록 일을 빠르게 처리 가능)

## 2. 자바에서 스레드 생성 방법

### (1) Thread 클래스 상속

```java
// Thread 클래스를 상속하여 스레드를 구현하는 방법
class MyThread extends Thread {
    public void run() {
        // 스레드가 실행될 때 수행할 작업 정의
        for (int i = 0; i < 5; i++) {
            System.out.println("Thread: " + i);
            try {
                Thread.sleep(500); // 0.5초 동안 스레드 일시 정지
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class ThreadExample {
    public static void main(String[] args) {
        MyThread t = new MyThread(); // 스레드 객체 생성
        t.start(); // 새로운 스레드 시작
    }
}
```

- `run()` 메서드: 스레드 실행 코드 작성
- `start()`: 새로운 스레드 시작 (직접 `run()`을 호출하면 멀티스레드가 아님)

### (2) Runnable 인터페이스 구현

```java
// Runnable 인터페이스를 구현하여 스레드를 생성하는 방법
class MyRunnable implements Runnable {
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Runnable: " + i);
            try {
                Thread.sleep(500); // 0.5초 동안 대기
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class RunnableExample {
    public static void main(String[] args) {
        Thread t = new Thread(new MyRunnable()); // Runnable 구현체를 이용한 스레드 생성
        t.start(); // 스레드 실행
    }
}
```

- `Runnable` 인터페이스를 구현하면 `Thread` 클래스를 직접 상속하지 않아 유연성 증가
- `Thread` 객체를 생성하면서 `Runnable` 구현체를 전달하여 실행

## 3. 멀티스레드의 필요성

- **단일 스레드의 문제**: 하나의 작업이 끝나야 다음 작업을 수행 가능 (예: UI 멈춤 현상)
- **멀티스레드의 장점**:
  - 여러 작업을 동시에 처리하여 성능 향상
  - UI와 백그라운드 작업 분리 가능 (예: 웹 서버, 채팅 프로그램)
- **비유**: 단일 스레드는 "1인 가게", 멀티스레드는 "여러 직원이 있는 가게"

## 4. 스레드의 동기화 (Synchronization)

- 여러 스레드가 같은 자원을 공유하면 충돌 발생 가능
- 해결 방법: `synchronized` 키워드 사용

```java
// 공유 자원을 사용하는 클래스
class SharedResource {
    private int count = 0;

    // synchronized 키워드를 사용하여 동기화된 메서드
    public synchronized void increment() {
        count++;
        System.out.println("Count: " + count);
    }
}

// 스레드를 생성하는 클래스
class Worker extends Thread {
    private SharedResource resource;

    Worker(SharedResource resource) {
        this.resource = resource;
    }

    public void run() {
        for (int i = 0; i < 5; i++) {
            resource.increment(); // 공유 자원 증가
        }
    }
}

public class SyncExample {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource(); // 공유 자원 생성
        Thread t1 = new Worker(resource);
        Thread t2 = new Worker(resource);
        t1.start();
        t2.start();
    }
}
```

- `synchronized`를 사용하면 한 번에 하나의 스레드만 메서드 실행 가능
- 동기화하지 않으면 두 스레드가 `count` 값을 엉뚱하게 증가시킬 가능성 있음

## 5. 스레드의 상태 (Thread States)

- `NEW`: 스레드가 생성되었지만 아직 시작되지 않음
- `RUNNABLE`: 실행 가능한 상태 (CPU 할당을 기다림)
- `BLOCKED`: 다른 스레드가 자원을 점유하고 있어 대기 중
- `WAITING` / `TIMED_WAITING`: 특정 조건을 기다리거나 일정 시간 동안 대기
- `TERMINATED`: 실행이 끝난 상태

## 6. 활용 사례

- **웹 서버** (클라이언트 요청을 여러 개 처리)
- **채팅 프로그램** (여러 사람이 동시에 메시지 전송 가능)
- **백그라운드 작업** (파일 다운로드, 비디오 렌더링 등)

## 7. 요약

- **스레드(Thread)**: 프로세스 내에서 독립적으로 실행되는 작업 단위
- **멀티스레드(Multithreading)**: 여러 스레드를 동시에 실행하여 성능을 향상시킴
- **자바에서 스레드 생성 방법**
  - `Thread` 클래스 상속 또는 `Runnable` 인터페이스 구현
- **동기화(Synchronization)**: `synchronized` 키워드를 사용하여 공유 자원 충돌 방지
- **활용 사례**: 웹 서버, 채팅 프로그램, 백그라운드 작업 등
