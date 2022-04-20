# 유닛테스트와 TDD (웹개발자를 위한 테스트 마스터 클래스🍯)

https://academy.dream-coding.com/courses/js-tdd

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

## 6일차: Jest Mock 심플버전, 더 나은 아키텍처로 코드 작성하는 법

```jsx
function check(predicate, onSuccess, onFail) {
  if (predicate()) {
    onSuccess('yes');
  } else {
    onFail('no');
  }
}

describe('check', () => {
  let onSuccess
  let onFail

  beforeEach(() => {
    onSuccess = jest.fn()
    onFail = jest.fn()
  })

  it('should call onSuccess when predicate is true', () => {
    check(() => true, onSuccess, onFail) // 이것이 커버리지의 대상이 된다.

    // expect 아무리 꼼꼼히 해봤자 coverage 에 포함은 안됨. 그니까 expect 하는걸로 커버리지 믿으면 안됨
    expect(onSuccess).toHaveBeenCalledTimes(1)
    // expect(onSuccess.mock.calls.length).toBe(1)
    expect(onSuccess).toHaveBeenCalledWith('yes')
    // expect(onSuccess.mock.calls[0][0]).toBe('yes')
    expect(onFail).toHaveBeenCalledTimes(0)
    // expect(onFail.mock.calls.length).toBe(0)
  })

  it('should call onFail when predicate is false', () => {
    check(() => false, onSuccess, onFail)

    expect(onFail).toHaveBeenCalledTimes(1)
    expect(onFail).toHaveBeenCalledWith('no')
    expect(onSuccess).toHaveBeenCalledTimes(0)
  })
})
```

- 현재 check 모듈의 테스트는 각 Callback 들이 호출되는 여부 및 매개변수만 체크하면 된다.
- 호출되는 Callback 들은 자기들만의 Test 가 따로 있을것이다. 따라서 간단히 Mocking만 하여 호출여부만 따지면 된다!!
- **커버리지에 포함되는 것은 코드의 실행여부일 뿐이다**. 그에따른 Assertion을 얼마나 꼼꼼히 짜는지는 전적으로 개발자에게 달려있다.

```jsx
// product_service_no_di.js
const ProductClient = require("./product_client");

class ProductService {
  constructor() {
    this.productClient = new ProductClient();
  }

  fetchAvailableItems() {
    return this.productClient
      .fetchItems()
      .then((items) =>
        items.filter((item) => item.available)
      );
  }
}

module.exports = ProductService;
```

```jsx
// product_client.js
class ProductClient {
  fetchItems() {
    return fetch('http://example.com/login/id+password').then((response) => response.json())
  }
}

module.exports = ProductClient
```

```jsx
// product_service_no_di.test.js
const ProductService = require("../product_service_no_di");
const ProductClient = require("../product_client");
jest.mock("../product_client");

describe("ProductService", () => {
  const fetchItems = jest.fn(async () => [
    { item: "🍦", available: true },
    { item: "🍕", available: false },
  ]);
  ProductClient.mockImplementation(() => {
    return {
      fetchItems,
    };
  });
  let productService;

  beforeEach(() => {
    productService = new ProductService();
    fetchItems.mockClear();
    ProductClient.mockClear();
  });

  it("should filter out only available items", async () => {
    const items = await productService.fetchAvailableItems();
    expect(items).toHaveLength(1);
    expect(items).toEqual([
      {
        item: "🍦", available: true,
      },
    ]);
  });
});
```

- 몇번이고 반복하지만, 단위 테스트는 **모듈 독립적**으로 해당 기능을 수행하기 위한 코드만을 작성해야한다
- 만약 다른 모듈에 의존성이 있다면, 다른 모듈의 환경에 영향을 받을 수가 있다(네트워크 에러 등등...)
- 따라서 의존성을 띄는 모듈이 있다면 반드시 해당 모듈을 Mock 해야 한다.
- describe 안의 맨 윗줄에 의존성있는 모듈을 Mock 하는 컨벤션 참 괜찮은것 같다.
- mock 테크닉(jest.mock 을 통해 불러온 모듈을 통째로 Mock 하여 `mockImplementation` 하기, 메서드를 미리 함수 mock 하여 이를 implementation 에 넣기)등을 눈여겨 봐두자.
- `jest.config.js` 에서 clearMocks가 true 이면 `beforeEach` 에서 `mockClear` 안해줘도 됨. false 이면 해줘야 하는데, 이는 팀이 선호하는 방향이 어떻느냐에 따라 달라질 수 있다.
- 이는 아직 완벽한 테스트코드는 아니다. 다음시간에 더욱 바람직한 방법으로 한다고 한다.

## 7일차: Stub과 Mock 의 적절한 사용법

Mock이란: 구현사항 X, 원하는 부분만 가짜흉내

Stub이란: 모듈의 실제 인터페이스를 최소한으로만 구현해 놓은 코드. 

### Stub 예제

```jsx
// stub_product_client.js
class StubProductClient {
  async fetchItems() {
    return [
      { item: "🍦", available: true },
      { item: "🍕", available: false },
    ];
  }
}

module.exports = StubProductClient;
```

```jsx
// product_service.test.js
const ProductService = require("../product_service");
const StubProductClient = require("./stub_product_client");

describe("ProductService - Stub", () => {
  let productService;

  beforeEach(() => {
    productService = new ProductService(
      new StubProductClient()
    );
  });

  it("should filter out only available items", async () => {
    const items =
      await productService.fetchAvailableItems();
    expect(items).toHaveLength(1);
    expect(items).toEqual([
      {
        item: "🍦",
        available: true,
      },
    ]);
  });
});
```

저번에 작성한 ProductService 테스트에서 ProductClient 를 Stub으로 만들어 Mock 대신 간편하게 사용할 수 있다. 이렇게 Mock 을 최대한 안 쓸수 있으면 안 쓰는 것이 낫다. 단, 호출 횟수 등의 Mock 전용 기능을 사용해야 하면 그때는 Mock 을 사용해야 한다.

또한 ProductService 를 DI 패턴으로 바꾸었다. 이렇게 의존성을 스스로 결정하지 않고 외부에서 받아와야 Stub을 주입받아 더욱 간편하게 테스트 할 수 있다. 이처럼 효율적인 테스트 코드를 작성하는 과정에서 자연스럽게 코드 품질이 향상되니 테스트란 여러모로 순기능을 하는 좋은 것이라 생각든다.

### Mock 을 사용해야할 때

```jsx
const UserService = require("../user_service");
const UserClient = require("../user_client");
jest.mock("../user_client");

describe("UserService", () => {
  const login = jest.fn(async () => "success");

  UserClient.mockImplementation(() => {
    return {
      login,
    };
  });

  let userService;

  beforeEach(() => {
    userService = new UserService(new UserClient());
    login.mockClear();
    UserClient.mockClear();
  });

  it("calls login() on UserClient when tries to login", async () => {
    await userService.login("abc", "abc");

    expect(login.mock.calls.length).toBe(1);
  });

  it("should not call login() on UserClient again if already logged in", async () => {
    await userService.login("abc", "abc");
    await userService.login("abc", "abc");

    expect(login.mock.calls.length).toBe(1);
  });
});
```

UserClient도 Stub으로 사용하면 좋겠으나 이처럼 메서드 호출 횟수를 테스트하고자 할 때는 Mock 을 사용할 수밖에 없다.

그리고 테스트는 Given-When-Then 의 순서대로 이루어져야 한다. 만약 expect 가 마지막에 있지 않고 중간에 뒤죽박죽 섞여있다면 그건 곧 테스트케이스를 나눠야 한다는 것을 의미한다!!

테스트를 잘 하기위한 좋은 아키텍쳐란 무엇인지 앞으로 꾸준히 고민하도록 하자 !!

## 8일차: 테스트의 원칙 - 좋은 테스트의 구조

테스트를 작성할 때마다 앞으로의 개념들을 항상 염두에 두면서 작성해 나가도록 하자!!

### 테스트의 비밀

Production에는 포함되지 않지만, 항상 repository에서 project와 함께 존재한다. 프로젝트의 기능이 변경될 때마다 항상 테스트코드도 유지보수해야한다.

1. 한번 작성된 테스트 코드는 영원히 유지보수 해야한다 ⇒ 테스트코드도 클린코드를 유지하도록 하자!!
2. 절대 내부 구현사항을 테스트하지 말자. 사용자 입장에서 API와 관련된 사항만 테스트 하도록 하자!!
3. 재사용성을 높이자. 반복되는 코드가 있으면 별도의 유틸리티로 빼도록 하자.
4. 배포용 코드와 철저히 분리. 테스트와 관련된 모든 코드, 목, 데이터들은 배포시 포함되지 않도록 주의를 기울이자!!!
5. 테스트코드를 통한 좋은 문서화의 효과를 누리도록 하자!!

### 좋은 테스트의 구조

1. Before(beforeEach, beforeAll)
2. a test: 준비, 실행, 검증 등의 3단계로 나뉘어짐. Arrange Act Assert(Triple A), Given When Then(GWT)
3. After(afterEach, afterAll)

예전에는 Triple A, GWT 를 주석으로 남겨서 구분을 하기도 했지만, 요즘 테스팅라이브러리는 많이 심플해졌기 때문에 코드상의 공백 정도로만 구분을 하는것이 가독성이 좋다.

Given 에서 준비과정이 반복되면 유틸을 만들어서 재사용 하는것이 좋다.

When 단계에서 의도적으로 실패를 해보도록 하자. 실패하지 않기 위해서 어떻게 코드 수정해야 할지 확인하자. 버그를 수정할 때 실패하는 테스트를 만들어서 버그가 발생하는 상황을 검증하여 테스트코드가 성공하도록 하자!!

Then 단계에서는 항상 마지막에 두자. 하나의 테스트에서 검사하는것이 너무 많으면, 너무 많이 검사하지 않나? 여러 테스트로 분리하면 좋지 않을까? 항상 고민하는 습관을 들이자.

## 9일차: 좋은 테스트의 원칙, 범위, 커버리지

### 좋은 테스트의 원칙: FIRST

- F(Fast): 테스트가 빠르게 수행되어야함. 느린것(파일,데이터베이스,네트워크)에 대한 의존성 낮추기. 많은 테스트를 빈번히 수행하도록 ⇒ Mock, Stub
- I(Isolated): 최소한의 유닛으로 검증. 어느부분에서 테스트가 실패했는지 알 수 있게 날카롭게
- R(Repeatable): 실행할 때마다 동일한 결과를 유지. (의존X, 환경에 영향을 받지 않도록 작성)
- S(Self-Validating): 내가 검증하지 말고 Assertion 라이브러리로 코드가 스스로 검증하도록. CI/CD 파이프라인에서 모든 테스트가 꾸준히 테스트되어 기존 테스트에 영향을 주는지 꾸준히 체크
- T(Timely): 시기적절하게 테스트코드 작성. 문제를 배포전에 잡도록, 사용자에게 배포되기 이전에 테스트코드 작성

### 좋은 테스트의 범위: Right-BICEP

어떤것을 테스트할지 막막할 때 Right-BICEP이 아주 좋은 척도가 된다.

- **Right: 모든 요구사항이 정상 동작 하는지 확인. 어떤 것을 집중해서?? ⇒ BICEP**
- B(Boundary conditions): 모든 코너 케이스에 대해 테스트를 하기. 잘못된 포맷의 인풋, null, 특수문자, 잘못된 이메일, 작은 숫자, 큰 숫자, 중복, 순서가 맞지 않음 ⇒ **CORRECT 원칙에 의거하여!!**
- I(Inverse relationship): 역관계를 적용해서 결과값을 확인. 일관성을 유지(덧샘 → 뺄셈, 추가 → 제거 시 원래대로 돌아오는지)
- C(Cross-check): 다른 수단을 이용해서 결과값이 맞는지 확인(추가된 과일 == 전체 과일 - 예전의 과일 갯수, A 알고리즘 == B 알고리즘)
- E(Error conditions): 불행한 경로에 대해 우아하게 처리하는가? 네트워크 에러, 메모리 부족, 데이터베이스 중지 등의 모든 에러 케이스에서 테스트가 통과하는지!
- P(Performance characteristics): 성능 확인은 테스트를 통해 정확한 수치로 확인. 성능 개선의 척도와 확인도 데이터를 통해 확인. Q) 테스트를 통해 성능 확인을 어떻게 수치화 하는가??

### CORRECT 원칙

함수를 테스트 할 때 다양한 조건, 상황에 대한 결괏값을 테스트 할줄 알아야 한다(ex. 나눗셈 시 0으로 나눴을때 등등..). **테스트 뿐만 아니라 좋은 코드 작성을 위한 원칙도 된다.**

- C(Conformance): 특정한 포맷을 준수하는지. 전화번호, 이메일, 아이디, 파일 확장자...
- O(Ordering): 순서 조건 확인하기. (학생의 순서가 id순서여야 하는 경우 순서가 잘못된 경우를 캐치하기)
- R(Range): 숫자의 범위. 제한된 범위보다 작거나 큰 경우
- R(Reference): 외부 의존성 유무, 특정한 조건의 유무. ~일때, ~가 되어 있을때, 어떤 특정한 상황/상태일때 이런 동작을 한다. 테스트코드를 작성하다가 예상치 못한 상황에서 오는 실패에 또다른 깨달음을 얻기도 함.
- E(Existence): 값이 존재 하지 않을 때 어떻게 동작? null, undefined, ‘’, 0
- C(Cardinality): 0-1-N 법칙에 따라 검증. 하나도 없을 때, 하나만 있을 때, 여러개가 있을때, 지나치게 많을때 코드의 동작을 확인
- T(Time): 상대, 절대 동시의 일들. 순서가 맞지 않은 경우, 소비한 시간, 지역 시간의 변화에 따라 코드가 어떻게 동작하는지.

## 10일차: TDD 실습

이번 실습을 하면서 깨달은 점이 정말 많다.. 내부 구현사항을 테스트하지 말고 사용자 입장에서 인터페이스 중심으로 테스트하라는 말을 명심하면서 해봤는데, 정말 테스트케이스가 쌓이면 쌓일수록 테스트와 구현코드를 유기적으로 왔다갔다 하는 재미가 쏠쏠했다. 하나의 케이스를 고민하고 그 실패 테스트를 해결해 나가는 과정이란.. 초록불이 켜지는 그 쾌감이란 이루 말할 수가 없었다.

‘최대한 간단히, 작은것 부터 시작하라.’ 인생 전반적으로 통용되는 말이다. 이 말을 테스트에서도 경험했다. 일단 하나의 요구사항, 케이스를 사용자 중심으로 면밀히 고민하고 그에대한 구현을 완성시키고, 이러한 과정을 계속 반복하니 간단한 코드인데도 어느 순간 테스트케이스가 꽤 많아진 것을 직접 느꼈다. 테스트에 대한 막연한 두려움을 TDD를 통해 쉽게 해소할 수 있을 것이란 자신감을 얻게 되었다.

근데 TDD를 하려면 요구사항이 명확해야 한다. 요구사항을 정의하고 사람이 머릿속으로만 테스트케이스를 작성해 나가는 것이란 은근히 힘든 일임은 분명하다. 나 역시 개발자이지만, 어느정도의 기획력과 다각도로 생각할줄 아는 힘을 갖춰야 한다는 것을 많이 깨달았다.

진짜 마지막으로, 리팩토링에 대한 자신감이 확실히 생겼다. 차곡차곡 열심히 만들어 놓은 테스트케이스. 이것들이 정말 든든한 동반자처럼 느껴졌다. 꾸준히 테스트를 제작하고 유지보수하는 연습을 해서 더 아껴주는 연습을 해야겠다. 구현사항을 테스트한 실수가 하나 있었는데, 사용성 및 향후 리팩토링을 위해서라도 인터페이스를 테스트해야 한다는 점을 꼭 명심하기로 하자!!
