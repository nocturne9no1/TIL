# [React] useState 에 관하여

## 서론

`useState`는 React 를 사용하면서 가장 많이 사용하는 Hook이 아닐까 싶다. 이번에는 `useState`를 중심으로 지금까지 그저 사용'만' 해왔던 React 이모저모를 살펴보자

## 기본 사용법

* `useState`의 기본적인 사용법은 아래와 같다

```React
import React, { useState } from 'react'

const Example = (props) => {
    const [state, setState] = useState('');
}
```

* 우선 useState를 import 해온 뒤
* []로 묶어 하나는 state의 이름 다른 하나는 set + 'state이름'으로 선언하고 
* 이를 `= useState(초기값)`의 형태로 선언한다



### 원래 쓰던 형태

* 지난번 Hook의 기원에 대해 살펴 봤을 때 class 컴포넌트 대신에 fucntion 컴포넌트를 위해 Hook을 쓴다고 알아보았다.
* 그렇다면 이전에는 어떻게 썼을까??

```React
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

* 리액트 공식문서에서는 버튼을 눌러 count 를 늘리는 컴포넌트를 위와 같이 작성한다고 소개한다.

