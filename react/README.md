# TDD와 리액트 테스트 (프론트엔드개발자를 위한 테스트 마스터 클래스 🍯)

https://academy.dream-coding.com/courses/react-tdd-invite-only-n9M24kN6ahvtS8Dw

## 1일차: React Testing 준비

### 마음가짐

어떻게 React 라는 구체적인 Application 을 테스트하는지, 어떻게 해야 촘촘하게 테스트 할 수 있는지 100% 자신감을 이번 강의에서 깨우치도록 하자.

### 구현만 된 상태인, TDD가 아닐경우?

최소한의 시간, 최소한의 테스트로 App의 70퍼센트를 커버하는 효율적인 테스트를 작성만 해두면, 나머지 테스트 혹은 UI 테스트를 하지 않아도 자신감 뿜뿜 가능. 이 70퍼센트를 어느 테스트로 커버해야하야 안정감을 느낄 수 있는지? 의 관점으로 접근하면 많이 도움됨.

### 공식문서를 먼저 훑어봐야 한다

- React 공식사이트: TESTING 섹션을 한번씩 훑어보기(테스팅에 대한 얘기, 프레임워크&라이브러리 추천, 커뮤니티의 진행방식 및 권장사항 확인) * Rendering component trees(단위테스트, 통합테스트), Running a complete app(E2E테스트)
- CRA 사이트: Testing 파트. CRA 에서 테스팅 라이브러리가 뭐뭐 포함돼있는지 확인.
- Jest, React Testing Library: React, CRA 사이트에서는 너무 간략하게 설명돼있어서 직접 라이브러리 문서를 보고 공부해와야 한다.

## 2일차: 기존 프로젝트에 테스트 추가하는 방법1 - presenter 만들기

기존 프로젝트에 테스트를 추가하려면 UI로부터 비즈니스 로직을 presenter 라는 클래스로 떼내어 UI와 비즈니스 로직을 분리하는 방법을 사용하면 좋다. 이렇게만 해도 전반적인 애플리케이션의 로직을 테스트하는 것이 가능하므로

- 굳이 복잡하게 React Testing Library 사용하여 컴포넌트 테스트를 하지 않고
- Jest 만을 이용할 수 있으며
- E2E 테스트를 하지 않아도 된다.

따라서 적은 시간으로 최대한 80퍼센트 테스트 커버리지 수준의 효율(실제로는 아니지만)이 발생할 것이라는 자신감이 뿜뿜 생긴다!!

### Presenter란?

UI에서 처리해야할 로직을 담는 클래스다. presenter 를 사용하는 방법은 MVP 모델을 이용하여 View 와 Presenter 사이에 인터페이스를 주고받는 방식도 있으나, 해당 모델 없이 presenter 만 사용해도 많이 개선할 수 있다.

### React 에서 좋은 테스트를 작성하는법

- 비즈니스로직이 컴포넌트 안에서 의존하고 있으면 React Testing Library 를 사용해야 하므로 테스트성이 떨어진다. ⇒ **비즈니스 로직을 분리하여 Jest 만 사용하도록 해야 한다.**
- 로직이 React 에 결합돼 있으면 UI View 라이브러리 변경에 따른 재사용성이 떨어진다. ⇒ **비즈니스 로직을 Presenter 로 분리해야 한다.**
- **최대한 View는 심플하게, 멍청하게 작성**해야 한다: KISS 원칙. [https://www.youtube.com/watch?v=jafa3cqoAVM&t=24s](https://www.youtube.com/watch?v=jafa3cqoAVM&t=24s)

## 3일차: 기존 프로젝트에 테스트 추가하는 방법2 - Unit Test 작성하기

음.. Unit test 작성에 대한 특이사항은 딱히 없었다. 그냥 작성하면 되고, 근데 작성하면서 의문점이 든게, Presenter 클래스를 순수함수의 집합으로 두면 안될까? 였다. this 에서 데이터를 관리하는 형태였는데, 찝찝하네.. 이걸 React 의 상태와 동기화 해야 하니까.. 어딘가에서 개발자의 실수로 동기화 안되면 어떡하지? Presenter 는 그냥 값을 받고 뱉는 역할을 하는게 더 바람직하지 않을까? 라는 생각을 해보았다.

그리고 또다른 깨달음!! immutable 한 배열 등을 뱉어낼때, 변동사항 없는 요소는 굳이 새로 생성하지 않아도 된다는 것. 굳이 또 생성한다면, 컴포넌트에 전달될 prop 값이 변화되어 렌더링 최적화에 불리하게 된다. 그니까 immutable 한 배열을 만들더라도 최적화를 꼭 고려해서 새로 만들 필요 없는 객체는 새로 만들지 않도록 해야한다.

테스트에서도 이러한 사항이 지켜졌는지 녹여내야 한다. (toBe. 객체의 참조값이 같은지)

## 4일차: 첫번째 컴포넌트 테스트하기

- React Testing Library: 컴포넌트의 내부 구현사항보단 사용자의 입장을 고려하여 손쉽게 테스트 할 수 있도록 도와주는 라이브러리
- Matcher 를 사용하기 위해선 jest-dom 을 설치해야한다 (**devdependency 에 설치해야 동작한다!!)**
- Core API 와 Query 를 잘 살펴보고 그 후 jest-dom 문서에서 Matcher 들도 살펴보며 이를 어떻게 매칭시킬지 자주 고민하자
- fireEvent 보단 userEvent 를 사용하자. fireEvent 는 low level 이고 userEvent 가 사용자가 발생시키는 이벤트에 더 가깝다.

```jsx
import React from 'react'
import { render, screen } from '@testing-library/react'
import '@testing-library/jest-dom'
import HabitAddForm from '../habitAddForm'
import userEvent from '@testing-library/user-event'

describe('HabitAddForm', () => {
  let onAdd
  let input
  let button

  beforeEach(() => {
    onAdd = jest.fn()

    render(<HabitAddForm onAdd={onAdd} />)
    input = screen.getByPlaceholderText('Habit')
    button = screen.getByText('Add')
  })
  it('has input and add button', () => {
    expect(input).toBeInTheDocument()
    expect(button).toBeInTheDocument()
  })

  it('calls onAdd prop when add button is clicked and valid habit is entered', () => {
    // fireEvent.change(input, { target: { value: 'New Habit' } })
    // fireEvent.click(button)

    userEvent.type(input, 'New Habit')
    userEvent.click(button)

    expect(onAdd).toHaveBeenCalledWith('New Habit')
  })

  it('does not call onAdd when the habit is empty', () => {
    userEvent.type(input, '')
    userEvent.click(button)

    expect(onAdd).toHaveBeenCalledTimes(0)
  })
})

```

## 5일차: 나머지 컴포넌트 테스트하기

### 접근성 준수를 유도하는 React Testing Library 들의 쿼리..

React Testing Library 들의 쿼리들은 정말 좋은것 같다.. 왜냐면 모든 쿼리가 접근성 준수를 유도하는 아주 좋은 쿼리들이기 때문이다. 쿼리하기 애매한 Element 들이 있다면 그것은 곧 접근성을 준수 못했다는 것. 예를들어 아무 텍스트도 없는 아이콘만 있는 버튼이 있다면, 아이콘에 alt 를 지정하거나 버튼에 title 을 주거나 해서 쿼리가 가능하게 만들면 된다. 이렇게 하면 자연스레 접근성이 준수가 된다..!! data-testid 만들려고 하지 말고 앞으로 최대한 쿼리에 맞게 요소들을 아주 집요하게 세팅해보자..

### 컴포넌트 테스트 자신감 뿜뿜 하는법!

1. 처음에 스냅샷테스트로 간편하게 렌더링 테스트를 한다.
2. 이벤트를 발생시켜 props로 전달된 콜백이 잘 수행되는지 테스트한다.

이 2가지만 제대로 하더라도 역시 80%자신감 커버리지가 완성된다.. 

### 부모도 일일히 다시 테스트 해야하는가??

여기서 내가 의문이 든것!! 부모로부터 콜백을 Prop Drilling 한 상태에서 자식 컴포넌트에서 이미 테스트를 만들어 놨는데 부모에서 똑같은 로직을 테스트하는게 결코 옳은 것일까? 정답은 테스트를 하는게 맞긴 하다는 것이다. 왜냐면 어쩔수 없이 부모로부터 전달된 콜백이 호출됐는지 확인해야 하니까. 그렇지만 똑같은 테스트로직을 또 만든다는 것은 매우 비효율적이긴 하다. 여기서 Prop Drilling 이 왜 테스트에 비효율적인지의 이유가 여실히 드러난다. Prop Drilling 하지말자. **상태관리 라이브러리를 열심히 공부하자!!!!**

## 6일차: App 컴포넌트 통합테스트하기

컴포넌트 테스트까지는 스냅샷, 콜백 수행 테스트로 자신감을 키울 수 있었다면, App 컴포넌트 통합테스트를 할 때는 이와 별개로 앱을 동작시키는 것 처럼 코드를 작성해야 한다.

수업에서 배운 소스는 Element 를 뽑아올 때 Index를 하드코딩한 경향이 강하고, 심지어 DOM 속성까지 참조하는 모습을 볼 수 있었다. 솔직히 말하자면 나는 이런 소스를 보면서 조금 불안함을 느꼈다. 일단 옆에 붙어있는 서로 다른 요소들을 getAll~ 쿼리를 해서 얻은 것들이 index 가 같다고 해서 adjacent 하다는 보장이 없다. 만약 동일한 것이 다른 컨테이너에 있었다면??

그리고 Mock 데이터에 너무 의존하여 하드코딩한 경향도 큰 것같고, testId를 안 써도 될 상황에 쓰면서 접근성도 향상도 안됐고.. 주어진 query 나 jest-dom Matcher 들을 잘 활용하지 않고, 전반적으로 방어적인 테스트 코드가 아닌것 같아서 좀 아쉬웠다.

그래서 아래의 수업 예제 소스를 다음과 같이 수정해 보았다.

### 수정 전

```jsx
// 수정 전
import { render, screen } from '@testing-library/react'
import userEvent from '@testing-library/user-event'
import React from 'react'
import renderer from 'react-test-renderer'
import App from '../app'
import HabitPresenter from '../habit_presenter'

describe('App', () => {
  let presenter
  beforeEach(() => {
    presenter = new HabitPresenter([
      { id: 1, name: 'Reading', count: 0 },
      { id: 2, name: 'Running', count: 0 },
      { id: 3, name: 'Coding', count: 1 },
    ])
  })

  it('renders', () => {
    const component = renderer.create(<App presenter={presenter} />)
    expect(component.toJSON()).toMatchSnapshot()
  })

  describe('Component', () => {
    beforeEach(() => {
      render(<App presenter={presenter} />)
    })

    it('counts only active habits', () => {
      const button = screen.getAllByTitle('increase')[0]
      userEvent.click(button)
      const count = screen.getByTestId('total-count')
      expect(count.innerHTML).toBe('2')
    })

    it('adds new habit', () => {
      const newHabit = 'New Habit'
      const input = screen.getByPlaceholderText('Habit')
      const button = screen.getByText('Add')
      userEvent.type(input, newHabit)
      userEvent.click(button)
      const addedName = screen.getAllByTestId('habit-name')[3]
      expect(addedName.innerHTML).toBe(newHabit)
      const addedCount = screen.getAllByTestId('habit-count')[3]
      expect(addedCount.innerHTML).toBe('0')
    })

    it('deletes an item', () => {
      const first = screen.getAllByTitle('delete')[0]
      userEvent.click(first)
      const next = screen.getAllByTestId('habit-name')[0]
      expect(next.innerHTML).not.toBe('Reading')
    })

    it('increases the counter', () => {
      const button = screen.getAllByTitle('increase')[0]
      userEvent.click(button)
      const count = screen.getAllByTestId('habit-count')[0]
      expect(count.innerHTML).toBe('1')
    })

    it('decreases the counter', () => {
      const button = screen.getAllByTitle('decrease')[2]
      userEvent.click(button)
      const count = screen.getAllByTestId('habit-count')[2]
      expect(count.innerHTML).toBe('0')
    })

    it('resets all counters', () => {
      const button = screen.getByText('Reset All')
      userEvent.click(button)
      screen.getAllByTestId('habit-count').forEach((count) => {
        expect(count.innerHTML).toBe('0')
      })
    })
  })
})
```

### 수정 후

```jsx
// 수정 후
import { render, screen, within } from '@testing-library/react'
import userEvent from '@testing-library/user-event'
import '@testing-library/jest-dom'
import React from 'react'
import renderer from 'react-test-renderer'
import App from '../app'
import HabitPresenter from '../habit_presenter'

describe('App', () => {
  const habits = [
    { id: 1, name: 'Reading', count: 0 },
    { id: 2, name: 'Running', count: 0 },
    { id: 3, name: 'Coding', count: 1 },
  ]
  let presenter

  beforeEach(() => {
    presenter = new HabitPresenter(habits)
  })

  it('renders', () => {
    const component = renderer.create(<App presenter={presenter} />)
    expect(component.toJSON()).toMatchSnapshot()
  })

  describe('Component', () => {
    beforeEach(() => {
      render(<App presenter={presenter} />)
    })

    it('counts only active habits', () => {
      const countWrapper = screen.getByTitle('total count')

      const totalCount = habits.reduce((totalCount, item) => {
        if (item.count > 0) {
          return totalCount + 1
        }
        return totalCount
      }, 0)
      expect(countWrapper).toHaveTextContent(String(totalCount))
    })

    it('adds new habit', () => {
      const newHabit = 'New Habit'
      const input = screen.getByPlaceholderText('Habit')
      const button = screen.getByText('Add')

      userEvent.type(input, newHabit)
      userEvent.click(button)

      // testid 해야될 때: 쿼리로 도저히 해결 못하는것.
      // 핵심은 구분되는 특징이 없고 오직 순서로만 찾아야 할때,
      // 특정 장소를 좁혀 그곳에서 쿼리를 수행해야 할때(Container)
      const habits = screen.getByTestId('habit-list')
      const addedHabit = within(habits).getAllByRole('listitem').slice(-1)[0] // last item
      const addedName = within(addedHabit).getByText(newHabit)
      const addedCount = within(addedHabit).getByText('0')
      expect(addedName).toBeInTheDocument()
      expect(addedCount).toBeInTheDocument()
    })

    it('deletes an item', () => {
      const first = screen.getAllByTitle('delete')[0]

      userEvent.click(first)
      const habits = screen.getByTestId('habit-list')
      const deletedHabitName = within(habits).queryByText('Reading')

      expect(deletedHabitName).not.toBeInTheDocument()
    })

    it('increases the counter', () => {
      const habits = screen.getByTestId('habit-list')
      const firstHabit = within(habits).getAllByRole('listitem')[0]
      const button = within(firstHabit).getByTitle('increase')

      const beforeCount = Number(within(firstHabit).getByTitle('count').textContent)
      userEvent.click(button)

      const afterCount = Number(within(firstHabit).getByTitle('count').textContent)
      expect(afterCount).toBe(beforeCount + 1)
    })

    it('decreases the counter', () => {
      const habits = screen.getByTestId('habit-list')
      const firstHabit = within(habits).getAllByRole('listitem')[0]
      const button = within(firstHabit).getByTitle('decrease')

      const beforeCount = Number(within(firstHabit).getByTitle('count').textContent)
      userEvent.click(button)

      const afterCount = Number(within(firstHabit).getByTitle('count').textContent)
      expect(afterCount).toBe(beforeCount - 1 < 0 ? 0 : beforeCount - 1)
    })

    it('resets all counters', () => {
      const button = screen.getByText('Reset All')

      userEvent.click(button)

      const habits = screen.getByTestId('habit-list')
      within(habits)
        .getAllByTitle('count')
        .forEach((count) => {
          expect(count).toHaveTextContent('0')
        })
    })
  })
})

```

### 깨달은 점

여기서 깨달은점 2가지가 있다.

1. **adjacent 한 것은 within 함수를 사용해서 쿼리를 날려라.** adjacent 함을 보장해 줄 지어니..
2. **testId 는 테스트의 범위를 좁히고 싶을 때만 사용해라.** Testing Library 의 쿼리만 사용하기에는 명백한 한계가 있다. 이름이 같은것이 있을 여지는 매우 많다.

수정된 테스트코드에서 여전히 아쉬운 점이 있다. 나 또한 `textContent` 라는 DOM 요소를 사용했고, 컴포넌트 테스트인데 숫자연산을 한것이 찝찝하기도 하고, 기존에 있는 아이템이 컴포넌트에 있는지의 여부를 하드코딩으로 확인했다. 이 소스를 다시 최대한 방어적인 코드가 될때까지 리팩토링 해보자. 그리고 거기서 깨달은 경험들을 내 것으로 꼭 만들도록 하자.

## 7일차: E2E 테스팅라이브러리 Cypress 소개

### Cypress
테스팅라이브러리로 진행한 컴포넌트 테스트로도 충분히 가상의 DOM 을 테스트할 수 있지만 실제 사용자의 입장에서 테스트를 하기 위해서는 e2e 테스트가 필요하다. 요즘 대세는 cypress. 공식문서의 오버뷰를 보니 정말 테스팅하기 편한 환경, 스스로 공부하기 좋은 문서 모두 고루 갖추었다. 선생님께서는 이것을 봐 가면서 스스로 테스트 코드 짜는 연습을 하라고 하셨다. 내일은 한번 문서만 보고 코딩해보자. 그 속에서 나만의 문서보는 노하우를 하나라도 터득해보자. 또한 새로운 라이브러리에 대한 대비도 확실히 하도록! 이 라이브러리가 영원할거라 생각하지 말고 변화에 유연하게 대처할 수 있는 마음의 준비를 항상 해두고 기술의 흐름을 파악할 줄 아는 자질도 갖추도록 하자.

## 8일차: Cypress 공식문서 Getting Started 공부 - 1 : Writing Your First Test

미쳤다.. Cypress 정말 잘 만들었는데..? 공식문서도 완전 떠먹여주는 꿀이고 [Kitchen Sink](https://github.com/cypress-io/cypress-example-kitchensink) 예제의 README.md 파일에 진짜 개꿀팁 정말 많다.. 정독하면서 인사이트 얻을거 많이 찾아보자.. 프로젝트 관리 이런식으로 해도 될거 같은데? (슬랙에 이어 README.md 꾸미기도 프젝관리에 추가.!!)

### 용어정리

- chaining: command 들의 이야기 집합

### install

```bash
npm i cypress -D
```

### execute

```bash
$(npm bin)/cypress open
```

```bash
npx cypress open
```

```jsx
{
  "scripts": {
    "cypress:open": "cypress open"
  }
}
```

### Add a test file

```bash
touch {your_project}/cypress/integration/sample_spec.js
```

### 3A or GWT of Cypress

1. Visit a web page
2. Query for an element.
3. Interact with that element. ⇒ 페이지 이동시 URL Assertion 해야함.
4. Assert about the content on the page.

### 자신의 서버에서 테스트해야하는 이유

1. 언제든지 사이트가 바뀔수가 있다
2. 해당 사이트가 A/B 테스트 중이라 결과에 일관성이 없을 수도 있다
3. Google 과 같은 사이트는 이런 스크립트를 감지해서 접근 거부한다.
4. Cypress 가 동작하지 못하도록 보안세팅을 해 놓았을 수도 있다.

### Page Transition 하는 법

1. 처음에 `cy.visit()` 을 하여 원하는 페이지 방문
2. 링크를 `.click()` 하여 새로운 페이지 방문

Page Transition은 페이지가 전부 로드될때까지 다음 command를 일시중지한다. 즉, 로드되지 않았는데 다음 커맨드가 실행될 걱정을 전혀 할 필요가 없다는 말이다. element Query 는 4초 타임아웃이고 Page Transition 은 60초 타임아웃이 걸린다. 이는 Configuration 에서 수정 가능하다.

### Debugging

#### Snapshot menu panel 의 역할

- before: 이벤트가 발생하기 바로 직전
- after: 이벤트가 발생하기 바로 이후

만약 링크 클릭 이벤트였다면, 엄청 빠른 사이트였다면 after 클릭 시 빈 화면이 나올수도 있다. 느린 사이트라면 그대로 보일것. 눈으로 바로 확인 가능한 이벤트라면 스냅샷에 잘 찍힘!!

#### Page Events

TEST BODY 를 보면 `(PAGE LOAD)` , `(NEW URL)` 로그가 있는 것을 볼 수 있다. 이것들은 COMMAND 가 아니고, Cypress 에서 저 둘 이벤트가 중요하기 때문에 남겨놓은 **로그일 뿐이다!!**

#### Console output

Commands 클릭하고 브라우저 Console 열면, 해당 Command 에 대한 정보를 보여준다.

- Command: 이슈된 커맨드
- Yielded: 이 커맨드에 의해 반환된 것 ⇒ Element 가 반환됐다면 오른쪽클릭 하여 element 패널에서 검사할 수 있다!!
- Elements: 찾아진 elements 갯수
- Selector: 사용한 argument

#### Special Commands

- `cy.pause()` : Cypress Test Runner 내의 Position Break
- `cy.debug()` : Browser Debug 기능 실행하여 이 코드의 위치를 첫 번째 Position Break로 잡는다.

## 9일차: Cypress 공식문서 Getting Started 공부 - 2 : Testing Your App

### 서버 실행순서

웹서버 → Cypress script: Cypress script 내부에 절대 웹서버 실행 코드를 넣지 말자!!

### Production 보단 local development server에서 테스트 해야하는 경우

Production 에는 여러가지 제약이 있다. development 에서 하면 그러한 제약을 풀고 자유롭게 컨트롤 하며 테스트할 수 있다.

### cy.visit baseUrl 지정해주는 법

프로젝트 루트의 cypress.json 를 설정해준다!

```json
{
	"baseUrl": "http://localhost:3000"
}
```

설정을 저장해주면 browser가 kill 된다. 파일을 다시 열어줘야 테스트 가능하다.

이 외에도 default timeout periods, environment variables, 사용할 reporter, 기타 등등을 설정할 수 있다. 해당 url 에서 configuration을 확인하자! [https://docs.cypress.io/guides/references/configuration](https://docs.cypress.io/guides/references/configuration)

### 테스팅 전략 - seeding

서버 데이터 mutation 없이, 테스팅 전 seed 명령어 실행해서 데이터 일일히 준비해주는 수고 없이 데이터를 Stubbing 하면 테스트를 좀 더 빠르게 수행할 수 있고 심지어는 서버가 없어도 된다.

[Testing Strategies](https://docs.cypress.io/guides/getting-started/testing-your-app#Testing-strategies)는 아직 내가 공부할 필요는 없어보인다. 아직 E2E의 필요성도 크게 없을 뿐더러 E2E를 공부하더라도 내가 테스팅하고자 하는 목적과는 살짝 벗어난것 같다. 나중에 필요하면 [Stubbing](https://docs.cypress.io/guides/getting-started/testing-your-app#Stubbing-the-server) 하는 정도만 찾아서 간편하게 적용해보자. 중요도 낮은 부분에 지금 당장 연연하지 말고, 내일은 어제 배운 8일차 지식을 기반으로 Habit Tracker 앱의 E2E 테스트 코드를 빨리 작성하는걸로 마무리를 짓도록 하자!! 다음 중요한 진도를 빨리 나가야지 :)

## 10일차: Habit Tracker에 Cypress 적용

Cypress 라이브러리 자체는 selector 를 사용해서 요소를 찾아오는 등 내부 구현사항에 너무 치중돼 있어서 이전에서 배웠듯이 올바른 테스팅에 어긋나다. cypress 역시도 [Testing Library](https://testing-library.com/docs/cypress-testing-library/intro/) 가 있다. 이것을 이용해 기존 Testing Library 에서 사용했던 쿼리를 그대로 사용하고, 거기다 event나 assertion 을 체이닝 하여 테스트를 진행하면 된다!!

### 타입정보 적용하는법

테스트코드 맨 위에 아래와 같은 소스를 포함시켜야 내가 원하는 타입정보를 제대로 받아올 수 있다.

```jsx
/// <reference types="cypress" />
```

### Assertion

`.should()` 로 체이닝하여 매개변수에 문자열을 넣는다. 여러가지 문자열 자동완성을 지원하기 때문에 편리하게 찾을 수 있다. 그때그때 필요한거 잘 찾아서 사용해 보도록 하자.

### Testing Library 적용 전 소스

내가 직접 문서를 봐 가면서 작성한 소스인데, 체계가 잘 잡혀있지 않는 느낌이 많이 든다. 무엇보다도 내부 구현사항에 치중된 쿼리가 사용자로 하여금 매우 헷갈리게 만들고, GWT, 3A 가 제대로 구분되어 있지 않아 이에대한 매서드 사용 요령에 관한 체계가 잡혀있지 않는 상태로, 아쉬운 점이 많다.

```jsx
describe('The Home Page', () => {
  beforeEach(() => {
    cy.visit('/')
  })
  describe('add', () => {
    it('appends a habit of Studying', () => {
      cy.get('.add-input')
        .type('Studying')
        .should('have.value', 'Studying')
      cy.get('.add-button').click()
      cy.contains('Studying')
    })
  })

  describe('delete', () => {
    it('removes an habit', () => {
      cy.get(':nth-child(1) > .habit-delete').click()

      cy.get('[data-testid="habit-list"]').should(
        'not.contain',
        'Reading'
      )
    })
  })

  describe('increment', () => {
    it('has 999 when plus button is clicked 10 times', () => {
      const plusButton = cy.get(
        ':nth-child(1) > .habit-increase'
      )

      for (let i = 0; i < 10; i++) {
        plusButton.click()
      }

      cy.get(
        ':nth-child(1) > [data-testid="habit-count"]'
      ).contains('10')
    })

    it('has active habit count 2 when incrementing 2 habits', () => {
      cy.get(':nth-child(1) > .habit-increase').click()
      cy.get(':nth-child(3) > .habit-increase').click()

      cy.get('.navbar-count').contains('2')
    })
  })

  describe('decrement', () => {
    it('decrements active count 2 into 1 when a habit become zero', () => {
      cy.get(':nth-child(1) > .habit-increase').click()
      cy.get(':nth-child(3) > .habit-increase').click()

      cy.get('.navbar-count').contains('2')

      cy.get(':nth-child(3) > .habit-decrease').click()
      cy.get('.navbar-count').contains('1')
    })

    it('cannot decrements a habit below zero', () => {
      cy.get(':nth-child(1) > .habit-increase').click()
      cy.get(
        ':nth-child(1) > [data-testid="habit-count"]'
      ).contains('1')

      cy.get(':nth-child(1) > .habit-decrease')
        .click()
        .click()
      cy.get(
        ':nth-child(1) > [data-testid="habit-count"]'
      ).contains('0')
    })
  })

  describe('Reset All', () => {
    it('changes all of the count to 0', () => {
      cy.get(':nth-child(1) > .habit-increase').click()
      cy.get(':nth-child(2) > .habit-increase').click()
      cy.get(':nth-child(3) > .habit-increase').click()

      cy.get(
        ':nth-child(1) > [data-testid="habit-count"]'
      ).contains('1')
      cy.get(
        ':nth-child(2) > [data-testid="habit-count"]'
      ).contains('1')
      cy.get(
        ':nth-child(3) > [data-testid="habit-count"]'
      ).contains('1')
      cy.get('.navbar-count').contains('3')

      cy.contains('Reset All').click()

      cy.get(
        ':nth-child(1) > [data-testid="habit-count"]'
      ).contains('0')
      cy.get(
        ':nth-child(2) > [data-testid="habit-count"]'
      ).contains('0')
      cy.get(
        ':nth-child(3) > [data-testid="habit-count"]'
      ).contains('0')
      cy.get('.navbar-count').contains('0')
    })
  })
})
```

### Testing Library 적용 후  소스

확실히 내부 구현사항에 치중되지 않는 사용자 입장에서의 쿼리로, 보기 훨씬 깔끔하다. 그리고 Testing Library 라서 나에게 반가운 쿼리들이 많았다. 쿼리를 수행하고 그 후에 event trigger 하고, `should` 를 통해 다양한 assertion 을 수행하는 일관성, 체계성을 확인하고 나서야 이제 좀 안정감이 들었다. 이 외에서 `each` 나 `cy.wrap` 이나, `first` , `last` 등등 흥미로운 것이 많았는데, 정말로 자연스러운 네이밍에서 기능을 유추할 수 있기때문에 금방 암기하고 넘어갈 수 있다는 생각이 든다. cypress 쪽은 정말 수작인것 같다. React Testing Library 에도 저런 편리한 기능이 있으면..

> 또 아쉬웠던 점, 예전 리팩토링에서 연구한 대로 한 listitem 을 뽑아오고 그 속에서 버튼클릭하고 값 확인하는 안정성있는 코드 작성하고 싶었는데, 지금도 여전히 신뢰성이 낮은 쿼리를 수행하고 있다는것. 이 소스도 조만간 손을 대야한다. 하지만 내가 지금 지방에 내려와 있는 관계로 시간관계상 여기까지밖에 할 수 없다는점.. 다시 이 글을 본다면 바로 VSCode 로 달려가서 리팩토링 수행하자.
> 

```jsx
/// <reference types="cypress" />
import '@testing-library/cypress/add-commands'

describe('Habit Tracker', () => {
  beforeEach(() => {
    cy.visit('/')
  })

  it('renders', () => {
    cy.findByText('Habit Tracker').should('exist')
  })

  it('adds new habit at the end', () => {
    cy.findByPlaceholderText('Habit').type('New Habit')
    cy.findByText('Add').click()
    cy.findAllByTestId('habit-name')
      .last()
      .should('have.text', 'New Habit')
    cy.findAllByTestId('habit-count')
      .last()
      .should('have.text', '0')
  })

  it('increases count', () => {
    cy.findAllByTitle('increase').first().click()
    cy.findAllByTestId('habit-count')
      .first()
      .should('have.text', '1')
  })
  it('decreases count', () => {
    cy.findAllByTitle('increase').first().click()
    cy.findAllByTitle('decrease').first().click()
    cy.findAllByTestId('habit-count')
      .first()
      .should('have.text', '0')
  })
  it('does not decreases below 0', () => {
    cy.findAllByTitle('decrease').first().click()
    cy.findAllByTestId('habit-count')
      .first()
      .should('have.text', '0')
  })
  it('shows active count on the header', () => {
    cy.findAllByTitle('increase').first().click()
    cy.findAllByTitle('increase').last().click()
    cy.findByTitle('total count').should('have.text', '2')
  })

  it('reset to 0 when clicking reset all', () => {
    cy.findAllByTitle('increase').first().click()
    cy.findAllByTitle('increase').last().click()
    cy.findByText('Reset All').click()
    cy.findAllByTestId('habit-count').each((item) => {
      cy.wrap(item).should('have.text', '0')
    })
  })
  it('deletes an item', () => {
    cy.findAllByTitle('delete').first().click()
    cy.findAllByTestId('habit-name').should(
      'not.contain.text',
      'Reading'
    )
  })
})
```

## 11일차: 네트워크를 사용하는 사이트 테스트, 비쥬얼 테스팅

### 네트워크를 사용하는 사이트 테스트 방법

시간이 지남에 따라 동적으로 변하는 데이터들은 테스트 하기 어렵다. 그래서 테스트의 일관성을 확보하기 위해, fixture 라는것을 만들어야 하는데, 일정한 포맷의 데이터를 json 으로 미리 만들어주면 된다. 이를 cypress 에서 `cy.intercept` 라는 함수를 사용하여 특정 request 시 해당 fixture 를 반환하도록 코드를 작성하면 된다. 그런데, cypress 공식문서를 보면 fixture 를 사용하지 않고도 좀 더 편리하게 테스트 하는 방법을 소개하고 있다. 그 방법은 무엇일지? 나중에 필요하면 찾아보도록 하자.

### 비주얼 테스팅

- 시각적으로 보이는 화면을 검증하기 위해서 Storybook 이라는 툴을 이용한다. [https://www.youtube.com/watch?v=jc9xKzdkYDg](https://www.youtube.com/watch?v=jc9xKzdkYDg) 에 자세한 소개영상이 있으니 참고할 것.
- Storybook과 연동하여 개발자로의 요구사항을 스크린샷으로 캡쳐하여 비교하게 할 수 있는 플랫폼이 있다(percy, chromatic). 공부하는 단계에서는 storybook 까지만 알아도 충분하나 현업에서 확실한 비쥬얼 테스팅을 하고싶다면 앞서말한 두 플랫폼을 고려해볼만 하다!
