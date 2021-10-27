# 리터럴, 유니론/교차 타입

### Literal Types
userName1처럼 정해진 string값을 가진 것
```ts
const userName1 = "Bob";
//userName1: "Bob"
let userName2 = "Tom";
let userName3: string | number = "Tom";
//userName2: string 또는 number
```
```ts
type Job = "police" | "developer" | "teacher";

interface User {
  name: string;
  job: job;
}

const user: User = {
  name: "Bob",
  job: "police"
}
```
### Union Types
| (세로줄)로 표시하며, A or B 의 `OR`의 의미
```ts
interface Car {
  name: 'car';
  color: string;
  start(): void;
}

interface Mobile {
  name: 'mobile';
  color: string;
  call(): void;
}
//식별 가능한 유니온 타입
function getGift(gift: Car | Mobile) {
  console.log(gift.color)
  if(gift.name === 'car') {
    gift.start();
  } else {
    gift.call();
  }
}
```
### Intersection Types
& (세로줄)로 표시하며, A and B 의 `AND`의 의미
```ts
interface Car {
  name: string;
  start(): void;
}

interface Toy {
  name: string;
  color: string;
  price: number;
}

//필요한 모든 기능을 한꺼번에 정의할 수 있음.
const toyCar: Toy & Car = {
  name: '타요',
  start(){},
  color: "blue",
  price: 1000,
}
```