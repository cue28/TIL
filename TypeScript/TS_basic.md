# TypeScript 기본기 다지기

Final Project 배포까지 마무리되고 발표 준비 중이다. Final에서 아쉬웠던 부분은 Redux, SCSS 사용으로 많이 난관이 예상되어 TS를 사용하지 않았다는 것이다. 개인 프로젝트와 리팩토링에 필요한 타입스크립트를 공부해보려고한다. 
<br/>

자바스크립트와 비슷하지만, 말 그대로 변수의 타입(number, string, arr 등)을 명시해준다는 것이 가장 큰 차이라는 것만 안다. 이번 프로젝트 때, Server 측에서 사용하여 어깨 넘어로 조금 보았지만, 아는 것은 이것뿐이다. 어떤 차이점이 있고, 어떠한 장점 때문에 많이들 사용하는지 궁금하다 ! 
<br/>
<br/>
 
타입스크립트를 사용하려면 가장 먼저 파일을 만들어야한다. 자바스크립트는 *.js, 타입스크립트는 *.ts 확장자를 사용한다.

```
$ npx create-react-app ts-tutorial --template typescript
```
```ts
const message: string = 1;
console.log(message);
```
라는 코드를 입력하면 에티어 상에서 오류가 발생하며, 터미널에서 tsc를 입력하면 ts 파일에서 명시한 값의 타입은 컴파일 되는 과정에서 모두 사라지게 된다.

```ts
let count = 0; // 숫자
count += 1;
count = '갑자기 분위기 문자열'; // 이러면 에러가 납니다!

const message: string = 'hello world'; // 문자열

const done: boolean = true; // 불리언 값

const numbers: number[] = [1, 2, 3]; // 숫자 배열
const messages: string[] = ['hello', 'world']; // 문자열 배열

messages.push(1); // 숫자 넣으려고 하면.. 안된다!

let mightBeUndefined: string | undefined = undefined; // string 일수도 있고 undefined 일수도 있음
let nullableNumber: number | null = null; // number 일수도 있고 null 일수도 있음

let color: 'red' | 'orange' | 'yellow' = 'red'; // red, orange, yellow 중 하나임
color = 'yellow';
color = 'green'; // 에러 발생!
```
여기까지는 간단하다. 타입을 설정해주면 된다. 장점도 금새 느낄 수 있었다. 타입을 설정해줌으로써 에러를 예방하여 디버그 시간을 줄여준다. 함수 타입도 정의할 수 있다.

```ts
function sum(x: number, y: number): number {
  return x + y;
}

sum(1, 2);
```
x, y 값에 number가 아닌 다른 값이 들어간다면 에러가 뜨며 컴파일이 되지 않는다.

 ```ts
function sumArray(numbers: number[]): number {
  return numbers.reduce((acc, current) => acc + current, 0);
}

const total = sumArray([1, 2, 3, 4, 5]);
```
배열의 내장 함수를 사용했을 때, 타입 유추가 잘 이루어지는 것에 편리함을 느낄 수 있다.

 
```ts
function returnNothing(): void {
  console.log('I am just saying hello world');
}
```
만약 함수에 아무것도 반환하고 싶지 않다면 void로 설정하면 된다. 
<br/>
<br/>

## 1. interface
---
interface는 클래스 또는 객체를 위한 타입을 지정할 때 사용하는 문법이다.
```ts
// Shape 라는 interface 를 선언합니다.
interface Shape {
  getArea(): number; // Shape interface 에는 getArea 라는 함수가 꼭 있어야 하며 해당 함수의 반환값은 숫자입니다.
}

class Circle implements Shape {
  // `implements` 키워드를 사용하여 해당 클래스가 Shape interface 의 조건을 충족하겠다는 것을 명시합니다.

  radius: number; // 멤버 변수 radius 값을 설정합니다.

  constructor(radius: number) {
    this.radius = radius;
  }

  // 너비를 가져오는 함수를 구현합니다.
  getArea() {
    return this.radius * this.radius * Math.PI;
  }
}

class Rectangle implements Shape {
  width: number;
  height: number;
  constructor(width: number, height: number) {
    this.width = width;
    this.height = height;
  }
  getArea() {
    return this.width * this.height;
  }
}

const shapes: Shape[] = [new Circle(5), new Rectangle(10, 5)];

shapes.forEach(shape => {
  console.log(shape.getArea());
});
```
위의 코드는 각 변수에 값들을 설정해주었다. 
<br/>
<br/>
타입스크립트에서는 constructor의 파라미터 쪽에 public 또는 private accessor를 사용한다면, 하나하나 직접 설정하는 수고스러움을 덜 수 있다.

```ts
// Shape 라는 interface 를 선언합니다.
interface Shape {
  getArea(): number; // Shape interface 에는 getArea 라는 함수가 꼭 있어야 하며 해당 함수의 반환값은 숫자입니다.
}

class Circle implements Shape {
  // `implements` 키워드를 사용하여 해당 클래스가 Shape interface 의 조건을 충족하겠다는 것을 명시합니다.
  constructor(public radius: number) {
    this.radius = radius;
  }

  // 너비를 가져오는 함수를 구현합니다.
  getArea() {
    return this.radius * this.radius * Math.PI;
  }
}

class Rectangle implements Shape {
  constructor(private width: number, private height: number) {
    this.width = width;
    this.height = height;
  }
  getArea() {
    return this.width * this.height;
  }
}

const circle = new Circle(5);
const rectangle = new Rectangle(10, 5);

console.log(circle.radius);
console.log(rectangle.width);

const shapes: Shape[] = [new Circle(5), new Rectangle(10, 5)];

shapes.forEach(shape => {
  console.log(shape.getArea());
});
```
public으로 선언된 값은 클래스 외부에서 조회할 수 있지만, private로 선언된 값을 클래스 내부에서만 조회할 수 있다. 따라서 circle은 조회할 수 있지만, rectangle의 width, height 값은 클래스 외부에서 조회할 수 없다.
<br/>
<br/>

## 2. 일반 객체 interface로 타입 설정하기
---
```ts
interface Person {
  name: string;
  age?: number; // 물음표가 들어갔다는 것은, 설정을 해도 되고 안해도 되는 값이라는 것을 의미합니다.
}
interface Developer {
  name: string;
  age?: number;
  skills: string[];
}

const person: Person = {
  name: '김사람',
  age: 20
};

const expert: Developer = {
  name: '김개발',
  skills: ['javascript', 'react']
};
Person과 Developer의 형태가 유사하다. 이런 경우 interface를 선언할 때, 다른 interfacefmf extents 키워드를 사용해서 상속받을 수 있다. 이렇게.

interface Person {
  name: string;
  age?: number; // 물음표가 들어갔다는 것은, 설정을 해도 되고 안해도 되는 값이라는 것을 의미합니다.
}
interface Developer extends Person {
  skills: string[];
}

const person: Person = {
  name: '김사람',
  age: 20
};

const expert: Developer = {
  name: '김개발',
  skills: ['javascript', 'react']
};

const people: Person[] = [person, expert];
```

## 3. Type Alias 사용하기
---
 
type은 특정 타입에 별칭을 붙이는 용도로 사용한다. 이를 사용하여 객체를 위한 타입을 설정할 수도 있고, 배열, 또는 그 어떤 타입이던 별칭을 지어줄 수 있다. 위에서 배운 interface와 비슷하다. 클래스와 관련된 타입은 interface를, 일반 객체 타입의 경우엔 그냥 type을 사용해도 괜찮다. 사실상 크게 상관은 없지만, 무엇이든 일관성 있게만 사용하면 된다. (interface VS type 기술 블로그 예약)

```ts
type Person = {
  name: string;
  age?: number; // 물음표가 들어갔다는 것은, 설정을 해도 되고 안해도 되는 값이라는 것을 의미합니다.
};

// & 는 Intersection 으로서 두개 이상의 타입들을 합쳐줍니다.
// 참고: https://www.typescriptlang.org/docs/handbook/advanced-types.html#intersection-types
type Developer = Person & {
  skills: string[];
};

const person: Person = {
  name: '김사람'
};

const expert: Developer = {
  name: '김개발',
  skills: ['javascript', 'react']
};

type People = Person[]; // Person[] 를 이제 앞으로 People 이라는 타입으로 사용 할 수 있습니다.
const people: People = [person, expert];

type Color = 'red' | 'orange' | 'yellow';
const color: Color = 'red';
const colors: Color[] = ['red', 'orange'];
```

## 4. Generics
---
제너릭은 타입스크립트에서 함수, 클래스, interface, type alias 를 사용하게 될 때, 여러 종류의 타입에 대하여 오환을 맞춰야 하는 상황에서 사용하는 문법이다.
<br/>
<br/>
### 함수에서 사용하기

객체 A와 객체 B를 합쳐주는 merge 라는 함수를 만든다고 가정하였을 때, 그런 상황에서는 A와 B가 어떤 타입이 올 지 모르기 때문에 any라는 타입을 쓸 수도 있다.
```ts
function merge(a: any, b: any): any {
  return {
    ...a,
    ...b
  };
}

const merged = merge({ foo: 1 }, { bar: 1 });
```
하지만, 이렇게 사용한다면 타입 유추를 할 수 없다. 결과가 any라는 것은 merged 안에 어떤 변수가 있는지 알 수가 없다는 것과 마찬가지이다. 바로 이런 상황에서 사용할 수 있다.
```ts
function merge<A, B>(a: A, b: B): A & B {
  return {
    ...a,
    ...b
  };
}

const merged = merge({ foo: 1 }, { bar: 1 });
function wrap<T>(param: T) {
  return {
    param
  }
}

const wrapped = wrap(10);
```
두 가지 예시를 사용한다면 파라미터로 다양한 타입을 넣을 수도 있고 타입 지원을 지켜낼 수 있다.
<br/>
<br/>

## 5. Interface 에서 Generics 사용하기
---
```ts
interface Items<T> {
  list: T[];
}

const items: Items<string> = {
  list: ['a', 'b', 'c']
};
 

 
Type 에서 Generics 사용하기
type Items<T> = {
  list: T[];
};

const items: Items<string> = {
  list: ['a', 'b', 'c']
};
```

<br/>
<br/>

## 6. Class 에서 Generics 사용하기
---
데이터를 등록할 수 있는 자료형이며, 먼저 등록(enqueue)한 항목을 먼저 뽑아올 수(dequeue) 있는 성절을 가지고 있는 Queue 이라는 클래스를 만들어보자.
```ts
class Queue<T> {
  list: T[] = [];
  get length() {
    return this.list.length;
  }
  enqueue(item: T) {
    this.list.push(item);
  }
  dequeue() {
    return this.list.shift();
  }
}

const queue = new Queue<number>();
queue.enqueue(0);
queue.enqueue(1);
queue.enqueue(2);
queue.enqueue(3);
queue.enqueue(4);
console.log(queue.dequeue());
console.log(queue.dequeue());
console.log(queue.dequeue());
console.log(queue.dequeue());
console.log(queue.dequeue());
```
터미널에서 작동 시킨다면,

```
$ tsc
$ node dist/practice

0
1
2
3
4
```

잘 작동한다.
<br/>
<br/>
여기까지 한다면, 타입스크립트를 리액트와 함께 스기위한 준비를 마친 것이라고 한다. 이제 본격적으로 타입스크립트를 사용해볼 것이다.
<br/>
<br/>
ref. https://react.vlpt.us/using-typescript/01-practice.html