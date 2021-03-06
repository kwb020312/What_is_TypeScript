타입스크립트 에 대하여

이 저장소는 https://www.typescriptlang.org/docs/handbook/typescript-from-scratch.html
를 보고 참고하여 만들어졌음을 밝힘.

현재 JavaScript의 고질적인 문제를 해결하기 위하여 TypeScript 사용자가 늘어나고있다. 

<img src="gitImages\TS_Logo.png">

## 설치

```npm
npm install -g typescript
```

윈도우 사용자의 경우 
cmd 에서 windows PowerShell 을 관리자 권한으로 실행한 후

```powershell
Set-ExecutionPolicy RemoteSigned
y
```

그렇게 한 후

```typescript
tsc test.ts
```

를 할 경우 같은 역할을 하는 js 파일이 생성됨.

```javascript
const obj = { width: 10 , height: 15 };
const area = obj.width * obj.heigth // NaN 스펠링이 틀렸음
```

위와 같은 경우를 많이 경험해봤을 것 이다. 

JavaScript 의 경우에 위의 area 는 NaN 을 return 할 뿐이지만

<img src="gitImages\errMSG.png">

TypeScript 의 경우에는 위와 같이 당신이 의미하려는 것이 'height' 가 맞냐고 친절하게 로그를 입력하여준다.

물론 이름과 같이 JS 의 Type 문제를 해결하기 위하여 만들어졌지만 여러 유용한 점이 있다는 것을 말하고 싶은 것이다.

## String

문자형은 

```typescript
let str:String = 'Hello World!'
```

위와 같이 타이핑한다.

## Object

객체형은 여러 방법이 있는데 

```typescript
interface Obj {
    name: string; // interface 는 object 가 아니기 때문에 , 로 구분하지 않도록 주의한다.
    id: number;
}

// Success
const user: Obj = {
    name:'Chobby',
    id:0
}

// Error
const err: Obj = {
    username:'woobin',
    id:1
}
```

마지막 err 객체를 보면 interface 는 name:string 인데 err 객체의 경우 username:string 이다. 이러한 경우 바로 오류를 잡아주는 로그를 준다.

<img src="gitImages\userName_TypeError.png">

## Class

클래스 형 또한 지원하는데,

```typescript
class UserAccount {
    name: string;
    id: number;
    constructor(name: string , id: number) {
        this.name = name
        this.id = id
    }
}
```

위와 같이 사용이 가능하다.

## Function

함수형 은 인자와 return 값 모두 타이핑이 가능하다.

```typescript
function getReturnType():Return {
    // ...
}

function getType(val:Val) {
    // ...
}
```

## Create Type

기존에 지정되어있는 타입이 아니더라도 내가 직접 타입을 만들 수 있다.

```typescript
// true OR false 를 return 한다면 오류가 발생하지 않음
type RandomBoolean = true | false

type DoorState = "open" | "close"

type EvenNumbers = 2 | 4 | 6 | 8

function NumORArray(obj:string | string[]) {
    // 위 인자와 같이 문자 배열의 형태라면 Array 가 아닌 string[] 으로 표현한다.
}
```

## Generic

제네릭은 배열 정보를 표기하는 곳에 사용되는데

```typescript
type StringArray = Array<string>
type NumArray = Array<number>
type ObjectArray = Array<{ name : string }>
```

위와 같이 선언이 가능하다.

## Declare 

declare 는 값을 정의하지 않고 , type 만을 가볍게 정의 할 때 사용된다.

```typescript
declare const backpack:Backpack
```

## Interface 

인터페이스 는 제네릭 과 같이 사용할 때 여러 방면으로 사용이 가능한데,

```typescript
interface Test<Type> {
    // void 는 무언가를 return 하지 않는 함수를 말함 ex)console.log()
    add: ( obj : Type ) => void
}

declare const first:Test<string>

// error 위 구문에서 Test<string> 을 했으므로 add 함수는 인자의 값으로 string 만을 허용함
first.add(23)
```

## 혼용 배열

숫자형과 문자형 이 섞여있는 배열은 어떻게 정의해야할까?
답은 이렇다

```typescript
let test:[string,number]

test = ['hello',10] // OK
test = [10,'hello'] // Fail
```

## enum

enum 의 사용법은

```typescript
enum Color {
    Red, // 0
    Green, // 1
    Blue // 2
}

let select: Color = Color.Green // 1
```

## unknown

변수 타입을 모르는 경우 unknown 으로 정의가 가능하다
```typescript
let notSure: unknown = 4
notSure = "문자형도 변경 가능하다"
notSure = false // boolean 또한 변형 가능
// 그러나 어느 타입으로도 정의가 되지 않기 때문에

declare let x : unknown;
const testNum : number = x // error num 아님
const testStr : string = x // error string 아님
const testBool : boolean = x // error boolean 아님
```

## any

any 는 unknown 과 같지만 어느 속성과도 호환이 가능하다

```typescript
declare let x : any;
const testNum : number = x // success num 
const testStr : string = x // success string
const testBool : boolean = x // success boolean
```

하지만 모든 편의를 위한 any 는 typescript 의 사용성을 해칠 뿐 아니라 안전성을 잃는 대가 로 사용하는 것 이다.

## void

void 는 console.log() 와 같이 아무것도 return 하지 않는 함수의 return type 으로 사용한다

```typescript
function NoReturn():void {
    console.log('Just Using Console Log')
}
```

## never

never 는 return 을 절대 하지 않는 함수 표현식 의 type 이다

```typescript
// error 를 만들어 return 이 불가능한 함수
function MakeError(msg:string):never {
    throw new Error(msg)
}

// error 를 return 하는 함수
function MakeFail():never {
    return error("Something Wrong!")
}

// 무한히 반복되는 함수
function Infinite():never {
    while(true) {
        // ...
    }
}
```

## 선택적 속성

일부 속성들은 있을 수도 있고 없을 수도 있을 것 이다.

```typescript
interface Person {
    age?:number;
    name?:string
}
```

위와 같이 선언한다면 , 없어도 에러를 표시하지 않는다.

## 읽기 전용 속성

읽기만 가능하며 수정이 불가능하게 만드는 경우 아래와 같다.

```typescript
interface Point {
    readonly x : number;
    readonly y : number;
}
```

이를 상속받은 객체가 수정을 하려 한다면 read-only property 에 제한 당하고있다는 에러 메시지가 표시되며 블록된다.

배열의 경우

```typescript
let test :ReadonlyArray<Type> = [1,2,3,4]
```

위와 같이 적용한다면 그 배열은 읽기전용 상태가 되어 수정이 불가능해진다.

## 함수 인자

함수의 인자는 기존 JS 와 다르게 매우 엄격하다

```typescript
function onlyOne(firstName:string , secondName:string) {
    return firstName + secondName
}
onlyOne('chobby') // error
onlyOne('chobby' , 'woobin') // success
onlyOne('chobby' , 'woobin' , 'kim') // error
```

위와 같이 인자의 수가 다르기만 해도 error 이다.