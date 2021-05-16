# React 개념정리

# React 컴포넌트가 업데이트 되는 경우
 1. props가 변경될때?
 2. state가 변경될때
 3. 부모 컴포넌트가 re-rendering될때
 4. this.forceUpdate로 강제로 랜더링 할때

# 컴포넌트 Life Cycle
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