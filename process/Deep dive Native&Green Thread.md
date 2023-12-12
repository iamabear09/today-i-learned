
### JVM의 PC Regiter와 OS의 TCB의 PC Regiter의 차이는 무엇인가?

내가 궁굼했던 부분은 Green Thread에서 JVM의 PC Regiter가 어떻게 CPU의 PC Register와 연결되는 것인지 궁굼했다.
하지만 여기서 내가 착각했던 부분이 있었다.
OS의 TCB의 PC Register가 CPU의 PC Register라고 착각했다. 다시 생각해보면 OS의 TCB는 Thread의 Snap shot이다. 따라서 이러한 snap shot은 Context switching이 발생할 때, 현재 실행 흐름을 잃어버리지 않게 하기 위해서 **Back Up**해두는 것이다.
이는 현재 쓰레드가 CPU에서 실행중인 경우 Context Switching이 발생하기 전 까지는 Thread에 대한 정보가 CPU의 Register에 존재하므로 TCB의 정보가 업데이트 되지 않는다.

정리: OS의 TCB 또한 Context Switching시 현재까지 실행했던 Thread를 Back Up하기 위한 공간이다.


### 위의 정보를 Green Thread에서 생각해보자.

User-level Thread와 Kernel-level Thread가 M:1 Mapping이 이루어진다. 어떻게?
내가 착각한 부분은 다음과 같다.
User level Thread간 Context Switching이 발생하기 위해서는 CPU의 Register 값에 User Space에 존재하는 TCB값을 덮어 씌워주어야 한다고 착각했다.
이는 불가능하다. 하지만, kernel이 관리하는 TCB 값에 User Space에서 관리되는 TCB값을 덮어 씌우면 될 것이다. 이 또한 System Call이 발생한다.
따라서 Context Switching이 발생하는 경우 현재 kernel space의 TCB값을 User Space의 TCB 값에 Back Up해 놓고 User Space의 다른 TCB 값을 현재 OS의 TCB에 덮어 씌우면 이것이 Context Switching 과정이 되는 것 같다.

이 과정은 생각해보면, H/W Thread와 OS kernel Thread가 mapping되는 과정과 상당히 유사한 것 같다.


### native thread와의 1:1 Mapping의 단점은?
native Thread의 단점은 Scheduling의 통제권이 OS에 넘어간다는 것이다. App이 할 수 있는 것이 없다.
"이것이 왜 단점이지" 라는 생각이 들 수도 있다. GC의 Stop the world과정을 Green Thread와 Native Thread의 관점에서 비교해보자.
만약 Green Thread에서 GC가 발생하는 경우 Stop the world를 동작 시키기 위해서는 그냥 GC를 수행하는 Thread가 계속 동작하도록 하면 된다.
하지만, OS가 Thread를 통제하는 순간 GC를 구현하기 위해서는 "현재 Thread가 GC를 수행하는 Thread가 아닌 경우 동작을 포기하도록" 구현해야 한다.
여기서 내가 착각한 부분이 존재한다.
GC의 Stop the world를 구현하기 위해서 disableInterrupt를 사용하는줄 알았다. 근데 생각해보면 이 코드의 동작은 OS의 권한이다. GC를 결국 Application Code가 구현하게 될 텐데 User Code에서 disable interrupt를 할 수 있으면 안된다.


### 왜 Thread Object를 생성하는 순간 Native Thread가 수행되는 것이 아니라, start() method를 호출하는 순간 Native Thread가 실행될까?
만약 Thread Object 생성과 함께 Native Thread도 생성된다고 생각해보자. 그러면 OS 입장에서 TCB가 생성된 것이고 이는 결국 언젠가 수행이 될 것이다.
이 말은 Thread의 시작 시점을 내가 결정 할 수 없다는 것이다. 즉, 언제 새로 생성한 Thread가 시작될지 알 수가 없다.


### new Thread.start() 사용 시 발생할 수 있는 문제점
위와 같은 맥락으로 위 코드가 실행되는 순간 나는 해당 Thread에 대한 통제권을 잃어버리게 된다. 만약 Thread에 무한 루프라도 존재하면, Object는 GC의 대상이 되지 않고 memory leak이 발생할 수 있다.
따라서, new Thread.start()와 같은 코드를 작성하고 있다면 문제가 발생하고 있는 것이다.

### new Thread.start() 말고 그러면?
따라서 Thread Pool 사용을 통해 Thread에 대한 제어권을 얻어 올 수 있도록 작성한다.