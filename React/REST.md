# REST



#### REST의 구체적인 개념



HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.

즉, REST는 자원 기반의 구조(ROA, Resource Oriented Architecture) 설계의 중심에 Resource가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍쳐를 의미한다.

웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 ID인 HTTP URI를 부여한다.

CRUD Operation

Create : 생성(POST)
Read : 조회(GET)
Update : 수정(PUT)
Delete : 삭제(DELETE)
HEAD: header 정보 조회(HEAD)



#### REST 구성 요소
자원(Resource): URI
모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
자원을 구별하는 ID는 ‘/groups/:group_id’와 같은 HTTP URI 다.

Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청한다.

행위(Verb): HTTP Method

HTTP 프로토콜의 Method를 사용한다.
HTTP 프로토콜은 GET, POST, PUT, DELETE 와 같은 메서드를 제공한다.

표현(Representation of Resource)

Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.
REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타내어 질 수 있다.
JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.



#### REST API 설계 기본 규칙



참고 리소스 원형



도큐먼트 : 객체 인스턴스나 데이터베이스 레코드와 유사한 개념
컬렉션 : 서버에서 관리하는 디렉터리라는 리소스
스토어 : 클라이언트에서 관리하는 리소스 저장소
URI는 정보의 자원을 표현해야 한다.

resource는 동사보다는 명사를, 대문자보다는 소문자를 사용한다.
resource의 도큐먼트 이름으로는 단수 명사를 사용해야 한다.
resource의 컬렉션 이름으로는 복수 명사를 사용해야 한다.
resource의 스토어 이름으로는 복수 명사를 사용해야 한다.

Ex) GET /Member/1 -> GET /members/1
자원에 대한 행위는 HTTP Method(GET, PUT, POST, DELETE 등)로 표현한다.
URI에 HTTP Method가 들어가면 안된다.

Ex) GET /members/delete/1 -> DELETE /members/1
URI에 행위에 대한 동사 표현이 들어가면 안된다.(즉, CRUD 기능을 나타내는 것은 URI에 사용하지 않는다.)

Ex) GET /members/show/1 -> GET /members/1

Ex) GET /members/insert/2 -> POST /members/2
경로 부분 중 변하는 부분은 유일한 값으로 대체한다.(즉, :id는 하나의 특정 resource를 나타내는 고유값이다.)

Ex) student를 생성하는 route: POST /students

Ex) id=12인 student를 삭제하는 route: DELETE /students/12
https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html



출처 : https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html