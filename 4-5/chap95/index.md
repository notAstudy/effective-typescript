# 선정한 items

<details>
<summary> item 31 - 타입주변에 null 값 배치하기 </summary>

어떤 값의 null 여부가 다른 값의 null 여부에 암시적으로 관여하도록 설계하면 안된다.

```ts
function extent(numberList: number[]) {
  let min, max;

  for (const numberValue of numberList) {
    if (!min) {
      // min이 undefined 또는 0 이면 max 또한 변경되는 구조
      min = numberValue;
      max = numberValue;
    } else {
      min = Math.min(min, numberValue);
      max = Math.max(max, numberValue);
    }
  }

  // numbrList.length < 1 이면 return 값은 [undefined, undefined] 가 된다.
  return [min, max];
}
```

</details>

<details>
<summary>item 32 - 유니온의 인터페이스 보다는 인터페이스 유니온 사용하기</summary>
타입 구조를 손 댈 수 없는 API Response 와 같은 경우라면 인터페이스의 유니온을 사용하여 속성 사이의 관계를 모델링 할 수 있음

```ts
interface IName {
  name: string;
}

interface IPersonWithBirth extends IName {
  placeOfBirth: string;
  dateOfBirth: Date;
}

type Person = IName | IPersonWithBirth;

function eulogize(person: Person) {
  if ("placeOfBirth" in person) {
    const { placeOfBirth, dateOfBirth } = p;
  }
}
```

</details>

<details>
<summary>item 33 - string 타입보다 더 구체적인 타입 사용하기</summary>

```ts
interface IAlbum {
  artist: string;
  title: string;
  releaseDate: string;
  recodingType: string;
}

const someAlbum: IAlbum = {
  artist: "에스파",
  title: "next level",
  releaseDate: "August 3, 2020",
  recodringType: "LIVE",
};

const anotherAlbum: IAlbum = {
  artist: "unkwon",
  title: "밀양 아리랑",
  releaseDate: "08. 22. 1400",
  recodingType: "live",
};
```

위 예시에서 `someAlbum` 은 에스파의 'next level' 이라는 곡의 정보이다. 그리고 밀양 아리랑에 대한 곡 정보가 있다. 제목과 가수에 `string` 타입을 설정한 부분은 이상해 보이지 않는다. 하지만 날짜와 녹음 타입에 대한 정보가 `string` 이라면 문제를 일으킬 수 있다.

`releaseDate` 타입이 `string` 이면 위 예시같은 표기가 가능하다. 하지만 이는 data를 가져다 사용하는 사람의 입장에서 보면 여간 불편한게 아니다. 예를 들어서 앨범 발매일로부터 얼마나 지났는지 계산해주는 기능을 개발한다고 생각해보자. `releaseDate` 에는 위 예시처럼 8월에 대한 표현이 `08` 또는 `August`, 더 나아가서 `8`, `8월` 등등 다양하게 넣어도 아무런 문제가 되지 않는다. 이 값에 대해서 모두 다 대응을 해줘야 하는데 불가능에 가까울 뿐 아니라 타입을 제한하는 방식이 더 효율적으로 보인다.

`recordingType` 의 타입이 `string` 이다. 각각 두 곡은 라이브 환경에서 녹음 했지만 서로 표기 방식이 다르다는 문제점을 가지고 있다.

이런 문제를 해결하기 위해서 속성에 대한 data input 이 정해져 있는 값은 넓은 타입보다는 훨씬 좁은 타입을 사용하여 같은 의미를 가진 다른 값이 들어오는 것을 방지해 주어야 한다.

</details>

<details>
<summary>item 36 - 해당 분야의 용어로 타입 이름 짓기</summary>
  - 같은 대상이나 같은 의미를 가지면 같은 용어(단어)로 표현해야 한다.
  - entity, data, info, thing, item, object 와 같은 단어는 피해야한다.
  물론 맥락에서 해당 단어가 큰 의미를 가질 수 있지만 그럴 경우에는 prefix 또는 postfix를 이용하여 부가적으로 설명해줘야 한다.
</details>

<details>
<summary>item 38 - any 타입은 가능한 좁은 범위에서만 사용하기</summary>
any 타입은 타입체커를 무효화 하는 기능을 하는데 이는 가끔 필요할 때가 있다. 하지만 any 를 남용하는 것은 타입스크립트의 사용도를 떨어뜨리고 버그 발생 확률을 높인다. 그래서 올바른 any 사용법을 익히는게 중요하다.

```ts
function processAnimal(value: Animal) {
  //...
}

const person = getPerson(); // x의 타입은
processAnimal(person); // 오류가 발생

// 타입 선언 함수
function typeDeclaration() {
  const person: any = getPerson();
  processAnimal(person); // 오류X
}

// 타입 단언 함수
function typeAssertion() {
  const person = getPerson();
  processAnimal(person as any); // 오류X
}
```

`typeDeclaration` 함수와 `typeAssertion` 함수는 `processAnimal`에 `person` 이 할당되지 못하는 이슈를 해결해준다. 하지만 `typeDeclaration` 함수처럼 tpye을 선언하는 방식은 좋은 방법이 아니다. 왜 일까?

현재 예시에서는 `person` 변수에 값을 할당하고 `processAnimal` 을 호출하고 함수가 종료된다. 하지만 실제 코드에서는 `person` 변수를 가지고 추가적인 로직을 충분히 설계할 수 있다. 이런 관점에서 코드를 다시 본다면 타입 선언이 어떤 이유에서 안 좋은지 추측이 가능할 것이다. `person` 을 `any` 로 선언해버리면 타입을 단언해주지 않는 이상 함수 내부 컨텍스느에서는 `any` 타입이다. 이와는 반대로 `typeAssertion` 에서는 함수를 호출하면서 단언을 해주었기 때문에 `typeAssertion`함수 실행 컨텍스트에는 `person` 이 존재하지 않는다.

위와 같은 현상은 타입 선언과 단언에서 오는 차이가 아니다. 단언과 선언을 예시로 들어서 혼동할 수 있다. 아래 예시를 보자

```ts
function typeAssertion2() {
  const person = getPerson() as any;
  processAnimal(person); // 오류X
  // 이후 person 타입은 any
}
```

타입 단언을 사용해도 실행 컨텍스트가 같다면 `Person` 은 `any` 타입이 되어버린다. 이처럼 `any`를 사용할 때는 각별한 주의가 필요하다 `any` 가 편리하지만 편리함의 함정에 속아버리면 프로그램을 망칠 수 있다.

</details>
  
<details>
<summary>item 39 - any를 구체적으로 변형해서 사용하기</summary>
타입스크립트에서 any 타입은 모든 타입을 아우르는 범위가 가장 큰 타입이라고 한다. 이런 타입을 사용할 때 구체적으로 타입을 변형해서 사용한다면 타입스크립트의 사용성을 높일 수 있다.

```ts
function hasTweleveLetterKey(obj: { [key: string]: any }) {
  for (const key in obj) {
    if (key.length === 12) {
      return true;
    }
  }
  return false;
}
```

위 예시처럼 함수에 주어진 매개변수가 객체지만 내부를 알 수 없는 경우는 `{[key: string]: any}` 대신 `object` 타입을 사용할 수 있다.

</details>
