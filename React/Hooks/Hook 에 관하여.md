# Hook 에 관하여

## 서론

지금 까지 `useState`, `useEffect` 등의 Hook 들을 그 의미나 등장 배경에 대해 제대로 이해하지 못하고 사용해 왔다. 분명히 어떤 불폄함이 있었기 때문에 Hook이 등장했을 것이다. 어렴풋이 `Vue`에서 사용하던 생명 주기에 관련된 메소드들을 `React`에서는 useEffect 등을 통해 관리한다 정도로만 알고 있었다. 따라서 Hook이 왜 등장했는 지를 시작점으로 각 Hook들이 어떻게 동작하는지 세세하게 파악하고, 나아가 custom Hook은 어떻게 만드는지도 생각해보자!

## Hook의 등장배경

### Class vs Function

단순히 class 문법을 사용하는 React Component는 더 이상 사용을 권고하지 않는다는 이유로 Function Component를 사용해왔다. 왜 class보다 fucntion 일까??

#### Class

* Fucntion Component 보다 더 많은 기능을 지원한다.
* state를 이용한 상태관리, component lifecyle에 정의된 메소드를 이용해 원하는 순서에 특정 동작을 가능하게 한다.
* 기본적으로 Class 형 component의 기본 형식은 다음과 같다.

```react
class ClassComp extends React.Component {
    state = {
        
    };
    render() {
        return (
            <div className="container">
                
            </div>
        )
    }
}
```

* 여기에 `componentWillMount()`, `componentDidMount()` 와 같은 `lifecyle method`를 사용할 수도 있다.

* 복잡한 작업에서는 이러한 과정을 하나하나 컨트롤 하는게 어려웠지만 React 16.8에 Hook이 추가되며 상황은 바뀐다.

#### Function

* 16.8버전 이전에는 state 관리나 lifecyle에 정의된 함수를 사용할 수 없어 비교적 간단한 동작에만 사용되었다.
* Function Component의 기본 형식은 다음과 같다.

```react
function FuncComp(props) {
    return (
        <div className="container">
        
        </div>
    )
}
```

* 위 class component 와 비교해 봤을 때 우선 보이는 차이점은 `state={};` 가 없다는 점이다.
* 여기서 Function Component는 `useState`를 사용하는 것이다.

### Component 간 상태 로직의 재사용

* React는 컴포넌트간 재사용 가능한 로직을 붙이는 방법을 제공하지 않음
* 이전에는 render props나 고차 컴포넌트와 같은 패턴을 통해 이러한 문제를 해결함
* 그러나 이런 패턴 사용은 컴포넌트 재구성을 강요하고 코드 추적을 어렵게 함
* 따라서 React는 상태 관련 로직을 공유하기 위해 좀 더 좋은 기초 요소가 필요했던 것
* Hook을 통해 상태 관련 로직을 추상화 가능 - 추상화가 뭔지 구체적으로 공부해야 할 듯
* Hook은 계층 변화 없이 상태 관련 로직을 재상요할 수 있도록 도와준다!
* 커스텀 훅에서 이 위력이 강하게 발휘 될 듯 하다

### 복잡한 컴포넌트에 대한 이해의 어려움

* 개발에 있어서 처음에는 간단하게 시작했더라도 점점 덩치가 커짐
* 이 과정에서 관리가 힘들어지는 상태 관련 로직들과 Side Effect가 있는 컴포넌트들을 유지보수 해야함
  * `componentDidMount`, `componentDidUpdate`는 컴포넌트 안에서 데이터를 가져오는 작업을 수행할 때 사용되어야 함
  * 그러나 같은 `componentDidMount`에서 EventLitener를 설정하는 것과 같은 관계없는 로직이 포함되기도 함
  * `componentWillUnmount`에서 cleanup 로직을 수행하기도 함
  * 사실 이 예시는 직접 사용해 보지 않아 크게 와닿지 않는다...
* 함께 변경되는 상호 관련 코드는 분리되지만
* 이와 연관 없는 코드들은 단일 메소드로 결합
* 이로 인해 버그가 쉽게 발생 + 무결성 쉽게 훼손
* 위와 같은 예시에서, 상태 관련 로직은 한 공간안에 묶여있음
* 따라서 이런 컴포넌트를 작게 분리하는 것은 불가능 + 테스트 어려움
* 때문에 많은 사용자들이 별도의 상태 관리 라이브러리를 사용함
  * 근데 이런 라이브러리는 너무 많은 추상화 + 서로 다른 파일 사이에 건너뛰기 요구
  * => 재사용 더욱 어렵게 만듬
* 이 같은 문제 해결을 위해 생명 주기 메소드를 기반으로 쪼개는 것보다
  * Hook을 통해 서로 비슷한 일을 하는 작은 함수의 묶음으로 컴포넌트를 나누는 방식 사용 가능!
  * 또 이런 로직의 추적을 쉽게 할 수 있도록 Reducer를 활용해 컴포넌트의 지역 상태 값 관리 가능!
  * `Effect Hook`에서 자세히 알 수 있다
    * 링크 https://ko.reactjs.org/docs/hooks-effect.html#tip-use-multiple-effects-to-separate-concerns

### Class는 어려웡

* 위에서 이미 비교했듯 Class Component는 Fucntion에 비해 처리해야할 문제가 많음
* 하지만 이전에는 state, life cyle method의 부제로 Function Component를 활용하기 어려웠음
* 또 React에서 Class 사용을 위해서 JavaScript의 `this` 키워드의 작동원리에 대해 정확히 알아야 함
  * JS 의 `this`는 다른 언어와 다르게 작동해 사용자에게 큰 혼란을 주고 코드 재사용성 및 구성을 어렵게 만들곤 했음
  * class 사용을 위해 이벤트 핸들러가 등록되는 방법을 정확히 파악해야 했음
  * 사용자들은 props, state, top-down 데이터 흐름을 완벽하게 알아도 class 이해에 어려움을 겪곤 함
  * React에서 함수 class 컴포넌트의 구별, 각 요소 사용 타이밍은 숙련된 React 개발자 사이에서도 의견이 일치하지 않음



## 결론

* Hook의 등장배경에서 가장 중요한 점은 `더욱더 쉽게 코드를 짜자`는 정신이다.
* 이 정신 속에서 복잡한 Class 형 컴포넌트 말고 함수형 컴포넌트를 사용하고자 했다.
* 하지만 당시에는 함수형 컴포넌트를 통해 `state관리`나 `life cycle 관련 메소드`를 사용하지 못했다.
* 이 문제를 해결하기 위해 등장한 것이 바로 `HOOK`!





## 참고자료

* Class vs Function - https://jbhs7014.tistory.com/39
* React 공식문서
  * https://ko.reactjs.org/docs/hooks-state.html#equivalent-class-example
  * https://ko.reactjs.org/docs/hooks-intro.html