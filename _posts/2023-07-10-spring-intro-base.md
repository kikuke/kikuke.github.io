---
title: "Spring Boot 웹 개발 방식"

categories: [Spring, 스프링 입문]

tags: [웹, 개발 방식]

last_modified_at: 2023-07-10T00:00:000
---

## 개요

**스프링의 웹 개발 방식은 크게 세가지가 있다.**

1. [정적 컨텐츠 방식](#정적-컨텐츠-방식)
2. [MVC와 템플릿 엔진 방식](#mvc와-템플릿-엔진-방식)
3. [API 방식](#api-방식)

사용자의 HTTP 요청이 스프링에 내장된 Tomcat 웹서버에 들어오면 Tomcat은 이것을 Contoller에 전달하게 된다.  
이때 두가지 조건에 따라 전달되는 방식이 달라지게 된다.

1. 요청받은 HTTP 리퀘스트, uri가 Controller에 `@GetMapping()` 등과 같은 어노테이션을 통해 매핑된 메소드에 존재하는가?
    - 존재하지 않는다면 이미 만들어진 html 파일을 전달하는 정적 컨텐츠 방식으로 동작
2. `@ResponseBody` 애노테이션이 매핑된 메소드에 있는가?
    - `@ResponseBody` 애노테이션이 있다면, HttpMessageConverter를 이용해 만들어진 JSON 또는 String을 전달하는 API 방식으로 동작  
    - `@ResponseBody` 애노테이션이 없다면, Model 값과 ViewResolver를 이용해 만들어진 html 파일을 전달하는 MVC와 템플릿 엔진 방식으로 동작

전체적인 스프링 계층 구조가 궁금하다면 [스프링 계층 구조](#스프링-계층-구조)를 참고하자.

-------

## 정적 컨텐츠 방식

**정적 컨텐츠 방식은 이미 만들어진 html 파일을 있는 그대로 보여주기만 하는 방식이다.**  
정적 컨텐츠는 프로젝트 내 `:resource/static` 폴더 하위에서 접근한다.

![정적 컨텐츠 방식](/assets/img/spring/intro/hello-static.png)

정적 컨텐츠 방식의 동작 과정은 아래와 같다.

1. 컨트롤러에서 요청받은 HTTP 리퀘스트, uri에 매핑되는 메소드가 없을 때
2. `:resouce/static` 하위의 폴더에 일치하는 url의 파일을 찾고,
3. 해당 url의 파일을 그대로 전달한다.

정적 컨텐츠 방식은 이미 만들어진 html 파일을 전달할 뿐이므로 ViewReosolver가 필요없다.

-------

## MVC와 템플릿 엔진 방식

**MVC와 템플릿 엔진 방식은 Controller에서 리턴한 ViewName(String)에 대응되는 html 파일과 Controller 에서 주입한 Model을 템플릿 엔진을 통해 html 파일을 동적으로 만들어 보내는 방식이다.**  
주로 html 파일을 주는 웹 서버를 구현하는데 쓰인다.

![MVC와 템플릿 엔진 방식](/assets/img/spring/intro/hello-mvc.png)

MVC와 템플릿 엔진 방식의 동작 과정은 아래와 같다.

1. 컨트롤러에서 요청받은 HTTP 리퀘스트, uri에 매핑되는 메소드가 있고, `@ResponseBody` 애노테이션이 없다면
2. 컨트롤러에서 관련 데이터 처리를 하고 Model에 값을 주입한 뒤
3. 컨트롤러에서 리턴 받은 ViewName(String)을 `:resource/templates/ + {ViewName} + .html` 파일을 찾아
4. ViewResolver(템플릿 엔진)에 Model과 함께 전달해 html을 동적으로 생성한 뒤
5. 생성된 html 파일을 전달한다.

MVC는 Model - View - Controller의 줄임말인데,

1. Controller에서 사용자의 요청을 받아 처리
2. Model에 데이터 주입
3. ViewResolver에 데이터가 담긴 Model을 전달해 html을 만들어 View를 처리

위와 같은 과정처럼 말그대로 Model- View - Controller를 분리하는 방식이다.  
이때 ViewResolver는 템플릿 엔진이다.  
템플릿 엔진은 html 파일을 동적으로 만들때 프로젝트 내 `:resource/templates/ + {ViewName} + .html` 파일을 찾아 이 html 파일을 Model에 담긴 값을 이용해 값을 주입해 변환시키는 방식으로 동작한다.

-------

## API 방식

API 방식은 Controller에서 리턴한 객체 또는 String을 HttpMessageConverter를 통해 Json 또는 String으로 변환후 HTTP Message로 전달하는 방식이다.  
데이터만 전달하기 때문에 API 서버간 통신도 쉽고 안드로이드 애플리케이션, 웹 애플리케이션 등이 클라이언트인 API 서버를 만들 때 사용한다.  

![API 방식](/assets/img/spring/intro/hello-api.png)

API 방식의 동작 과정은 아래와 같다.

1. 컨트롤러에서 요청받은 HTTP 리퀘스트, uri에 매핑되는 메소드가 있고, `@ResponseBody` 애노테이션이 있다면
2. 컨트롤러에서 관련 데이터 처리를 하고 객체 또는 String을 리턴
3. 컨트롤러에서 리턴 받은 것을 HttpMessageConverter를 통해 객체면 Json으로 변환후 Http body에 담아 HttpMessage로 만들어 전송, String이면 String을 Http body에 담아 HttpMessage로 만들어전송

단, 이때 변환 되는 클래스는 [자바 빈 규약](https://ko.wikipedia.org/wiki/자바빈즈)에 의해 getter, setter가 존재해야 한다.(프로퍼티 접근 방식)  
HttpMessageConverter는 Http Accept 헤더와 매핑된 메소드의 반환 타입 정보 둘을 조합해서 선택한다.

-------

## 고민한 점

학교 프로젝트를 하기 위해 급하게 처음 사용해 본 것은 API 방식이다.  
때문에 나는 스프링이 API 방식만 지원하는 줄 알았는데, 나중에 자료들을 찾다보니 웹서버를 구현하는 방식이 많아서 스프링은 뷰를 어떻게 구현하는지 궁금한 점이 되게 많았다.  
특히 나는 그동안 Json 데이터와 String 데이터만 보냈었는데 아예 뷰를 보여주는 것이 어떻게 가능한지 궁금했다.  
하지만 이번 강의를 들어보며 스프링, 웹서버는 요청받은 HTTP 리퀘스트와와 uri에 따라 그에 해당되는 로직을 처리한 뒤 그냥 데이터를 담아 Http Message를 전달할 뿐, Http Message에 담긴 데이터와, 그걸 요청한 클라이언트가 안드로이드 앱인지, 웹 브라우저인지에 따라 데이터를 이용해 나온 결과물이 달랐을 뿐이라는 것을 알게됐다.

-------

## 부록
### 스프링 계층 구조

![스프링 계층 구조](/assets/img/spring/intro/layer.png)

 - Presentation Layer (Controller Layer)
    - 외부 요청과 응답과 관련
 - Business Layer (Service Layer)
    - 트랜잭션과 관련
 - Data Access Layer (Repository Layer)
    - DB 접근에 관련
 - Data Transfer Object(DTO)
    - 계층 간 데이터 교환을 위한 객체
 - Domain Model
    - 대상을 추상화 한 것
    - 무조건 DB 테이블과 관계가 있어야 하는 것이 아닌, VO와 같은 값 객체도 이에 해당

-------

# * 참고할 만한 자료

 * [스프링 메뉴얼](https://spring.io/projects/spring-boot#learn)

-------

# * 참고자료

 * [스프링 입문](https://www.inflearn.com/course/스프링-입문-스프링부트/)