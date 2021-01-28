타입스크립트 에 대하여

이 저장소는 https://www.typescriptlang.org/docs/handbook/typescript-from-scratch.html
를 보고 참고하여 만들어졌음을 밝힘.

현재 JavaScript의 고질적인 문제를 해결하기 위하여 TypeScript 사용자가 늘어나고있다. 

<img src="gitImages\TS_Logo.png">

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