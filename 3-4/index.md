# 챕터 4-5
## 선택된 item
### union의 interface 보다는 interface의 union을 사용하기 (item 32)
> 명확한 의미 전달을 위해, interface union을 잘 사용하자.
<details>
  <summary>예시</summary>

  ```typescript
  // 개선 전
  interface Layer {
    layout: FillLayout | LineLayout | PointLayout;
    paint: FillPaint | LinePaint | PointPaint
  }


  // 개선 후
  interface FillLayer {
    layout: FillLayout;
    paint: FillPaint;
  }
  interface LineLayer {
    layout: LineLayout;
    paint: LinePaint;
  }
  interface PointLayer {
    layout: PointLayout;
    paint: PointPaint;
  }
  type Layer = FillLayer | LineLayer | PointLayer;
  ```
</details>

- 장점
    1. type의 조합으로 발생하는, 의도치 않은 오용을 막을 수 있다.
    1. 사용 맥락에서 추가/누락에 대한 대응이 수월하다.
- 떠오른 질문
    - 명확한 의미 전달이 중요한 이유


### any type은 가능한 한 좁은 범위에서만 사용하기 (item 39)
> 왜 any를 쓰는지 고민하고, 좁은 범위로 쓰자
<details>
  <summary>예</summary>
  
  ```typescript
    // 1. array가 필요한 경우
    any[];

    // 2. object가 들어올 경우
    {[key: string]: any;}

    // 3. 특정 함수의 형태가 필요한 경우 
    () => any;
  ```
</details>

- 떠오른 질문
  - 왜 any를 쓰는게 나쁠까?
  - 좁은 범위의 any의 효용은 뭘까?

### 모르는 type의 값에는 any 대신 unknown을 사용하기(item 42)
> unknown은 모른단걸 명확하게 나타낸다!

- any의 대체제로 쓴다면, generic보다 의도를 나타낸 방법이 될 수 있다.
    <details>
      <summary>type단언을 해야 함을 명시한다.</summary>
      
      ```typescript
      function hello<T>(a: T) {
        console.log(a.say()); // error 발생 가능, type에선 에러 안날 수 있음
      }

      function hello(a: unknwon) {
        if (say in a) {  // 명확하게 check하도록 강제
          console.log(a.say());
        }
      }
      ```
    </details>

## 선정에 사용한 기준
1. 많이 선정한 것
1. 재미있는가
1. 실무에 적용하지 않으면 큰일 날 것 같은가
1. 공유가 되면 좋은가