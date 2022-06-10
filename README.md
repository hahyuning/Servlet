# Servlet
HttpServlet과 FrontController를 이용한 Spring MVC 구현 실습 예제

<br>

## 프론트 컨트롤러
- 프론트 컨트롤러 서블릿 하나로 클라이언트 요청을 받으면 프론트 컨트롤러가 요청에 맞는 컨트롤러를 찾아서 호출
- 공통 처리가 가능해지고, 프론트 컨트롤러를 제외한 나머지 컨트롤러는 서블릿을 사용하지 않아도 됨
- 스프링 웹 MVC의 DispatcherServlet이 프론트 컨트롤러로 구현되어 있음

<br>

#### V1: 프론트 컨트롤러 도입
#### V2: 뷰 로직 분리
#### V3: 모델 추가
- 컨트롤러가 서블릿 기술을 사용하지 않으며, 컨트롤러는 뷰의 논리 이름을 반환하고 실제 물리 위치의 이름은 프론트 컨트롤러에서 처리
- ModelView: 서블릿의 종속성을 제거하기 위해 Model을 직접 만들고 추가로 View 이름까지 전달하는 객체로, ViewName과 뷰를 렌더링할 때 필요한 model 객체를 가지고 있다.
- model은 단순히 map으로 되어 있으므로 컨트롤러에서 필요한 데이터를 key, value로 넣어주면 된다.
- viewResolver: 컨트롤러가 반환한 논리 뷰 이름을 실제 물리 뷰 경로로 변경하고, 실제 물리 경로가 있는 MyView 객체를 반환한다.
   
![image](https://user-images.githubusercontent.com/60869749/173031392-11b0b74b-f802-4357-8e8a-7ab503cea6bf.png)

#### V4: V3와 비슷하지만 단순하고 실용적
- 기본적인 구조는 V3와 같으나 컨트롤러가 ModelView를 반환하지 않고 뷰의 논리 이름인 ViewName만 반환한다.
- model 객체를 프론트 컨트롤러에서 생성해서 파라미터로 넘겨준다.

![image](https://user-images.githubusercontent.com/60869749/173031418-da576d0a-916b-4b48-8a26-5582d71c41e0.png)

#### V5: 어댑터 도입, 유연하고 확장성 있는 설계

![image](https://user-images.githubusercontent.com/60869749/173031445-b937f596-b54c-493d-b9c4-cc26b3c429b3.png)
