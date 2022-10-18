# Chapter 2 - 3

저는 모든 챕터를 보면서 제가 인상깊었던 내용만 골라 정리해보았습니다.

그런데 어쩌다보니 딱 여섯 아이템이 골라졌네요 ㅎㅎ

## 아이템 9: 타입 단언보다는 타입 선언을 사용하기

요약: 타입 단언은 개발자가 타입스크립트 서버에게 어떤 변수의 타입을 강제로 알려주는 것을 뜻한다. 이 방식은 올바를 타입 체킹을 어렵게 만들기 때문에, 대부분의 경우에서는 타입 선언을 통해 타입스크립트로 하여금 해당 변수가 지정된 타입을 따라야만 함을 알려주는 것이 좋다.

<aside>
💡 56p. 변수의 접두사로 쓰인 `!` 는 `boolean` 의 부정문입니다. 그러나 접미사로 쓰인 `!` 는 그 값이 `null` 이 아니라는 단언문으로 해석됩니다.

</aside>

→ 변수 뒤에도 느낌표를 붙일 수 있다는 사실을 처음 알게 되었습니다. 그런데 이 문법은 자바스크립트엔 없고 타입스크립트에만 있는 것일까요?

## 아이템 10: 객체 타입 래퍼 피하기

요약: 자바스크립트의 원시 타입은 불변하며 메서드를 갖지 않는다. 하지만 null, undefined를 제외한 원시 타입의 경우 메서드를 갖고 있는 것처럼 작동한다. 예를 들어 string의 연산자가 사용될 때, 자바스크립트는 String 객체를 string 변수에 래핑한 뒤 메서드를 사용하고, 쓸모없어진 String 객체를 삭제하는 식으로 동작한다. 한 가지 유의할 점은 String 객체는 string 원시 타입을 포괄할 수 없다는 점이다. 실제 개발을 할 때는 객체 타입보다는 원시 타입을 바로 사용할 것을 권장한다.

<aside>
💡 60p. `string` 은 `String` 에 할당할 수 있지만 `String` 은  `string` 에 할당할 수 없습니다.

</aside>

## 아이템 11: 잉여 속성 체크의 한계 인지하기

요약: 타입이 명시된 변수에 리터럴 객체를 추가하면 타입스크립트의 ‘잉여 속성 체크’라는 기능이 동작하여 불필요하거나 부정확한 프로퍼티를 검사한다. 하지만 임시 변수에 객체를 추가하면 타입이 명시되어 있더라도 잉여 속성 체크가 작동하지 않는다. 이런 차이가 유용할 때도 있다. (DOM 객체를 할당할 때라든지)

## 아이템 13: 타입과 인터페이스의 차이점 알기

요약: 타입과 인터페이스는 유사한 점이 많지만 나름의 차이가 있다. 인터페이스는 부분집합의 개념으로만 확장되지만, 타입은 유니언, 인터섹션 등등의 복잡한 집합 연산이 가능하다.

<aside>
💡 70p. 타입스크립트 초기에는 인터페이스 접두사로 ‘I’를 붙이는 것이 관례였습니다. (C#에서 유래됨) 그러나 지금은 권장되지 않습니다.

</aside>

<aside>
💡 74p. 이번 아이템의 처음 질문으로 돌아가 타입과 인터페이스 중 어느 것을 사용해야 할지 결론을 내려 보겠습니다. 복잡한 타입이라면 고민할 것도 없이 타입 별칭을 사용하면 됩니다. 그러나 타입과 인터페이스, 두 가지 방법으로 모두 표현할 수 있는 간단한 객체 타입이라면 일관성과 보강의 관점에서 고려해 봐야 합니다. 일관되게 인터페이스를 사용하는 코드베이스에서 작업하고 있다면 인터페이스를 사용하고, 일관되게 타입을 사용 중이라면 타입을 사용하면 됩니다.

아직 스타일이 확립되지 않은 프로젝트라면, 향후에 보강의 가능성이 있을지 생각해 봐야 합니다. 어떤 API에 대한 타입 선언을 작성해야 한다면 인터페이스를 사용하는 게 좋습니다. API가 변경될 때 사용자가 인터페이스를 통해 새로운 필드를 병합할 수 있어 유용하기 때문입니다. 그러나 프로젝트 내부적으로 사용되는 타입에 선언 병합이 발생하는 것은 잘못된 설계입니다. 따라서 이럴 때는 타입을 사용해야 합니다.

</aside>

## 아이템 16: number 인덱스 시그니처보다는 Array, 튜플, ArrayLike를 사용하기

요약: 배열 순회 시 개발자는 배열의 인덱스가 number라고 가정하지만, 실제 런타임에 사용되는 키는 string 타입이다. 이런 배열 인덱스 시그니처의 불확실성 때문에 `for (const idx in item)` 를 사용한 루프는 `for (const item of arr)` 루프나 C 스타일 루프에 비해 몇 배나 속도가 느리다. 숫자를 키로 이용한 배열 작업을 하고 싶다면 Array 또는 튜플 타입을 사용하는 게 낫다. 다만 고작 배열 순회를 위해 Array같은 큰 타입을 사용하고 싶지 않다면 ArrayLike 타입을 사용하면 된다. 여기에는 길이와 숫자 인덱스 시그니처만 있다. 그러나 그 키는 여전히 문자열로 된 숫자일 수 있다.

```tsx
const tupleLike: ArrayLike<string> = {
  '0': 'A',
	'1': 'B',
	length: 2,
} // 정상
```

## 아이템 26: 타입 추론에 문맥이 어떻게 사용되는지 이해하기

요약: 개발을 할 때, 특정한 값들을 타입으로 잡아서 활용하고 싶을 때가 종종 있다. 이럴 때 ‘문맥으로부터 값을 분리 하지 않’고 개발하는 관점을 갖는 게 중요하다. (매개변수에 엄격한 타입을 설정하는 등) 다만 유연한 개발을 위해서는 타입 체커에게 우리가 원하는 깊이의 ‘상수 문맥’을 제공해야만 한다.

```tsx
// 튜플 타입 매개변수를 설정할 때, 타입 체커가 실제로 들어오는 인자를 배열로 오해하지 않도록
// readonly 키워드를 추가해준다
function panTo(where: readonly [number, number]) {/*...*/}

// as const 키워드는 변수뿐만 아니라 그 내부의 요소들까지도 상수임을 단언해준다
const loc = [10, 20] as const;

panTo(loc) // 정상
```