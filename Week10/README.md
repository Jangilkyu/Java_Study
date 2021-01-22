# 목표
- 자바의 멀티쓰레드 프로그래밍에 대해 학습하세요.

# 학습할 것 (필수)
# Thread 클래스와 Runnable 인터페이스
Thread를 구현하는 방법은 두가지 방법이 있다.

## Thread class extends(상속)하는 방법
- `java.lang.Thread`class를 상속받고 Thread가 가지고 있는 `run()`를 Overriding한다.
- 자바는 다중상속이 안되기 때문에 Runnable 인터페이스를 사용하는 편이다.

1. Thread 클래스를 상속
```java
    public class MyClass extends Thread {

```

2. Run Method를 Override하고 동시에 처리되어야할 코드를 정의 (Thead로 동작할 코드를 정의)
```java
    public void run(){
        //동시에 실행되어야 할 코드를 정의
    }
```

3. 자식클래스로 객체 생성(부모인 Thread가 생성된다.)
```java
    MyClass mc = new MyClass();
```

4. Thread 클래스의 start()를 호출하여 run()를 호출한다.
```java
        mc.start(); // Thread에 start()를 호출했지만 run()이 오버라이드 되어서 내 클래스에 있는 run()가 호출된다.
  
    }//class
```


## Runnable interface implements(구현)하는 방법

1. Runnable interface를 구현
```java
    public class MyClass implements Runnable {
  
```

2. run() abstract method Override
```java
    public void run() {
        //Thread로 동작해야할 코드 (동시에 실행 되어야할 코드)
    }//run
```

3. 자식 클래스를 객체화
```java
    MyClass mc = new MyClass();
```

4. Thread클래스를 객체화
```java
    Thread t = new Thread(mc); // has a
```

5. Thread에 존재하는 strat()를 호출하여 run()를 호출한다.
```java
    t.strat();
```

# 쓰레드의 상태
|상태|설명|
|----|----|
|NEW|스레드가 생성되고 start()메소드가 호출되지 않은 상태|
|RUNNABLE|start()가 호출되어 실행 대기중이고 run()을 하면 RUNNING(CPU 점유)이 된다.|
|WAITING|Thread의 작업이 종료되지는 않았지만 실행이 가능하지 않은 일시정지 상태|
|TIMED_WAITING|일시정지시간이 주어진 경우|
|BLOCK|동기화 블록에 의해 일시정지 상태이다.(사용하려는 객체의 lock이 풀릴때 까지 대기중인 상태)|
|TERMINATED | Thread의 작업이 종료가 된 상태|

# 쓰레드의 우선순위

Thread의 우선순위의 범위는 1~10이며 숫자가 높을수록 우선순위가 높다.

main 쓰레드는 우선순위가 5이므로, main 메서드에서 생성하는 쓰레드의 우선순위는 자동적으로 5가 된다.

```java
 void setPriority(int newPriority);
 int getPriority();
 
 public static final int MIN_PRIORITY = 1;   // 최소 우선순위
 public static final int NORM_PRIORITY = 5;  // 보통 우선순위
 public static final int MAX_PRIORITY = 10;  // 최대 우선순위
```

[출처](https://devbox.tistory.com/entry/Java-%EC%93%B0%EB%A0%88%EB%93%9C%EC%9D%98-%EC%9A%B0%EC%84%A0%EC%88%9C%EC%9C%84)

# Main 쓰레드
> `JVM이 자바 프로그램`이 시작 할때 Thread가 즉시 실행되는데 Main Thread이다.

```java
public static void main(String[] args) {
    Thread t = Thread.currentThread(); // 현재 실행중인 메인 스레드. 
    ...
}
```

# 동기화
> 여러 개의 Thread가 한 개의 자원을 사용하고자 할 때,
해당 Thread만 제외하고 나머지는 접근을 못하도록 막는 것

특정 객체에 lock을 걸 때
```java
    synchronized(객체의 참조변수){

    }
```
synchronized의 block은 block의 시작부터 lockd이 걸렸다가 block이 끝나면 lock이 풀린다.

- 메서드에 lock을 걸고자 할때
`synchronized method의 경우에는 한 쓰레드가 synchronized 메서드를 호출해서 수행하고 있으면, 메소드가 종료될 때 까지 다른 쓰레드가 이 메서드를 호출할 수가 없다.

```java
    public synchronized void cal() {
        
    }
```


# 데드락
두 개 이상의 Thread가 서로 상대방의 락을 얻기 위해 영원히 block상태로  대기하고 있는 상태이다.

아래의 4가지 조건이 전부 충족되면 `데드락`발생한다.

- 상호배제: 자원은 하나의 프로세스만 사용(점유)할수 있다.
- 비선점: 사용중인 자원을 뺏을 수 없다.
- 환형대기: 대기하는 프로세스가 순환을 이룬다.
- 점유와 대기: 자원을 사용하고 있으면서 다른 자원을 요구하며 대기하는 상태인 프로세스가 있다.

- 데드락을 해결
    - 예방 : 교착 상태 발생 조건 중에 하나를 제거한다. 단, 자원 낭비가 심하다. 
    - 회피 : 교착 상태가 발생하면 피해나가는 방법
    - 회복 : 교착 상태를 일으킨 프로세스를 종료하거나, 할당된 자원을 해제함으로써 회복한다.