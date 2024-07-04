---
description: https://docs.gradle.org/current/userguide/gradle_basics.html
---

# - Gradle Build 개념

Gradle을 처음 사용한다면, 여기부터 시작하세요.

## 핵심 컨셉

### 1. Gradle 기초

Gradle은 빌드 Script을 기반으로, 소프트웨어의 building, testing, deployment(배포)를 자동화 합니다.&#x20;

<figure><img src="https://docs.gradle.org/current/userguide/img/gradle-basic-1.png" alt=""><figcaption></figcaption></figure>

####

* `Projects`
  * Application의 라이브러리와 같이 빌드 되는 단위의 소프트웨어를 말합니다.
  * Single project 빌드는 root project라고 하는 한개의 프로젝트만을 포함하는 경우입니다.
  * Multi porject 빌드는 root project와 다수의 sub-porject를 포함하는 경우입니다.
* `Build Scripts`
  * Build Script는 project을 빌드하기 위해 어떤 단계를 거쳐야 하는지 Gradle에서 상세히 알려줍니다.
  * 각 Proejct는 한개 이상의 build script을 가질 수 있습니다.
* `Dependency 관리`
  * 종속성 관리는 각 project에 대해, 외부 resource을 선언하고 종속성을 해결(resolve)하는 자동화된 기술 입니다.
  * 각 project는 외부 종속성을 포함하며, Gradle은 build 동안 종속성을 해결합니다.
* `Tasks`
  * Tasks는 컴파일코드 또는 테스트 실행과 같은 work와 같은, 기초 일의 단위 입니다.
  * 각 project는 build script, 또는 plugin에 한개 이상의 task을 정의합니다.
* `plugins`
  * plugin은 gradle의 사용범위를 확장하거나, proeject에 선택적으로 task을 시킬때 사용합니다.

#### **Gradle Project 구조**

기존 프로젝트를 통해 많은 개발자들이 Gradle을 접할 것이다. 프로젝트의 root 디렉토리에 위치한 `gradlew`, `gradle.bat` 파일은 gradle을 사용한다는 표시다.

```
project
├── gradle                                  (1)                      
│   ├── libs.versions.toml                  (2)
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew                                 (3)
├── gradlew.bat                             (3)
├── settings.gradle(.kts)                   (4)
├── subproject-a
│   ├── build.gradle(.kts)                  (5)
│   └── src                                 (6)
└── subproject-b
    ├── build.gradle(.kts)                  (5)
    └── src                                 (6)
```

`(1)` : wrapper 파일 저장을 위한 Gradle 디렉토리. `(2)` : 종속성 관리을 위한 Gradle 버전 카탈로그. `(3)` : Gradle wrapper scripts. `(4)` : root 프로젝트 또는 sub-프로젝트 정의하는 Gradle 설정 파일. `(5)` : sub-프로젝트의 build scripts. `(6)` : sub-프로젝트 소스코드

#### **Gradle 호출**

Gradle은 많은 IDE에 내장되어 있다. (ex. 안드로이드 스튜디오, 인텔리 J, Visual Studio, Eclipse, Netbans) Gradle은 IDE에서 당신의 APP을 build, clean 명령하면 자동으로 호출된다. Gradle을 사용하고 구성하는 방법에 대해 자세히 알아 보려면 선택한 IDE의 설명서를 참조하는 것이 좋다.

Gradle은 설치 후, 아래의 명령으로 호출 가능하다

```
$ gradle build
```

#### **Gradle Wrapper**

Wrapper는 선언된 Gradle 버전을 호출하는 스크립트를 말한다. Gradle Build를 실행하는데 권장되는 방법이다. 이 스크립트(Wrapper)는 root 디렉토리에 `gradlew`, `gradle.bat` 파일로 있다.

```
$ gradlew build   // linux or osx
$ gradle.bat bild // window
```

### 2. Gradle Wrapper Basics

Gradle Wrapper을 통한 Gradle build 방식이 권장된다.  Wrapper Script는 선언된 Gradle 버전을 실행하며, 필요한 경우 미리 다운로드 한다. ![](https://docs.gradle.org/current/userguide/img/wrapper-workflow.png) Wrapper는 `gradlew`, `gradle.bat` 파일을 통해 가능하다.

<figure><img src="https://docs.gradle.org/current/userguide/img/gradle-basic-2.png" alt=""><figcaption></figcaption></figure>

* 주어진 gradle 버전으로 프로젝트를 표준화한다.
* 다양한 사용자에게 동일한 Gradle 버전이 제공된다.
* 다양한 실행환경(IDE,CI서버...)을 위한 Gradle 버전을 제공한다.

#### **Gradle Wrapper 사용**

안정적이고 통제되며 표준화된 빌드 실행을 보장하려면, Wrapper을 사용하여 빌드를 실행하는 것이 권장된다. 운영체제에 따라, `gradle`명령 대신 `gradlew`, `gradle.bat`을 실행한다.

Gradle 실행 :

```
$ gradle build
```

Linux/OSX 에서의 Wrapper 실행 :

```
$ ./gradlew build
```

Window Powershell 에서의 Wrapper 실행 :

```
$ .\gradlew.bat build
```

Wrapper가 위치한 동일한 디렉토리에서 실행한다. 다른 위치에서 실행하는 경우, 상대경로를 사용하면 된다.

```
$ ../gradlew build
```

아래의 console 결과는 Window에서 Wrapper 사용을 보여준다. (cmd창이며, 자바기반 프로젝트)

```
$ gradlew.bat build

Downloading https://services.gradle.org/distributions/gradle-5.0-all.zip
.....................................................................................
Unzipping C:\Documents and Settings\Claudia\.gradle\wrapper\dists\gradle-5.0-all\ac27o8rbd0ic8ih41or9l32mv\gradle-5.0-all.zip to C:\Documents and Settings\Claudia\.gradle\wrapper\dists\gradle-5.0-al\ac27o8rbd0ic8ih41or9l32mv
Set executable permissions for: C:\Documents and Settings\Claudia\.gradle\wrapper\dists\gradle-5.0-all\ac27o8rbd0ic8ih41or9l32mv\gradle-5.0\bin\gradle

BUILD SUCCESSFUL in 12s
1 actionable task: 1 executed

```

### 3. 명령어 인터페이스 기본

기본 명령어 인터페이스는 IDE가 아닌 곳에서 Gradle과 소통하는 기초적인 함수(method)입니다.  `Gradle Wrapper`를 사용되는 것을 강하게 권장합니다.

<figure><img src="https://docs.gradle.org/current/userguide/img/gradle-basic-2.png" alt=""><figcaption></figcaption></figure>

cmd 에서 Gradle 실행하는 명령어는 아래와 같습니다:

```bash
$ gradle [taskName...] [--option-name...]
```

옵션은 task 이름의 전 후에 허용됩니다.

```bash
$ gradle [--option-name...] [taskName...]
```

만약 복수의 task를 정의한다면, space을 통해 구분해야합니다.

```bash
$ gradle [taskName1] [taskName2] [--option-name...]
```

옵션과 옵션의 값의 사이에 `=` 의 유무와 상관없이 옵션값은 인식됩니다. `=`의 사용을 권장합니다.

```bash
$ gradle [...] --console=plain
```

동작을 활성화하는 옵션에는 `--no`을 사용하여 반대를 의미하는 옵션이 있다.

```bash
$ gradle [...] --build-cache
$ gradle [...] --no-build-cache
```

**명령어 사용 법**

아래는 명령어를 설명합니다. 다른 플러그인은 자체 명령어 옵션을 가질 수도 있습니다.

* Task 실행하기 `taskName`이라는 task을 실행하기 위해 :

```bash
$ gradle :taskName
```

명령어는 single `taskName` 과 포함된 종속성을 실행합니다.

* Task에 특정 옵션 설정하기 task에 옵션을 전달 하기 위해, taskName 뒤에 `--`을 옵션 앞에 붙여 사용합니다.

```bash
$ gradle taskName --exampleOption=exampleValue
```

더 많은 명령어는 [Gradle Command Line Interface reference](https://docs.gradle.org/current/userguide/command\_line\_interface.html#command\_line\_interface)을 참고하세요.

### 4. settings file 기초

이 파일 세팅은 모든 Gradle 프로젝트의 진입점(entry point) 입니다.&#x20;

<figure><img src="https://docs.gradle.org/current/userguide/img/gradle-basic-3.png" alt=""><figcaption></figcaption></figure>

settins file 기본 목적은 build에 sub-project을 추가하기 위함입니다. Gradle은 single 또는 multi-proejct 빌드를 제공합니다.

* single 프로젝트 빌드를 위해, settings file은 선택입니다.
* multi 프로젝트 빌드를 위해, settings file은 필수 이며 모든 project을 선언해야합니다.

#### **settings script**

settings file은 script 입니다. groovy로 적힌 `settings.gradle` 또는 kotlin으로 적힌 `settings.gradle.kts`도 마찬가지 입니다.

Groovy DSL 과 Kotlin DSL만 Gradle Script으로 허용됩니다. 이 settings file 은 전형적으로 프로젝트의 root 디렉토리에서 위치합니다. 살펴봅시다 :

```
rootProject.name = 'root-project'   (1)

include('sub-project-a')            (2)
include('sub-project-b')
include('sub-project-c')
```

* (1) : 프로젝트 이름을 정의합니다.
* (2) : sub-project을 추가합니다.

### 5. Build File 기초

일반적으로, build script는 build 설정, tasks, 플러그인을 상세화 합니다.&#x20;

<figure><img src="https://docs.gradle.org/current/userguide/img/gradle-basic-4.png" alt=""><figcaption></figcaption></figure>

모든 Gradle build은 적어도 한개의 build script을 구성합니다. build 파일에서, 두 가지 형태의 종속성이 추가 될 수 있습니다:

1. Gradle이 종속하는 라이브러리 (와/또는) 플러그인
2. 프로젝트 소스가 종속하는 라이브러리

#### **Build Scripts**

Build Script는 groovy로 적힌 `build.gradle` 또는 kotlin 으로 적힌 `build.gradle.kts`입니다. Groovy DSL 과 Kotlin DSL만 Gradle Script으로 허용됩니다. 살펴봅시다 :

```groovy
plugins {
    id 'application'                    (1)        
}

application {
    mainClass = 'com.example.Main'      (2)
}
```

* (1) : 플러그인 추가
  * 플러그인은 Gradle의 기능을 확장하고 프로젝트의 task에 일을 시킬 수 있습니다.
  * 빌드에 플러그인을 추가하는 것을 `플러그인 적용` 이라 하며 부가적인 기능을 가능하게 합니다.
  * `application` 플러그인은 실행가능한 JVM 어플리케이션을 생성하도록 합니다.
  * Application 플러그인을 적용하는 것은 java 플러그인 적용을 의미합니다. `java` 플러그인은 프로젝트의 bundling 과 testing 기능과 함께 자바 컴파일을 추가합니다.
* (2) : 패키지 명명 속성
  * 플러그인은 프로젝트에 task을 추가합니다. 또한, 속성과 함수(methods)을 추가합니다.
  * `application` 플러그인은 `run` task 같은, 패키지를 정의하고 application을 분산합니다.
  * Application 플러그인은 실행에 요구되는 java application 의 main 클래스를 정의하는 방법을 제공합니다.

### 6. 종속성 관리 기초

Gradle은 종속성 관리를 위한 내장형을 지원합니다.

&#x20;&#x20;

<figure><img src="https://docs.gradle.org/current/userguide/img/gradle-basic-7.png" alt=""><figcaption></figcaption></figure>

종속성 관리는 프로젝트가 필요로 하는 종속성을 선언하고 충돌을 해결하기 위한 자동화된 기술입니다. Gradle build script은 외부 종속성이 필요되는 프로젝트를 build 하는 프로세스를 정의합니다. 종속성은 프로젝트 빌드를 지원하는 JAR, 플러그인, 라이브러리, 또는 소스 코드로 나타냅니다.

#### **버전 카탈로그**

버전 카탈로그는 종속성 선언을 `libs.versios.toml`파일에 중앙화하는 방법을 제공합니다. 카탈로그를 사용하면 하위 프로젝트 간의 종속성 및 버전 구성을 간단하게 공유할 수 있습니다. 또한 팀은 대규모 프로젝트에서 라이브러리 및 플러그인 버전을 적용할 수 있습니다.

버전 카탈로그에는 일반적으로 다음 네 가지 섹션이 포함된다:

1. `[versions]` : 플러그인과 라이브러리가 참조할 버전 번호를 선언합니다.
2. `[libraries]` : 빌드 파일에 사용되는 라이브러리를 정의합니다.
3. `[bundles]` : 종속성 세트를 정의합니다.
4. `[plugins]` : 플러그인을 정의합니다.

```toml
[versions]
androidGradlePlugin = "7.4.1"
mockito = "2.16.0"

[libraries]
google-material = { group = "com.google.android.material", name = "material", version = "1.1.0-alpha05" }
mockito-core = { module = "org.mockito:mockito-core", version.ref = "mockito" }

[plugins]
android-application = { id = "com.android.application", version.ref = "androidGradlePlugin" }
```

파일은 Gradle 및 IDE에서 자동으로 사용할 수 있도록 gradle 디렉터리 에 있습니다 . 버전 카탈로그를 소스 제어로 체크 되어야 합니다: gradle/libs.versions.toml.

#### **의존성 선언**

프로젝트에 의존성을 추가하기 위해, `build.gradle(.kts)` 파일의 dependencies 단에 특정 dependency을 추가한다. 아래의 `build.gradle.kts`파일은 플러그인과 2개의 종속성을 위의 버전 카탈로그를 사용하여 프로젝트에 추가한다.

```toml
plugins {
   alias(libs.plugins.android.application)                              (1)
}

dependencies {
    // Dependency on a remote binary to compile and run the code
    implementation(libs.google.material)                                (2)

    // Dependency on a remote binary to compile and run the test code
    testImplementation(libs.mockito.core)                               (3)
}
```

* (1) : Android 앱 빌드와 관련된 여러 기능을 추가하는 Android Gradle 플러그인을 프로젝트에 적용합니다.
* (2) : 프로젝트에 Material 종속성을 추가한다.
* (3) : 프로젝트에 Mockito 종속성을 추가한다.

`Material` 라이브러리는 `implementation` 설정으로 추가된다. 이는 compiling 과 running (production)환경을 위한 코드다. `Mockito-core` 라이브러리는 `testImplementation` 설정으로 추가된다. 이는 compiling 과 running (test) 환경을 위한 코드다.

#### **종속성 확인**

```bash
$ ./gradlew :app:dependencies

> Task :app:dependencies

------------------------------------------------------------
Project ':app'
------------------------------------------------------------

implementation - Implementation only dependencies for source set 'main'. (n)
\--- com.google.android.material:material:1.1.0-alpha05 (n)

testImplementation - Implementation only dependencies for source set 'test'. (n)
\--- org.mockito:mockito-core:2.16.0 (n)
```

### 7. Tasks 기초

Task는 class 컴파일링, JAR생성, Javadoc 생성, 저장소에 archieve 발행 과 같은 빌드 행위인 독립적인 단위의 일을 의미한다.&#x20;

<figure><img src="https://docs.gradle.org/current/userguide/img/gradle-basic-5.png" alt=""><figcaption></figcaption></figure>

Gradle `build` task를 `gradle` 명령어를 또는 Gradle Wrapper을 사용하여 실행한다.

```
$ ./gradlew build
```

**가능한 Tasks**

프로젝트의 모든 가능한 task는 Gradle Plugin 과 build Scripts에 있다. 아래의 명령어를 터미널에 실행하여, 간으한 모든 task를 리스트화 할 수 있다.

```
$ ./gradlew tasks
Application tasks
-----------------
run - Runs this project as a JVM application

Build tasks
-----------
assemble - Assembles the outputs of this project.
build - Assembles and tests this project.

...

Documentation tasks
-------------------
javadoc - Generates Javadoc API documentation for the main source code.

...

Other tasks
-----------
compileJava - Compiles main Java source.

```

#### **task 실행하기**

`./gradlew run`을 통해 실행 한다 :

```
$ ./gradlew run

> Task :app:compileJava
> Task :app:processResources NO-SOURCE
> Task :app:classes

> Task :app:run
Hello World!

BUILD SUCCESSFUL in 904ms
2 actionable tasks: 2 executed
```

java 프로젝트 샘플에서, `run`의 결과는 `Hello World!`를 console에 출력한 것이다.

#### **task 의존성**

작업을 먼저 실행하려면, 다른 작업이 필요한 경우가 많다. 예를 들면, gradle이 `build` 작업을 실행하려면 java 코드가 먼저 컴파일 되어야 한다. 따라서, `build` task는 `compileJava` task에 의존한다. `compileJava`가 `build`보다 먼저 실행될 것이라는 의미다:

```
$ ./gradlew build

> Task :app:compileJava
> Task :app:processResources NO-SOURCE
> Task :app:classes
> Task :app:jar
> Task :app:startScripts
> Task :app:distTar
> Task :app:distZip
> Task :app:assemble
> Task :app:compileTestJava
> Task :app:processTestResources NO-SOURCE
> Task :app:testClasses
> Task :app:test
> Task :app:check
> Task :app:build

BUILD SUCCESSFUL in 764ms
7 actionable tasks: 7 executed
```

### 8. 플러그인 기초

플러그인은 build 기능을 확장하고 Gradle을 사용자 정의화 하는데 사용된다. ![](https://docs.gradle.org/current/userguide/img/gradle-basic-6.png)
