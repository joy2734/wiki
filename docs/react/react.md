# React 개념정리

## setState
 - state 변경시 push 보단 ...state 스프레드 연산자나 concat을 사용하는것이 좋다.

## Prototypes

 - prop 속성에 대한 기본자료형과 대응되는 type을 제공할수있다.
 - `isRequired` 를사용하면 필수로 전달
 - `defaultProps`를 통하여 디폴트값지정가능
```javascript
import ProtoTypes from 'prop-types';

 SomeComponent.propTypes = {
   someString: PropTypes.string.isRequired,
   someNumber: PropTypes.number.isRequired,
   someBool: PropTypes.bool,
   someArray: PropTypes.array,
   someArrayA: PropTypes.arrayOf(PropTypes.number),//배열안 요소지정

   someObject: PropTypes.object,
   someObjectA : PropTypes.objectOf(PropTypes.number),//배열안요소지정
   complexObject: PropTypes.shape({//객체에 대한속성 디테일하기 지정
     name: PropTypes.string,
     age: PropTypes.number
   })
   someFunc: PropTypes.func,
   someSymbol: PropTypes.symbol

 }

 SomeComponent.defaultProps = {
   someString : 'test'
 }
```
 - 지정된값만 사용하도록 지정할수도있음

 ```javascript
 import ProtoTypes from 'prop-types';

 SomeComponent.propTypes = {
   //특정값만 넣을수있음
   dayOfWeek: PropTypes.oneOf(['월','화','수','목','금','토']),
   
   //특정타입만 넣을수있음
   union: Proptypes.oneOfType([
     PropTypes.string,
     PropTypes.number,
     PropTypes.instanceOf(Hello)
   ]),

  //아무것이나가능
   any: PropTypes.any
 }

 ```


## React 컴포넌트가 업데이트 되는 경우
 1. props가 변경될때?
 2. state가 변경될때
 3. 부모 컴포넌트가 re-rendering될때
 4. this.forceUpdate로 강제로 랜더링 할때

## 컴포넌트 Life Cycle
- 마운팅 이벤트
  1. componentWillMount - React 엘리먼트가 실제 DOM에 곧 추가 될 것을 알려준다.
  2. componentDidMount - 엘리먼트가 실제 DOM에 추가한 시점

- 갱신 이벤트
  1. componentWillReceiveProps(newProps)
  2. shouldComponentUpdate()
  3. componentWillUpdate()
  4. componentDidUpdate()

## Redux + Reducer + Action


## React HOOK


## React useEffect

- `useEffect` Hook은 Class 컴포넌트 에서 componentDidMount, componentDidUpdate, componentWillMount가 합쳐진 것이라고 생각.
  - 정리를 이용하지 않는 useEffect
    - 컴포넌트 업데이트시 막생성된(componentDidMount) 것인지 생성 후 변경(componentDidUpdate)이 일어난건지 알 수 없기 때문에 중복코드가 발생한다.
    - React Hook의 useEffect 사용시 useEffect 안쪽의 함수를 기억하였다가 컴포넌트가 다시 DOM에 랜더링된 후에 실행된다.
    - 기본적으로 useEffect 안에 function은 첫번째 랜더링과 이후 모든 업데이트에서 발생한다.(단, 상황에 따라서 변경가능)
    - 만약 동기적 실행이 필요한 경우에는 `useLayoutEffect` 사용하여 처리
    ```javascript
    import React, { useState, useEffect } from 'react';

    function Example() {
        const [count, setCount] = useState(0);

        useEffect(() => {
            document.title = `You clicked ${count} times`;
        });

        return (
            <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>
                Click me
            </button>
            </div>
        );
    }
    ```

  - 정리를 이용하는 useEffect
    - componentDidMount/componentWillUnMount 좀더작성필요....


- https://reactjs.org/docs/hooks-reference.html
- 
## BasicHook

  - useState : 상태유지값과 그값을 갱신하는 함수를 반환함.
    - useState함수 파라미터:초기값
    - count: 상태값
    - setCount: 상태값을 갱신하는함수
  - state hook을 현재의 state와 동일한 값으로 갱신하는경우에 react는 랜더링을 회피하고 그 처리를 종료함.
  ```javascript
  const [count, setCount] = useState(0);

  //갱신함수사용시 prevState를 인자로받을수있다.
  setCount(prevState =>{
    return {...prevState, ...updatedValues};
  });

  //초기 state를 함수로도정의가능
  const [state, setState] = useState(() => {
    const initialState = someExpensiveComputation(props);
    return initialState;
  });

  ```
  - useEffect
    - 화면이 랜더링이 완료 된 후에 실행되는 함수.
    - 기본적으로 모든 랜더링이 완료된 후에 수행되지만, 어떤값이 변경될때만 해당함수가 실행되게 할 수도있다.
    - 실행타이밍
      - 레이아웃 배치/그리기를 완료한 후 발생
    - 사용자에게 노출되는 DOM 변경은 다그리기 이전에 동기화 해야하므로 `useLayoutEffect` 사용하여 처리할 수 있다.
    - effect는 의존성중 하나라도 변경된다면 항상 재생성되기때문에 과도한 작업이 이루어질수있다. 이를 위해서 두번째인자로 배열에 특정 값이 변경될때만 efftect 함수가 실행될 수 있도록 할 수있다.
      - 해당effect 한번만 수행하길원한다면 [] 을 두번째 인자로 전달
  
  ```javascript
    useEffect(
      () => {
        const subscription = props.source.subscribe();
        return () => {
          subscription.unsubscribe();
        };
      },
      [props.source],
    );
  ```
  
  - useContext  
    - React.createContext Api를 좀더쉽게사용.///나중에정리
  
## Additional Hooks

  - useReducer
    - 첫번째 인자 리듀서함수, 두번째인자 초기 상태값
    - or 첫번째 리듀서, 두번째 함수인자 초기값, 세번쨰 함수
      - ex)  const [state, dispatch] = useReducer(reducer, initialCount, init);
    - 반환 인자 state, dispatch
```javascript
const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```

  - useCallback
    - 불필요한 re-rednering을 방지
    - useCallback(fn, deps)는 useMemo(()=> fn, deps) 와동일
    - useCallback안에서 사용되는 props나 state속성을 두번째 배열인자에 넣어줘야함 
    - 특정 상태의 변경의 경우에만 해당 함수가 재생성됨.
    - `함수`를 반환
```javascript
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```
  - useMemo
    - 모든 랜더링시 고비용 계산방지
    - `값`을반환
```javascript
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

  - useRef
    - useRef는 .current 프로퍼티로 전달된 인자(initialValue)로 초기화된 변경 가능한 ref 객체를 반환
    - 순수 자바스크립트 객체를 생성해준다.
```javascript
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    // `current` points to the mounted text input element
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

  - useImperativeHandle

  - useLayoutEffect
  
  - useDebugValue