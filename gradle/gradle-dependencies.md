
### compileOnly

컴파일을 할 때만 필요한 의존성을 명시하는데 사용 된다. 이는 무슨 의미일까?
`Compile`의 핵심을 생각하면 `source code`를 `java byte code`로 변경하는 것이다.
즉, source code를 java byte code로 변경 할 때만 사용 된다는 것이다.

**ex) `Lombok`**
`lombok`의 경우 compile타임에 annotation을 확인해서 java code를 추가해준다. 따라서 compile이 완료된 이후 java byte code가 실행 될 때 (runtime) 과연 Lombok이 필요할까?
전혀 필요하지 않다. 
따라서 compile하는 경우에만 lombok에 대한 의존성이 필요하다.

<br><br>
### runtimeOnly

컴파일과 반대로 프로그램을 실행할 때 필요한 의존성을 명시한다. 

**ex) `JDBC`**
JDBC는 사실 Interface이다. 이러한 interface는 구현체를 필요로 한다. 
생각해보면, JDBC구현체를 컴파일 타임에 결정하지 않는다. 프로그램이 동작하면서 (JDBC의 경우 내 기억으론 forclass를 통해 동적으로 찾아왔던 것으로 기억한다.) 의존성이 결정된다.
따라서, 프로그램이 실행될 때 해당 byte code가 필요하다.

<br><br>

### implementation

컴파일 타임과 런타임에 모두 의존성을 갖는다.

<br><br>

### lombok 사용 시 configuration 확장

```
## kotlin
configurations {
    compileOnly {
        extendsFrom(configurations.annotationProcessor.get())
    }
}

## groovy
configurations {  
    compileOnly {  
        extendsFrom annotationProcessor  
    }  
}

```

[Declaring dependencies (gradle.org)](https://docs.gradle.org/current/userguide/declaring_dependencies.html)

일단, configuration이 무엇인지 알아보자. 아래 설명에 따르면 우리가 흔히 접하는 `implementation`, `compileOnly`와 같은 것이 configuration이다.
> Gradle represents the scope of a dependency with the help of a [Configuration](https://docs.gradle.org/current/dsl/org.gradle.api.artifacts.Configuration.html).
> Every configuration can be identified by a unique name.
> 
> Many Gradle plugins add pre-defined configurations to your project. The Java plugin, for example, adds configurations to represent the various classpaths it needs for source code compilation, executing tests and the like

위 설정을 통해 `copileOnly` configuration은 `anntationProcessor`에서 명시한 dependencies를 상속 받는다.

> A configuration can extend other configurations to form an inheritance hierarchy.
> Child configurations inherit the whole set of dependencies declared for any of its superconfigurations.

이는 기본적인 `java plugin`에서도 사용된다. 생각해보면 `testImplementation`은 기본적으로 source code의 `implementation`을 알고 있어야 한다는 것은 당연하다.
> For example the `testImplementation` configuration extends the `implementation` configuration. The configuration hierarchy has a practical purpose: compiling tests requires the dependencies of the source code under test on top of the dependencies needed write the test class


<br><br>

### Lombok 사용 관련 피드백

```
configurations {  
    compileOnly {  
        extendsFrom annotationProcessor  
    }  
  
    testCompileOnly {  
        extendsFrom testAnnotationProcessor  
    }  
}  
  
dependencies {  
    compileOnly 'org.projectlombok:lombok'  
    annotationProcessor 'org.projectlombok:lombok'  
  
  
    testCompileOnly 'org.projectlombok:lombok'  
    testAnnotationProcessor 'org.projectlombok:lombok'  
  
    testImplementation 'org.springframework.boot:spring-boot-starter-test'  
}
```

위 코드를 살펴보자. 이상한 점은 분명 `compileOnly`는 `annoationProcessor`를 extends 하고 있는데 왜 dependencies에서  compileOnly에서 또 lombok을 의존했을까?
그래서 두 가지 테스트를 해보았다.
1. `compileOnly`에서 `lombok`을 의존하지 않아도 되는가? → 문제 없었다.
2. configuration을 지우고 compileOnly를 지우면 문제가 발생하는가? → lombok을 인식하지 못한다.

이것과는 별개로 lombok의 plugin을 사용하는 것이 lombok에서 권장하는 방법이다.


### IntelliJ 설정

>When you add annotation processors through the build scripts in [Maven](https://www.jetbrains.com/help/idea/work-with-maven-dependencies.html#annotation_processors) or [Gradle](https://www.jetbrains.com/help/idea/annotation-processors-support.html#gradle_annotations) projects, IntelliJ IDEA automatically enables the annotation processing and adds the appropriate paths in the annotation processor settings.

[Configure annotation processors | IntelliJ IDEA Documentation (jetbrains.com)](https://www.jetbrains.com/help/idea/annotation-processors-support.html#annotation_processing)