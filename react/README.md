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
      const countWrapper = screen.getByTestId('total-count')
      const count = within(countWrapper).queryByText('2')
      expect(count).toBeInTheDocument()
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
