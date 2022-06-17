### TODO LIST_v3
### 1️⃣ 개요
- 사용 기술 스택
  - React
  - Redux, Redux MiddleWare
  - Json-server
---------------------------------
### 2️⃣ Todo List v2에서 구현해 놓은 것
  1. Redux를 이용한 상태관리
     1. [TODO_LIST_v2/src/modules/todoState.jsx](https://github.com/augusstt06/TODO_LIST_v2/blob/master/src/modules/todoState.jsx)
        1. TodoList에 대한 전체 데이터의 상태를 Store에 저장하여 관리
     2. [TODO_LIST_v1/src/modules/modalState.jsx](https://github.com/augusstt06/TODO_LIST_v2/blob/master/src/modules/modalState.jsx)
        1. Modal을 열고 닫는것에 대한 상태관리
---------------------------------
        
### 3️⃣ Todo List v2를 바탕으로 수정 및 보완할 점
1. __Modal 용도 재 정립__
   1. TodoList v2에서 Modal을 각각의 리스트 항목마다 적용한 결과 오히려 더 구조가 복잡해졌다.
   2. TodoList의 특성상 간단히 사용이 가능해야 하기 때문에, 항목의 확인/수정은 Main 컴포넌트에서 해결하고 삭제시 Modal을 이용하여 확인하는 용도로 바꾼다.
2. __API요청시 비동기 처리__
   1. API 요청 후, 데이터를 받아오기 전까지 다른 작업이 가능하도록 고친다
   2. Suspense, Redux MiddleWare를 이용한다.
      - Redux MiddleWare
         >__Redux-Saga__
         > * 사용이유
         >    1. 비동기 작업시 작업 취소 가능
         >    2. API 요청 실패시 재요청 작업 가능
         >* 작동원리
         >    1. Redux가 Action을 수행하면 Redux-Saga에서 Dispatch하여 Redux의 Action을 가로챈다
         >    2. Redux_Saga에서 Action의 역할을 수행 하고 다시 Action을 발행하여 데이터를 저장하거나 다른 이벤트를 실행시킨다. 
      - Suspense
        - 컴포넌트의 렌더링을 어떤 작업이 끝날 때까지 잠시 중단시키고 다른 컴포넌트를 먼저 렌더링 한다.
          - 사용 전
            1. 1번 컴포넌트 마운트
            2. 1번 컴포넌트 안의 useEffect를 사용하여 API 통신/데이터 수신
            3. 수신된 데이터를 바탕으로 화면 구성
            * __1번 컴포넌트의 데이터 수신이 늦어질수록 사용자가 보는 화면의 구성이 늦어진다.__ 
          - 사용 후
            1. 1번 컴포넌트 마운트
            2. 컴포넌트가 마운트 되는 동안 사용자가 볼 다른 컴포넌트 호출
            3. 1번 컴포넌트 안의 useEffect를 사용하여 API 통신/데이터 수신
            4. 1번 컴포넌트의 데이터 수신이 완료되면 1번 컴포넌트 호출
            5. 화면 구성
            * __1번 컴포넌트가 데이터를 수신하는 동안 다른 컴포넌트를 호출하여 사용자 입장에서 화면의 구성이 끊기지 않고 이어진다.__
3. CSS 라이브러리 사용 (Material-UI)
   1. CSS 라이브러리를 사용하여 직접 CSS를 작성하는것보다 직관적이고 보기 좋은 화면을 구성한다.