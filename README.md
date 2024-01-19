## Today I Learned Record

#### 📘학습 기록

**2024-01-19 (금)**
- Project - Domain Logic에서 update를 어떻게 만들까 고민
  1. minor GC가 자주 발생하도록 새로운 객체를 생성해서 Reference를 끊는 방법
  2. 일반적인 update 방법
    
  → (내 생각) Reference를 끊는 경우, 연관 관계가 있는 다른 모든 객체에 다시 연결을 해주어야 하므로 일반적인 방법을 선택하는 것이 맞다고 생각한다.
  → GC 조금 까먹었는데, 나중에 다시 Review하자

**2024-01-18 (목)**
- [Test에 대한 Review](test/TEST에%20대하여.md) & Project - Fake Repository를 어떻게 만들어야 할까..?
  → [해결(24.01.19)]

**2024-01-17 (수)**
- [gradle의 lombok dependency without springinitializer](gradle/gradle-dependencies.md)

**2024-01-16 (화)**
- [Project - API를 어떻게 설계하는 것이 더 좋은 방법일까?](https://github.com/f-lab-edu/self-monitoring/issues/3#issuecomment-1893046172)

**2024-01-15 (월)**
- [Project - 상당히 많은 Response가 내려올 때, 어떻게 해당 값을 검증해야 할까?](https://github.com/f-lab-edu/self-monitoring/issues/3#issuecomment-1873681594)

**2024-01-12 (금)**
- [gradle의 dependency 범위 관련 공부](gradle/gradle-dependencies.md)

**2024-01-11 (목)**
- [gradle shell script 분석](https://github.com/iamabear09/self-monitoring/commit/7e74e01716b408439bf964dba5e0b3f12d427142#comments)

**2024-01-05 (금)**
- [gradlew - shell script 공부](https://github.com/iamabear09/shell-script-study/commit/048ae895ad64fc122ae2bd849e1d51ec9ee6aec9)

**2024-01-02 (화)**
- [Github의 일반 merge vs rebase merge의 차이에 대해서 살펴보자.](github/github-rebase-merge-vs-merge.pdf)

**2023-12-30 (토)**
- [Github Repository fork](github/Github%20Repository%20fork.md) :: fork Repo와 Origin Repo의 충돌 발생 시

**2023-12-29 (금)**
- [boot Jar란 무엇인가?](gradle/gradle-bootJar.pdf)

**2023-12-28 (목)**
- [Gradle Toolchain이란?](gradle/gradle-toolchain.pdf)

**2023-12-27 (수)**
- [데이터 처리 - 서버 or 클라이언트](project/self-monitoring/데이터%20처리%20-%20서버%20or%20클라이언트.md) :: 데이터 가공을 클라이언트에서 하는 것이 좋을까, 아니면 서버에서 하는 것이 좋을까?

**2023-12-25 (월)**
- 학습 기록물이 없다.. Gradle 공식문서 읽는 중.. 이제 Tasks와 Plugin이 어떻게 동작하는지 이해 완료했다. 공식문서 다시 읽은 후 정리하고 업로드 예정!

**2023-12-23 (토)**
- [Gradle의 Build Lifecycle 및 extra 사용](gradle/gradle-build-lifecycle-and-extra-usage.pdf)

**2023-12-22 (금)**
- [Gradle Task 수행을 Multi Project 상황의 예시를 통해 이해해보자.](gradle/gradle-multi-project-executing-tasks.pdf)

**2023-12-21 (목)**
- [Kotlin 문법은 어떻게 Gradle의 Kotlin DSL가 되는가? - Gradle 읽는 방법](gradle/kotlin-for-gradle.pdf)

**2023-12-20 (수)**
- [Gradle 삽질 중... Kotlin 문법 정리](gradle/Kotlin%20문법%20정리%20for%20Gradle.md)

**2023-12-19 (화)**
- [Thread Per Request Model의 장단점 및 INSITE](spring-thread-model/thread-per-request.pdf)

**2023-12-18 (월)**
- [asynchronous에 대한 생각 정리 - 왜 Event Loop가 필요하게 되었는지 파악 가능](spring-thread-model/asynchronous-기본.pdf)

**2023-12-17 (일)**
- [socket programming시 표준 입출력 함수 사용의 장점 - 버퍼링 & 파일 디스크립터에 대한 이해](network/TCP&UDP-표준입출력함수%20장점.pdf)

**2023-12-16 (토)**
- [다중 접속 서버 구현 및 Select를 통한 멀티플렉싱 서버 원리 학습](network/TCP-multi-flexing-select-function.pdf)

**2023-12-15 (금)**
- [Process간 통신의 원리](process/process-comunication.pdf) 

**2023-12-14 (목)**
- [TCP socket의 내부 동작 Study 및 기억하고 싶은 부분 기록](network/TCP&UDP-socket.pdf)

**2023-12-12 (화)**
- [Deep dive Native&Green Thread](process/Deep%20dive%20Native&Green%20Thread.md)

**2023-12-11 (월)**
- [Green Thread vs Native Thread 그리고 JVM의 Thread 동작 과정](process/user_thread-vs-native_thread.pdf)

**2023-12-09 (토)**
- [Process의 Data Structure :: Task_descriptor](process/process-task_descriptor.pdf)

**2023-12-08 (금)**
- [Process는 어떤 과정을 거쳐 생성될까?](process/process-create.pdf)

**2023-12-07 (목)**
- [Linux의 Process가 실제 코드로 어떻게 생긴거지?](process/process-code.pdf)

**2023-12-06 (수)**
- [Java의 Synchronization은 Monitor로 구성되어있는데 도대체 어떻게 동작하는거지?](synchronization/sychronization-in-java.pdf)

**2023-12-05 (화)**
- [Garbage Collection과정에서 Stop-the-World는 왜 필요한거지?](jvm/garbage-collection/garbage-collection-stop-the-world.pdf)

**2023-12-04 (월)**
- [multi core에서 동시성 이슈 해결 방법 학습](synchronization/sychronization-in-multicore.pdf)

**2023-12-03 (일)**
- [운영체제의 semaphore 학습](synchronization/semaphore.pdf)

**2023-12-02 (토)**
- [GC의 Stop-and-Copy과정 중 사용되는 forwarding pointers가 왜 필요하지?](jvm/garbage-collection/garbage-collection-forwarding-pointers.pdf)
  
**2023-12-01 (금)**
- [OOPs의 Mark Word  학습](jvm/ordinary-object-pointers(oops)/ordinary-object-pointers-mark-word.pdf)
  
**2023-11-30 (목)**
- [jvm heap영역에서 instance의 memory layout 형태](jvm/ordinary-object-pointers(oops)/ordinary-object-pointers-basic.pdf)
  
  <sup>참고 자료</sup> https://www.baeldung.com/java-memory-layout

**2023-11-29 (수)**
- [garbage collection 기본 학습](jvm/garbage-collection/garbage-collection-basic.pdf)

   <sup>참고 자료</sup>  https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html
  
**2023-11-28 (화)**
- [building simple reliable transfer protocol - TCP 원리 학습](network/building-simple-reliable-data-transfer-protocol.pdf)

**2023-11-27 (월)**
- [network-delay의 원인 학습](network/network-delay.pdf)
- [Demux/Mux와 TCP&UDP의 socket 연결 시 차이점](network/TCP&UDP-connection&connectionless.pdf)

**2023-11-26 (일)**
- [jvm memory 학습 및 method 호출 시 jvm memory 변화 과정 학습](jvm/jvm-memory.pdf)

**2023-11-25 (토)**
- [class가 loading되고 초기화 되는 과정까지의 과정 학습](jvm/life-of-a-class.pdf)

**2023-11-24 (금)**
- [Java Byte Code (.Class file) format](jvm/class-file-format.pdf)

**2023-11-23 (목)**
- [JVM ClassLoader 학습](jvm/jvm-classloader-전반적인동작과정.pdf)