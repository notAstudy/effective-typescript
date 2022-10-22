# 2/3장 범위(item 6~27)

<details>
<summary>item 8 - 타입 공간과 값 공간의 심볼 구분하기<summary>

```ts
type T1 = typeof p; // Person
type T2 = typeof email;
// (p: Person, subject: string, body: string) => Response

const v1 = typeof p; // object
const v2 = typeof email; // function
```

type의 관점에서 `typeof` 는 타입스크립트의 타입을 반환한다. 하지만 값에서 `typeof`는 자바스크립트 런타임의 `typeof`를 반환하게 되는데 JS의 런타임 타입은 `string, number, boolean, undefined, object, function` 뿐이다. 그래서 타입스크립트의 `typeof` 와 전혀 다른 타입을 반환 할 수 있다.

```ts
class Car {
...
}


const sampleValue = typeof Car; // sampleValue === 'function'
type TSampleType = typeof Car; // 타입은 Car 타입

declare let sampleFunction:TSampleType;
const c = new sampleFunction(); // c의 타입은 Car
```

위 예시처럼 타입이 반환되는 이유는 실제 클래스의 구현이 JS에서는 함수로 되어있기 때문에 `sampleValue`의 타입은 `function` 이 된다. 여기서 `TSampleType`은 인스턴스 타입이 아니라 생성자 타입이라는 점을 유의하자

</details>
  
<details>
<summary>item 9 - 타입단언 보다는 타입선언을 사용하기</summary>

```ts
interface ICar {
  name: string;
  price: number;
}

const audi: ICar = {
  name: "A6",
  price: 10000,
}; // 타입 declare

const kia = {
  name: "K5",
  price: 2000,
} as ICar; // 타입 assertion

// 둘 가 가능

const gm: ICar = {}; // error
const toyota = {} as ICar; // no problem

const hyundai: ICar = {
  name: "avante",
  price: 2500,
  fuelType: "Gasoline", // error
};

const ssangyong = {
  name: "musso",
  price: 1000,
  fuelType: "disel",
} as ICar; // no problem
```

</details>
