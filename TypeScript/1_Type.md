# 기본타입

```ts
let age:number = 30;
let isAdult:boolean = true;
let a:number[] = [1,2,3];
let a2:Array<number> = [1,2,3];

let week1:string[] = ['mon','tue','wed'];
let week2:Array<string> = ['mon','tue','wed'];
```

### 튜플 (Tuple)

```ts
let b:[string, number];

b = ['z', 1];
//b = [1, 'z'];  ->  X

b[0].toLowerCase();
//b[1].toLowerCase();  ->  X
```

### void, never


```ts
//void : 아무것도 반환하지 않는 함수의 타입, 로그만 찍음
function sayHello():void{
  console.log('hello');
}

//never : 항상 에러를 반환하거나 영원히 끝나지 않는 함수의 타입
function showError():never{
  throw new Error();
}
```

### enum

```ts
//enum : 비슷한 값들끼리 묶어줌, 아무것도 지정해주지 않으면 0부터 자동으로 지정됨.
enum Os {
  Winsow = 3,
  Ios = 10,
  Android
}

//숫자일 경우, 양방향으로 출력이 가능함, 문자로 할당해주는 경우는 단방향 맵핑만 가능함
console.log(Os[10]) //'Ios'
console.log(Os['Ios']) //10

let myOs:Os;

myOs = Os.Window; //특정 값만 입력하게 하고 싶을 때 사용함.
```

### null, undefined

```ts
let a:null = null;
let b:undefined = undefined;
```