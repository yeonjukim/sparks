# Vuex
[document](https://vuex.vuejs.org)

## Vuex란?
- Vue.js application에 대한 상태 관리 패턴 + 라이브러리
- 모든 컴포넌트에 대한 중앙 집중식 저장소 역할
- 예측 가능한 방식으로 상태를 변경할 수 있다.

## 필요한 이유
- Vue app
```
  new Vue({
    // state
    data () {
      return {
        count: 0
      }
    },
    // view
    template: `
      <div>{{ count }}</div>
    `,
    // actions
    methods: {
      increment () {
        this.count++
      }
    }
  })
```
- Vue는 각 컴포넌트가 자신만의 state(data 옵션)를 가질 수 있다.
- `one-way data flow` (State -> View -> Actions -> State) 단방향 데이터 흐름의 한계
- 공통의 상태를 공유하는 여러 컴포넌트가 존재할 때,
  - 여러 view는 같은 state에 의존하고 서로 다른 view의 action은 동일한 state의 변경이 필요할 수 있다.
  - 각 컴포넌트들이 관리하고 있는 state를 props로 전달하는 것의 한계.
  - state를 변경하기 위해 event를 emit하는 것의 복잡함.

## 개념
- 모든 Vuex 애플리케이션 중심에는 기본적으로 애플리케이션 state를 보유하고 있는 컨테이너인 store가 존재한다.
  - 전역객체와 차이점:
    1. vuex store는 반응형이다. store의 state가 변경되면 효율적으로 대응하고 업데이트한다.
    2. store의 state를 직접적으로 변경할 수 없고, 오직 명시적인 committing mutations(커밋을 이용한 변이)로 store의 state를 변경할 수 있다.
- 모든 state 정보를 최상위 부모 컴포넌트에 저장하고 자식 컴포넌트로 props를 이용해 전달하여 화면에 나타낸다.
- state 정보를 변경할 때는 이벤트버스 객체를 이용해 event를 발생시켜 최상위 부모 컴포넌트로 변경하고자 하는 정보를 전달한다.

## 시작하기
```
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment (state) {
      state.count++
    }
  }
})
```
- state 객체에 `store.state`로 접근해 `store.commit` 메소드로 상태 변경을 트리거 할 수 있다.
  ```
    store.commit('increment')

    console.log(store.state.count) // -> 1
  ```
- 뷰 컴포넌트들에서 `this.$store`속성으로 접근하기 위해 뷰 인스턴스에 생성된 store를 제공해야 한다.
  ```
  new Vue({
    el: '#app',
    store: store, //ES6에서는 store: store 대신 store만 써도 됨
  })
  ```
- Vuex는 root 컴포넌트의 모든 자식 컴포넌트에 `store` 옵션을 사용해 store를 'inject'하는 메커니즘을 가지고 있다.
- 컴포넌트의 메소드에서 mutation을 commit할 수 있다.
  ```
  methods: {
    increment() {
      this.$store.commit('increment')
      console.log(this.$store.state.count)
    }
  }
  ```
