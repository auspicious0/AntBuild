# Ant Build_ex_01

## 1. Ant Build란?

Ant Build는 Apache Ant를 사용하여 소프트웨어 프로젝트를 빌드하는 프로세스를 의미합니다. Build는 프로젝트를 컴파일하고, 테스트하고, 패키징하고, 배포하기 위한 단계적인 작업을 자동화합니다.

- **컴파일(Compile):** 소스 코드를 기계어로 변환하여 실행 가능한 바이너리 파일로 만듭니다.
- **테스트(Test):** 작성된 코드가 예상대로 작동하는지 확인하기 위해 테스트를 실행하여 버그를 식별하고 프로그램의 안정성을 검증합니다.
- **패키징(Package):** 컴파일된 소스 코드 및 관련 리소스를 소프트웨어 패키지로 묶습니다. 이 패키지는 사용자가 소프트웨어를 설치하고 실행할 수 있도록 도와줍니다.
- **배포(Deploy):** 패키지된 소프트웨어를 최종 사용자에게 배포합니다. 이 단계에서는 소프트웨어를 설치하고 구성하는 등의 작업이 포함됩니다.

Ant는 이러한 빌드 프로세스를 XML 기반의 빌드 스크립트를 사용하여 정의합니다. 빌드 스크립트에는 빌드 프로세스의 각 단계를 수행하는 데 필요한 작업들이 포함되어 있습니다. 예를 들어, 소스 코드의 위치, 컴파일러 옵션, 테스트 스위트의 실행 방법 등이 빌드 스크립트에 기술됩니다.

## 2. Ant Build 사전 준비 사항

자바가 설치되어 있어야 하며 JDK가 환경 변수에 설정되어 있어야 합니다. 그 후 아래 사이트에 접속하여 자신의 OS와 Java 버전에 맞는 Apache Ant를 다운로드합니다.
[Apache Ant 다운로드 페이지](https://ant.apache.org/bindownload.cgi)

그 후 시스템 변수에 `ANT_HOME`을 추가하고 `Path`에 경로를 추가하여 환경 변수 설정을 완료합니다.

## 3. Ant Build 예제

먼저 아래와 같이 간단한 Java 클래스 파일을 작성합니다.

```
public class HelloWorld {
	public static void main(String[] args) {
		System.out.println("Hello World");
	}
}
```
그 후 자바 프로젝트 내에 build.xml 파일을 추가합니다.
 
build.xml에 아래 내용을 작성합니다.

```
<!-- build.xml -->
<project name="HelloWorld" default="compile-and-run" basedir=".">
    
    <!-- 속성 정의 -->
    <property name="src.dir" value="src"/>
    <property name="build.dir" value="build"/>
    <property name="main.class" value="HelloWorld"/>
    
    <!-- 디렉토리 생성 -->
    <target name="init">
        <mkdir dir="${build.dir}"/>
    </target>
    
    <!-- 컴파일 -->
    <target name="compile" depends="init">
        <javac srcdir="${src.dir}" destdir="${build.dir}"/>
    </target>
    
    <!-- 실행 -->
    <target name="run" depends="compile">
        <java classname="${main.class}" classpath="${build.dir}"/>
    </target>
    
    <!-- 컴파일하고 실행 -->
    <target name="compile-and-run" depends="compile, run"/>
    
    <!-- 정리 -->
    <target name="clean">
        <delete dir="${build.dir}"/>
    </target>
    
</project>
```
아래는 각 코드에 관한 설명입니다.

### 각 코드에 대한 설명

- `<!-- build.xml -->`: 이 부분은 XML 주석으로, 파일의 이름을 설명합니다.

- `<project>`: Ant 프로젝트를 시작하는 태그입니다. 
  - `name` 속성은 프로젝트의 이름을 나타내고, 
  - `default` 속성은 기본적으로 실행할 작업을 지정합니다. 여기서는 `compile-and-run`으로 설정되어 있습니다. 
  - `basedir` 속성은 프로젝트의 기본 디렉토리를 나타냅니다.

- `<property>`: 속성을 정의하는 태그입니다.
  - `name` 속성은 속성의 이름을 나타내고,
  - `value` 속성은 속성의 값입니다.

- `<target>`: 작업을 정의하는 태그입니다.
  - `name` 속성은 작업의 이름을 나타냅니다.
  - `depends` 속성은 해당 작업이 실행되기 전에 선행 작업이 실행되어야 함을 나타냅니다.

- `<javac>`: 자바 소스 코드를 컴파일하는 Ant 작업을 수행하는 태그입니다.
  - `srcdir` 속성은 소스 코드가 위치한 디렉토리를 나타냅니다.
  - `destdir` 속성은 컴파일된 클래스 파일이 저장될 디렉토리를 나타냅니다.

- `<java>`: 자바 클래스를 실행하는 Ant 작업을 수행하는 태그입니다.
  - `classname` 속성은 실행할 클래스의 이름을 나타냅니다.
  - `classpath` 속성은 클래스 경로를 나타냅니다.

- `<delete>`: 디렉토리를 삭제하는 Ant 작업을 수행하는 태그입니다.


실행결과 화면입니다.
 
![image](https://github.com/auspicious0/AntBuild/assets/108572025/8673f3f1-60cc-4fdc-8203-5e8faee23786)


