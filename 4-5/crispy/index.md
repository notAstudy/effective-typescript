# 선정한 items
## 28. 유용한 상태만 표현하는 타입을 지향하기
### 상태의 접근은 계획될 필요가 있습니다.
저는 때로 상태 하나를 여러군데에서 사용 했습니다. 그 결과 다양한 에러가 발생했고, 협력이 어려운 코드를 만들었습니다. 상태를 명시하는 속성은 따로 선언하는게 필요합니다. 


### 32. 유니온 인터페이스 보다 인터페이스 유니온 속성 사용하기
속성의 필요성에 따라, optional이면 하나의 객체로 관리하는 것도 좋은 방법이다.
```typescript
// someBooleanVal은 서로 연관이 있다고 합시다. 
interface BeforeChange {
  someBooleanVal?: boolean;
  someBooleanVal2?: boolean;
}

// 명시적으로 연관있는 두 변수 모두를 설정하거나, 하지 않도록 정의합니다.
interface AfterChange {
  someBooleanVal?: {
    1: boolean;
    2: boolean;
  }
}
```

- 37. 공식 명칭에는 상표 붙이기
포인트 계산 등 실수가 나오면 안되는 처리가 있다면, 사용해도 좋은 방법일 것 같습니다.

```typescript
interface Point {
  private _name: 'point'; // 다른 변수를 할당하는 연산에서 에러를 명시적으로 띄웁니다.
  value: number;
}

function 
```
- 42. 모르는 타입의 값에는 any대신 unknown 쓰기
## 선정 기준
- 내가 제대로 몰랐는가.
- 공유 되어야 의미 있는 내용인가. (혼자 지키는 것 보다 함께 지켰을때 더 좋은가?)
