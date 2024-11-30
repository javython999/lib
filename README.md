# 스프링 부트 스타터와 라이브러리
라이브러리 직접 선택시 발생하는 문제
웹 프로젝트를 하나 설정하기 위해서는 수 많은 라이브러리를 알아야 한다.
여기에 추가로 각각의 라이브러리의 버전까지 골라서 선택해야 한다.
눈에 보이지 않은 가장 어려운 문제는 각 라이브러리들 간의 호환성이다.
개발자가 라이브러리의 버전을 선택할 때 이런 부분까지 고려하는 것은 매우 어렵다.

## 스프링 부트 라이브러리 관리
스프링 부트는 개발자 대신에 수많은 라이브러리의 버전을 직접 관리해준다.
이제 개발자는 라이브러리만 고르고 라이브러리의 버전은 생략해도 된다.
그러면 부트가 부트 버전에 맞춘 최적화된 라이브러리 버전을 선택해준다.

버전 관리 기능을 사용하려면 `io.spring.dependency-management` 플러그인을 사용해야 한다.

build.gradle - plugins 수정
```groovy
plugins {
    id 'org.springframework.boot' version '3.0.2'
    id 'io.spring.dependency-management' version '1.1.0'
    id 'java'
}
```

### dependency-management 버전 관리
`io.spring.dependency-management` 플러그인을 사용하면 `spring-boot-dependencies`에 있는 다음 bom 정보를 참고한다.

버전 정보 bom(Bill Of Materials)
* `https://github.com/spring-projects/spring-boot/blob/main/spring-boot-project/springboot-dependencies/build.gradle`
* 해당 `build.gradle` 문서안에 보면 `bom`이라는 항목이 있다.
* 각각의 라이브러리에 대한 버전이 명시되어 있는 것을 확인할 수 있다.
* 물론 현재 프로젝트에서 지정한 스프링부트 버전을 참고한다.

## 스프링 부트 스타터
* 개발자 입장에서는 그냥 웹 프로젝트 하나 시작하고 싶은 것이고, 일반적으로 많이 사용하는 대중적인 라이브러리를 포함해서 간단하게 시작하고 싶을 것이다.
* 스프링 부트는 이러한 문제를 해결하기 위해 프로젝트를 시작하는데 필요한 관련 라이브러리를 모아둔 스프링 부트 스타터를 제공한다.

스프링 부트 스타터 - 이름 패턴
* `spring-boot-starter-*`
* 쉽게 찾게 도와줌
* 공식: `spring-boot-starter-*`
* 비공식: `thirdpartyproject-spring-boot-starter`
  * ex) `mybatis-spring-boot-starter`


스프링 부트 스타터 - 자주 사용하는 것 위주
* `spring-boot-starter`: 핵심 스타터, 자동 구성, 로깅, YAML
* `spring-boot-starter-jdbc`: JDBC, HikariCP 커넥션풀
* `spring-boot-starter-data-jpa`: 스프링 데이터 JPA, 하이버네이트
* `spring-boot-starter-data-mongodb`: 스프링 데이터 몽고
* `spring-boot-starter-data-redis`: 스프링 데이터 Redis, Lettuce 클라이언트
* `spring-boot-starter-thymeleaf`: 타임리프 뷰와 웹 MVC
* `spring-boot-starter-web`: 웹 구축을 위한 스타터, RESTful, 스프링 MVC, 내장 톰캣
* `spring-boot-starter-validation`: 자바 빈 검증기(하이버네이트 Validator)
* `spring-boot-starter-batch`: 스프링 배치를 위한 스타터

라이브러리 버전 변경
외부 라이브러리의 버전을 변경하고 싶을 때는 다음과 같은 형식으로 편리하게 변경할 수 있다.
`ext['tomcat.version] = '10.1.4`