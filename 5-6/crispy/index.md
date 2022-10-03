# 5/6장 범위 (items 45 ~ 57)
## 선정한 item
### 의존성 분리를 위해 미러 타입을 사용하기 (items 51)
> 특정 환경에 의존한 코드를 짤 때, 목적에 따라 라이브러리용으로 따로 선언하는 것도 좋은 접근이다.

- Node환경에서 사용되는 특정 type의 정의를 CRA등에서 사용할 때, 그냥 되니까 @types/node를 사용했던 기억이 있다. 해당 code가 동작하는 실행환경에서는 상관 없었겠으나, 외부 공개용 library를 짤때는 주의할 필요가 있을 것 같다.

### source map을 사용하여 typescript debugging하기 (items 57)
> typescript의 source map과 browser를 사용해서 debugging 하자

- console.log의 노가다는 빠르되, 정확하지 않다.
- react dev tool을 react를 사용할 때는 사용할 수 있으나, 기타 라이브러리를 쓸때는 console.log 밖에 사용하지 않았다.
- typescript에 기반한 frame work나 library들을 시도할 때 쓸만 할 것 같다.

## 선정의 기준
1. 내가 몰랐다.
2. 개인의 생산성과 관련해, 지키면 좋을 것 같다.
