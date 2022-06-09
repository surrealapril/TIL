# SpringMVC 구조 
1. 클라이언트 요청이 들어오면 DispatcherServlet에서 HandlerMapping을 통해 해당 요청을 맵핑한 Controller가 있는지 검색
   - DispatcherServlet 
     - web.xml에 포함.
   - HandlerMapping 
     - servlet설정파일인 xxxxx.xml에 포함. @RequestMapping()제공
2. Controller 찾으면, 해당 Controller 처리를 요청 ( .xml에서 Bean 등록 )
3. Service->DAO->DTO를 통해 DB 데이터/처리결과를 가지고->DAO->Service->Controller
4. Controller에서 요청을 처리하고 결과를 출력할 View이름을 DispatcherServlet으로 리턴
5. ViewResolver(web.xml에 포함된 servlet-context.xml 에 등록된 Bean )를 통해 Controller에서 보내온 View이름을 검색
6. 처리 결과를 View에 송신 -> 처리결과가 포함된 View를 DispatcherServelt으로 송신
7. 최종 결과 화면을 클라이언트에 출력
<br><br><br>

## 📌Annotation
@component 보다 @Controller, @Service, @Repository 로 명시적으로 선언
<br><br><br>

## 📌Context
**Spring이 관리하는 Bean들이 담겨있는 컨테이너**

1. web.xml에 있는 context-param을 이용해 root-context 설정
2. listener 태그의 ContextLoaderListener클래스를 이용해 contextConfigLocation에 있는 root-context들을 불러옴
3. 클라이언트 요청이 들어오면 servlet 태그 안에 있는 설정들이 작동하면서 sevlet-context.xml과 root-context을 동시에 불러옴. 이때 DispatcherServlet 클래스 실행
<br><br><br> 

## 📌xml 파일 역할
- **pom.xml**
  - Maven 설정 파일
- **web.xml**
  - 웹 설정 파일. WAS가 처음 구동될 때 web.xml 을 읽어 웹 어플리케이션 설정을 구성.
  - appServlet(DispatcherServlet)에 context.xml 위치 설정.
- **Spring>root-context.xml (예전 프로젝트에서 applicationContext.xml과 같음)**
  - View를 제외한 객체 정의. Service, DAO, DB등 비지니스 로직과 관련된 설정 (DB설정, mybatis, sqlsession, jdbc 등등)
  - root-context에 등록된 Bean은 모든 context에서 사용가능(공유가능)
  - 서로 다른 servlet-context에서 공유해야하는 빈들을 등록 후 사용 가능.
  - servlet-context 안에 있는 Bean 이용 불가.
- **Spring>servlet-context.xml**
  - org.springframework.web.servlet.view.InternalResourceViewResolver : Controller가 Model을 리턴하고 DispatcherServlet이 View(.jsp)를 찾을 때 쓰이는 정보를 기술하는 태그.

<br><br><br>

[참조링크] 
- https://devpad.tistory.com/24
- https://kingofbackend.tistory.com/77