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

provider 프로바이더 : 앱이 제공하고자 하는 핵심 기능, 즉 비즈니스 로직을 수행하는 역할/ 
단일책임원칙에 의해 소프트웨서 구조상 컨트롤러와 역할을 분리. 
즉, 컨트롤러는 요청을 받고 응답을 보내는 역할만 수행하고, 비즈니스 로직은 프로바이더가 수행한다.
service, repository, factory, helper 등이 프로바이더에 해당한다.

nestjs가 제공하는 provider의 핵심
1. 의존성 주입 (dependency injection - di)
객체를 생성하고, 사용할 때 관심사 분리가능. --> 코드의 가독성과 재사용성이 높은 sw
2. 