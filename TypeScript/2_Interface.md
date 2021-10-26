# Interface

### 기본 사용법
```ts
interface User {
  name : string;
  age : number;
}

let user : User = {
  name : 'amy';
  age : 30
}

user.age = 10;
user.gender = 'male' //에러 발생

console.log(user.age)
```

### 옵셔널 & 읽기전용 값
```ts
interface User {
  name : string;
  age : number;
  gender? : string; //있어도 되고, 없어도 되는 옵셔널한 값
  readonly birthyear : number;
}

let user : User = {
  name : 'amy';
  age : 30;
  birthyear : 2000;
}

user.age = 10;
user.gender = 'male' 
user.birthyear = 1000; //에러 발생 (읽기전용)

console.log(user.age)
```
### 여러개의 키 한꺼번에 만들기
```ts
type Score = 'A' | 'B' | 'C' | 'F';

interface User {
  name : string;
  age : number;
  gender? : string; //있어도 되고, 없어도 되는 옵셔널한 값
  readonly birthyear : number; //읽기전용
  //[grade:number] : string; -> string을 값으로 가지는 number를 키가 여러개 존재 가능
  [grade:number] : Score; //Score를 값으로 가지는 number를 키가 여러개 존재 가능
}

let user : User = {
  name : 'amy';
  age : 30;
  birthyear : 2000;
  1 : 'A';
  2 : 'E'; //에러 발생
}

user.age = 10;
user.gender = 'male' 

console.log(user.age)
```
### 함수
```ts
interface Add {
  (num1:number, num2:number): number;
}

const add : Add = function(x, y) {
  return x + y;
}

add(10,20); //하나를 더 적거나 다른 타입값이 들어가면 에러 발생

interface IsAdult {
  (age:number):boolean;
}

const a:IsAdult = (age) => {
  return age > 19;
}

a(20); //true
```
### 클래스
```ts
//implements
interface Car {
  color : string;
  wheels : number;
  start() : void;
}

class Bmw implements Car {
  color = 'red';
  wheels = 4;
  start() {
    console.log('go..');
  }
  //interface에 있는 모든 값이 불어와저야 에러가 뜨지 않는다.
}
```
```ts
//implements
interface Car {
  color : string;
  wheels : number;
  start() : void;
}

class Bmw implements Car {
  color;
  wheels = 4;

  constructor(c:string) {
    this.color = c;
  }

  start() {
    console.log('go..');
  }
  //interface에 있는 모든 값이 불어와저야 에러가 뜨지 않는다.
}

const b = new Bmx('green);
console.log(b); //OK
b.start(); //OK
```
### 클래스 확장 (extends)
```ts
interface Car {
  color : string;
  wheels : number;
  start() : void;
}

interface Benz extends Car {
  door : number;
  stop() : void;
}

const benz : Benz = {
   door : 5,
   stop() {
     console.log('stop');
   },
  color : string; //원래 있었던 키, 값까지 설정해주어야 에러가 뜨지 않는다.
  wheels : number;
  start() : void;
}
```
```ts
interface Car {
  color : string;
  wheels : number;
  start() : void;
}

interface Toy {
  name : string;
}

interface ToyCar extends Car, Toy {
  price : number;
}
```