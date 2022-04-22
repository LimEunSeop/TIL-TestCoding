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
