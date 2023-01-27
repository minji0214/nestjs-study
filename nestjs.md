아벤트루프 
총6단계
nextTickQueue, microTaskQueue 
살행 --> 이벤트루프 생성. ==> Main.js 실행.

패키지 버전명 
major.minor.patch
major: 호환불가능시 up
minor: 기능추가시 up
patch: 버그수정시 up
label: pre, rc, alpha, beta(부가 설명)


nest는 기본적으로 typescript, jest 사용 

interface class 선언방법 
`interface User{
name: string;
age: number;
}`
`class User{
constructor(public name: string, public age: number){}
}`

데커레이터 decorator: 클래스, 메소드, 프로퍼티에 추가적인 기능을 부여할 수 있게 해주는 문법
```typescript
class User{
    @IsEmail()
    @MaxLength(10)
    readonly email: string;
}
```
메서드 데커레이터가 가져야 하는 3개의 인수
1. target: 클래스의 prototype
2. propertyKey: 메서드 이름
3. descriptor: 메서드의 속성을 담고 있는 객체
```typescript
interface PropertyDescriptor{
    value?: any;  //속성값
    writable?: boolean; //수정가능 여부
    configurable?: boolean; // 속서으이 정의수정 여부
    enumerable?: boolean; //열거형 여부
    get?(): any; //getter 함수
    set?(v: any): void; //setter 함수
}
```

컨트롤러 controller: 들어오는 요청을 받고 처리돈 결과를 응답으로 돌려주는 인터페이스
엔드포인트 라우팅 메커니즘을 통해 컨트롤러가 받을 수 있는 요청을 분류한다. 


put 리소스 전체교체
patch 리소스 일부교체

페이로드 다루기 
payload =body
nestjs에는 데이터 전송 객체(dto)가 구현되어 있다. 


컨트롤러 패턴 
request와 response를 관리 하는 껍데기 
그리고 그 request안에 로직들을 처리하는 알맹이가 provider
provider 프로바이더 : 앱이 제공하고자 하는 핵심 기능, 즉 비즈니스 로직을 수행하는 역할/ 
단일책임원칙에 의해 소프트웨서 구조상 컨트롤러와 역할을 분리. 
즉, 컨트롤러는 요청을 받고 응답을 보내는 역할만 수행하고, 비즈니스 로직은 프로바이더가 수행한다.
service, repository, factory, helper 등이 프로바이더에 해당한다.

nestjs가 제공하는 provider의 핵심
1. 의존성 주입 (dependency injection - di)
객체를 생성하고, 사용할 때 관심사 분리가능. --> 코드의 가독성과 재사용성이 높은 sw


pipe 파이프 : 요청과 응답을 가로채어, 요청을 처리하기 전에 데이터를 변환하거나, 응답을 보내기 전에 데이터를 변환할 수 있다.
nestjs에서는 파이프를 통해 데이터를 검증하거나, 데이터를 변환할 수 있다.
미들웨어와 비슷한 역할.(미들웨어는 애플리케이션의 모든 콘텍스트에서 사용하도록 불가능/ 실행콘텍스트를 알지못함.)

파이프 사용목적 :데이터 변환, 유효성 검사 

메타데이터 : 데이터에 대한 데이터, constructed data with a purpose  

middeleware 미들웨어 : 라우트 핸들러가 클라이언트의 요청을 처리하기 전에 수행되는 컴포넌트 
미들웨어에서 수행되는 작업들 
쿠키파싱, 세션관리,, 인증인가, 본문파싱, 

예외처리 
nest에서는 예외에 대한 처리를 위해 exception filter를 제공한다.

인터셉터 
요청과 응답을 가로채서 변형을 가할  수 있는 컴포넌트 
클라이언트와 @get 라우트 핸들러 사이에 위치한다.
인터셉터 이용시 가능한 기능 
1. 메서드 실행 전후 추가로직바인딩
2. 함수에서 반환된 결과를 변환 
3. 함수에서 던져진 예외를 변환 
4. 기본 기능읠 동작을 확장 
5. 특정 조건에 따라 기능을 완전히 재정의 (캐싱)

요청 생명주기 request lifecycle
들어온 요청이 어떤 컴포넌트를 거쳐서 처리되고, 생성된 응답은 또 어떤 컴포넌트를 거쳐 처리되는지를 말함. 
생명주기를 잘 알면 애플리케이션의 동작을 쉽게 이해할 수 있다. 
미들웨어, 가드, 인터셉터, 파이프, 예외 필터,
미들웨어 : 전역으로 바인딩된 미들웨어실행 -->  모듈에 바인딩되는 순서대로 진행
가드 : 라우트 핸들러 실행전에 실행
인터셉터 : 요청: 전역 --> 컨트롤러 --> 라우터  / 응답 : 라우터 --> 컨트롤러 --> 전역

CQRS
Command Query Responsibility Segregation 명령과 조회를 분리하여 성능과 확장성 및 보안성을 높일 수 있도록 해주는 아키텍처 패턴 

클린 아키텍처 
양파 아키텍처라고 불리던 아키텍처에서 발전한것. 
소프트웨어를 여러 동심원 레이어로 나누고 각 레이어에 있는 컴포넌트는 안쪽 원에 있는 컴포넌트만 의존성을 가지도록 함. 안쪽 원에 존재하는 컴포넌트는 바깥원에 독립적 .
원을 중심으로 각각의 기능들을 하는 레이어들로 싸여있다. 

은탄환은 없다- 프레더릭 브룩스 (맞는말 대잔치 )
클린 아키텍처가 만능은 아니다. 
레이어를 4개로 나누고 각 레이어로 책임ㅇ르 분리하게 되면 작성할 코드양은 당연히 늘어난다. 
테스트코드를 작성한다면 테스트코드도 따라서 늘어난다. 
코드양이 늘어난다고 해서 소프트웨어의 복잡도가 떨어진다는 뜻은 아니다. 
오히려 레이어별로 코드가 분리되어 있기 때문에 코드를 이해하기 쉬워진다. 
하지만 조그마한 변경 사항이나 추가 기능 구현에도 시간이 오래 걸린다는 단점은 분명히 존재한다. 
mvp를 만들어 아이디어를 빠르게 검증해보고 싶다면 적합하지 않은 아키텍처 일 수 있다.
주의하자. mvp의 구조가 제품의 구조로 그대로 따라가는 경우는 매우 흔하다. 
시간에 쫓겨 상용 제품의 품질을 떨어뜨린느 우를 범하지 않도록. 

유저서비스에서 클린 아키텍처 적용하기 
```
src/users
├── application
├── domain
├── common
├── infra
├── interface
```


테스트 자동화 
