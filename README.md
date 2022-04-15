# TIL-TestCoding

## 1일차: 테스트란 무엇인가? 언제 테스트를 해야할까? 테스트를 하는 이유, 장점

### 테스트란 무엇인가?
- 제품이 원하는 대로, 예상하는 대로 동작하는지 확인하는 과정
- 제품: 함수, 특정한 기능, UI, 성능, API 스펙 등.. => 다양한 소프트웨어 테스트가 있을 수 있다.
- 목표, 플랫폼, 환경에 따라 다양한 테스트가 있을 수 있다.
- JS 로 제품이 expectation 을 만족하는지를 확인하는 테스트 코드를 작성한다.

### 언제 테스트를 해야할까?
- 결론부터 말하자면, 개발 하면서 Automated QA 코드를 작성해야 한다!
- 예전에는 QA 팀이 수동으로 테스트 진행함. => bottleneck, 비용발생
- 그 후 Automated QA 코드를 개발후 QA 단에 갈 때 테스트늘 진행 => 여전히 bottleneck 발생
- 최종적으로, 개발단에서 개발을 진행하며 Automated QA 코드를 작성하여 많은 사항이 개선됨
- 장점: 자동화 시간, 속도 빨라짐, 쉽게 작성 가능, 높은 커버리지 => 모두 개발하면서 꼼꼼히 작성할 수 있었기에 가능한것!!
- 여전히 QA 팀은 필요함. 사용자 입장에서 좀 더 면밀한 테스트를 하기 위해!

### 테스트를 하는 이유, 장점
- 무엇보다 우리가 작성한 코드가 예상한 대로 동작할 거라는 **"큰 자신감"** 확보가 가능.
- 기능이 정상 동작
- 요구사항 만족 확률 상승(자세히 알아보고 이해하기 때문)
- 테스트 코드를 읽는 것 만으로 이슈를 예측할 수 있음
- 버그를 빠르게 발견할 수 있음
- 기존 소스를 자신감 있게 리팩토링 할 수 있음. => 이거 정말 내가 와닿는 장점!! 리팩토링은 항상 버그발생의 여지가 있다.
- 손쉬운 유지보수 가능
- 코드의 품질 향상
- 코드간 의존성을 낮춤: 효율적인 테스트 코드 작성을 위해서는 의존성을 낮춰야 하기 때문
- 좋은 문서화: 모듈 사용법, 상황에 따른 예측이 가능하여 테스트코드 자체가 좋은 문서가 됨.
- 시간 절약: 개발단계에서 실시간 버그 발견, 리팩토링, 유지보수 간편 => 결과적으로 시간을 절약하는 행동이다!!

## 2일차: 꼭 알아야 하는 테스트 피라미드
- Unit Test: 모듈 각각의 단위를 테스트
- Integration Test: 모듈들이 어우러져 특정 동작을 수행하는지 테스트
- E2E Test: UI, 사용자 테스트. 실제 사용자의 입장에서 테스트 하는것
- Unit Test 가 가장 비용이 적고 효율적으로, 버그를 잡기가 쉽다
- Unit Test 부터 많이 작성해 두는 것을 추천.
- 개발자 필수: Unit, Integration Test
- Integration 까지 하는 경우가 대부분. QA 가 크로스플랫폼 스크립트로 E2E테스트 작성
- 개발자가 E2E 하는 경우도 있음
- 플랫폼마다 E2E 테스트 어떻게 하는지 알아두면 좋음
- QA 만이 할 수 있는 E2E 테스트란?

## 3일차: TDD, CI/CD
- TDD란?: 작은 단위의 테스트 케이스를 먼저 작성하고 테스트를 만족하는 코드 작성, 그 후 요구사항을 모두 충족할 때까지 테스트케이스를 늘려 같은 작업을 계속 반복 하고 모든 요구사항을 작성하고 통과했다면 리팩토링으로 마무리하는 개발 방법론
- TDD의 장점: 테스트케이스 작성을 위해 요구사항의 검토를 강제하는 효과로, 요구사항을 먼저 면밀히 점검할 수 있다. 구현보다는 인터페이스 설계에 먼저 집중하기 때문에 decoupling이 용이하여 코드 퀄리티가 향상된다. 이에따라 자연스레 시스템 전반적인 설계가 향상된다. 부가적으로 이 모든 과정이 게임과도 같아서 개발 집중력을 향상시키는 효과가 존재한다.
- TDD를 꼭 해야 하는가?: 필수는 아니다. 그러나 사용자에게 배포되는 코드일때!! 코드가 Merge 되거나 코드리뷰받기 전 등 **코드가 완성되었을 때는 테스트가 같이 작성돼 있어야 한다**. 왜냐하면 CI 파이프라인에서 테스트 실행을 하는데, 모든 테스트를 실행하여 모든 버그를 미연에 확실히 잡아 CI의 목적성에 부합하도록 하기 위함이다. 또! 테스트가 같이 동봉돼있어야 코드에 대한 문서화 효과를 누릴 수 있다.
- TDD 언제 사용돼야 하는가?: 요구사항이 명확할 때(테스트케이스 작성 용이하니까), 비즈니스 로직일때, 협업시 명세서 역할(동료개발자에게 일 배분할때 테스트코드 제작하여 건네줌), 설계에 대한 고민이 필요할 때
- UI 는 TDD를 하진 않는다. 만들어두고 Visual Test or UI 테스트 코드 작성. UI와 분리된 비즈니스 코드를 TDD할 뿐이다.
- CI/CD: https://youtu.be/0Emq5FypiMM 영상 시첨하기. CI/CD 의 효과가 200% 발휘되기 위해서는 모든 테스트코드 작성이 선행돼야 한다.
- CI
  - 코드 변경사항(테스트코드 포함)을 주기적으로 빈번하게 머지해야 한다. 충돌방지 & 버그의 발생 단위를 줄이기 위함
  - 통합을 위한 단계 (빌드, 테스트, Merge)를 자동화해야 한다. 버그수정 용이(문제점 빠르게 발견), 코드 퀄리티 향상, 개발 생산성 향상 등 **이 모든 것은 테스트코드가 존재했을 때 빛을 발한다**
- CD: CI에서 준비된 Release를 Continuous Delivery(개발자 or 검증팀이 직접 검사후 수동 배포), Continuous Deploy(Release 준비 되자마자 배포 자동화)
- CI/CD 툴: **Jenkins, Buildkite**, Github Actions, GitLab CI/CD, Bitbucket Pipelines, CircleCI


## 4일차: 유닛 테스트, Jest 소개 및 환경설정

- Test Runner: 테스트를 실행 후 결과 생성, 보고(Mocha)
- Assertion: 테스트 코드 내에서 조건, 비교를 통한 테스트 로직(Chai, expect.js, better-assert)
- Test Runner, Assertion 이 모두 적용되는 라이브러리 ⇒ Jest!!
- Jest: 모든 JS 환경에서 심플하게 동작하는 Testing Framework
- Jest의 특징: zero config, snapshots 지원, isolated(Test 각각 자기자신만의 process), it expect 등의 great API, Fast AND Safe, Code Coverage 제공, Easy Mocking, Great Exceptions
- Jest 설치법

```jsx
npm i -D jest
npx jest --init // jest 환경 세팅
npm i -D @types/jest // VSCode 상에서 인터페이스 확인을 위해 필요. 공식문서와 함께 보면 좋음
```

- test 폴더에 src 폴더 트리구조 형태랑 똑같이 test 파일들 만들자.
- 커버리지 설정 변경: collectCoverage: false : 커버리지 감춘다. 가끔 보고싶을때 `jest --coverage`
- 자동 테스트 실행: `jest --watchAll` 은 전체 테스트 실행, `jest --watch`  는 커밋이 안된 파일들만 watch 수행. 내가 활발하게 작업중인 것만 선택적으로 테스트 가능~

## 5일차: 테스트에 관한 고민, 테스트 작성 팁(Coverage, 계층, async테스트)

- 테스트는 기술적인 측면에서는 전혀 어렵지 않다. 다만 실제 프로젝트에서 어떤 단위로 테스트케이스를 작성하고 어느 범위 까지 만들 것인가. 실제 프로젝트를 하면서 익혀 나갈 수밖에 없다.
- [공식문서의 Introduction](https://jestjs.io/docs/getting-started)을 모두 보고 Guides 는 Indexing 정도만 하도록 하자.
- toBe와 toEqual,matches,소수비교 등의 Matcher 들 눈에 익혀두고 resolves와 rejects, not 등의 AndNot 들의 타입이 있다는 것을 명심하자.
- **모든 단위 테스트는 독립적이어야 한다.** 공통적인 부분이 있다면 beforeEach 등을 쓰고 전체 시작전 하고싶은게 있다면 beforeAll 등을 쓰자.
- 에러 테스트 방법: expect 안에 에러가 실행되는 구문을 콜백과 함께 심어주고 toThrow 로 검증하자. 에러 검증 안한다면 —coverage 옵션으로 커버리지 체크할 때 커버리지가 부족한 것을 볼 수 있다. 난 테스트 할때 커버리지 옵션 키는게 더 나은것 같다. 커버리지 체크 테이블이 좀 크다면 화면을 넓히거나, 주기적으로 커버리지를 의식적으로 어떻게 체크하는지 확인하는 방안을 한번 마련해 보도록 하자.
- describe 안에서 또 테스트케이스를 묶고 싶다면 또 describe 사용할 수 있다. 이렇게 계층적으로 구성하는 것이 가능하다.
- async 테스트 방법

```jsx
function fetchProduct(error) {
  if (error === 'error') {
    return Promise.reject('network error')
  }
  return Promise.resolve({ item: 'Milk', price: 200 })
}

describe('Async', () => {
	// 비동기 끝나는 시기 수동명시: Assertion 불일치 시 타임아웃때문에 불편.
  it('async - done', (done) => {
    fetchProduct().then((item) => {
      expect(item).toEqual({ item: 'Milk', price: 200 })
      done()
    })
  })

	// Promise 리턴하면 타임아웃 문제가 해결되어 Assertion 불일치 시 타임아웃문제 해결 가능
  it('async - return', () => {
    return fetchProduct().then((item) => {
      expect(item).toEqual({ item: 'Milk', price: 200 })
    })
  })

	// 테스트 콜백이 async 일때도 마찬가지임
  it('async - await', async () => {
    const product = await fetchProduct()
    expect(product).toEqual({ item: 'Milk', price: 200 })
  })

	// AndNot 타입 사용 => expect를 리턴하는 것을 보니 Matcher 실행 결과를 Promise화 하는걸까??
  it('async - resolves', () => {
    return expect(fetchProduct()).resolves.toEqual({
      item: 'Milk',
      price: 200,
    })
  })
  it('async - rejects', () => {
    return expect(fetchProduct('error')).rejects.toBe('network error')
  })
})
```

여기서 알 수 있는 것은, 테스트할 함수가 비동기일 경우 done 함수 인자를 설정하여 비동기의 종료시점을 명시화 하거나, 테스트 콜백이 Promise 를 리턴해야 한다는 점이다(async function 같은 경우에도 undefined 가 resolve된 Promise 를 리턴한다) Promise 를 리턴한다는 것을 Test Runner 가 감지해야 비동기로 이루어지는 로직을 테스트 할 수 있다. 만약 Promise 를 리턴하지 못한다면, Test Runner 가 동기적으로 종료되어 Assertion이 불일치 하더라도 테스트가 성공되는 부작용을 낳는다.
