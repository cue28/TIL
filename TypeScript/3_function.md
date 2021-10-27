# 함수

### 매개변수 및 return 값 type 지정
```ts
function add(num1: number, num2: number): number {
  return num1 + num2
  //3번째 number은 리턴해야하는 값
}

//만약 리턴하는 값이 없다면(console.log) -> :void
function add(num1: number, num2: number): void {
  console.log(num1+num2)
}

function isAdult(age: number): boolean {
  return age > 19;
}
```
### 옵셔널
```ts
// ? -> optional parameter 선택적 매개변수
function hello(name?: string) {
  return `Hello, ${name || "world"}`;
  //interface처럼 옵셔널 값을 설정해줄 수 있다. name이 있으면 name 없으면 world.
}
//default 값을 설정해줄 수도 있다.
function hello(name = "world") {
  return `Hello, ${name}`;
  //interface처럼 옵셔널 값을 설정해줄 수 있다. name이 있으면 name 없으면 world.
}
```
```ts
//주의 : 옵셔널 값을 무조건 뒤에 와야한다.
function hello(name: string, age?: number): string {
  if(age !== undefined) {
    return `Hello, ${name}. I'm #{age} years old.`;
  } else {
    return `Hello, ${name}.`
  }
}

console.log(hello("Sam"));
console.log(hello("Sam", 30));

//만약 옵셔널 값이 앞에 위치하게 하고 싶다면
function hello(age: number | undefined, name: string): string {
  if(age !== undefined) {
    return `Hello, ${name}. I'm #{age} years old.`;
  } else {
    return `Hello, ${name}.`
  }
}

console.log(hello(30, "Sam"));
console.log(hello(undefined, "Sam"));
```
### 나머지 매개변수의 타입
```ts
function add(...nums: number[]) {
  return nums.reduce((result, num) => result + num, 0);
}

add(1,2,3); //6
add(1,2,3,4,5,6,7,9,10); //55
```
### this
```ts
interface User {
  name: string;
}

const Sam: User = {name: 'Sam'}

function showName(this:User){
  console.log(this.name)
}

const a = showName.bind(Sam);
a();
```
### 함수 오버로드
전달받은 매개변수의 갯수나 타입에 따라 다른 동작을 하게 만드는 것
```ts
interface User {
  name: string;
  age: number;
}

function join(name: string, age: string):string;
function join(name: string, age: number):User;
function join(name: string, age: number | string):User | string {
  if (typeof age === 'number') {
    return {
      name,
      age
    } else {
      return '나이는 숫자로 입력해주세요.';
    }
  }
}
```