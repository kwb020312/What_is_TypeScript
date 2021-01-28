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