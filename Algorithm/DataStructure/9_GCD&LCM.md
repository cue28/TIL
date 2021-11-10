# GCD / LCM

- 약수: 어떤 수를 나누어떨어지게 하는 수
- 배수: 어떤 수의 1, 2, 3, ...n 배하여 얻는 수
- 공약수: 둘 이상의 수의 공통인 약수
- 공배수: 둘 이상의 수의 공통인 배수
- 최대 공약수(GCD. Greatest Common Divisor): 둘 이상의 공약수 중에서 최대인 수
- 최소 공배수(LCM. Least Common Multiple): 둘 이상의 공배수 중에서 최소인 수

최대공약 (유클리드 호제법)

```js
const GCD = (min,max) ⇒ (min === 0) ? max : GCD(max, min%max)
```

```js
//최대공약수
function gcd(m, n) { 45 10 => 5
  if (m % n === 0) return n;
  return gcd(n, m % n);
}

//최소 공배수
function lcm(a,b) {
	return a * (b/gcd(m,n)) 45 * 10/5 => 90
}
```