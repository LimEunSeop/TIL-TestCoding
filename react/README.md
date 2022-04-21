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
