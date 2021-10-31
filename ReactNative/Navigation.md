# Navigation

* 모바일 앱은 하나의 화면으로 구성되는 경우가 거의 없음
* 일반적으로 다양한 화면이 상황에 맞게 전환되면서 나타남
* 따라서 내비게이션은 모바일 앱에서 가장 중요한 기능 중 하나



* 리액트 네이티브에서는 내비게이션 기능 지원 않음으로 외부 라이브러리 이용해야 함
* 여기서는 `React Navigation`라이브러리 사용할 것임



## React Navigation

* 리액트 내비게이션 라이브러리는 리액트 네이티브 앱의 내비게이션을 쉽고 간단하게 관리할 수 있도록 도와줌

* 지원하는 내비게이션의 종류는 세 종류

  * 스택 내비게이션 `stack`

  * 탭 내비게이션 `tab`

  * 드로어 내비게이션 `drawer`

    

### Navigation Structure

* 리액트 내비게이션에는 다음과 같이 구성됨
  * NavigationContainer 컴포넌트
  * Navigator 컴포넌트
  * Screen 컴포넌트

* Screen 컴포넌트
  * 화면으로 사용되는 컴포넌트
  * `name` 과 `component` 속성을 지정해야 함
  * `name`은 화면 이름으로 사용
  * `component`에는 화면으로 사용될 컴포넌트 전달
  * 화면으로 사용되는 컴포넌트에는 항상 `navigation`과 `route`가 `props`로 전달된다는 특징
* Navigation 컴포넌트
  * 화면을 관리하는 중간 관리자 역할
  * 내비게이션 구성
  * 여러 개의 Screen 컴포넌트를 자식 컴포넌트로 가지고 있음
* NavigationContainer 컴포넌트
  * 내비게이션의 계층 구조와 상태를 관리하는 컨테이너 역할
  * 모든 내비게이션 구성 요소를 감싼 최상위 컴포넌트여야 함



### 설정 우선 순위

* 리액트 내비게이션에서 설정할 수 있는 다양한 `속성을 수정하는 방법`
  * Navigator 컴포넌트의 속성으로 수정하는 방법
  * Screen 컴포넌트의 속성으로 수정하는 방법
  * 화면으로 사용되는 컴포넌트의 `props`로 전달되는 `navigation`을 이용해서 수정하는 방법
* 화면 사용되는 컴포넌트 설정 + Screen 컴포넌트에서 설정하는 방법 -> 해당 화면만 적용
* Navigator 컴포넌트에서 속성 지정하는 방법 -> 자식 컴포넌트로 존재하는 모든 컴포넌트에 적용
* 작은 범위의 설정일수록 우선순위가 높으므로
  * 만약 `Screen 컴포넌트`와 `화면으로 사용되는 컴포넌트`에 `동일 옵션` 적용되었다면 
  * `화면 컴포넌트` 설정이 우선함



### 폴더 구조와 라이브러리 설치

* src/App.js

  ```react
  import React from "react";
  import styled from "styled-components/native";
  
  const Container = styled.View`
    flex: 1;
    background-color: #ffffff;
    justify-content: center;
    align-items: center;
  `;
  
  const App = () => {
    return <Container></Container>
  };
  
  export default App;
  ```

* App.js

  ```react
  import App from "./src/App";
  
  export default App;
  ```

* ```
  react-native-navigation
  \---src
      |   App.js
      |   
      +---navigations
      \---screens
  \---App.js
  ```

* 폴더 구조를 위와 같이 하여 화면 컴포넌트 관리

* ```bash
  npm install --save @react-navigation/native
  ```

* react-navigation 설치

* 리액트 내비게이션은 각 기능별로 모듈 분리되어 있어

* 이후에도 사용하는 내비게이션의 종류에 따라 개별적으로 추가 라이브러리 설치해야함(???)

* 대부분 내비게이션에서 반드시 필요한 종속성 설치

* ```bash
  expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view
  ```



## Stack Navigation

* 가장 기본적인 내비게이션인 스택 내비게이션에 대해 알아보자

* 우선 다음 명령어 통해 스택 내비게이션 활용에 필요한 라이브러리 설치

* ```bash
  npm install @react-navigation/stack
  ```

* 스택 내비게이션은 가장 많이 사용되는 내비게이션

* 현재 화면 위에 다른 화면 쌓으면서 화면 이동하는 특징

  * 예를 들면
  * 채팅 앱에서 채팅방에 입장하는 상황
  * 여러 목록 중 특정 항목 상세 화면 이동 등

* 스택 내비게이션은 화면 위에 새로운 화면을 쌓으면서`push` 이동하기에

  * 이전 화면 계속 유지

* 이런 구조 때문에 가장 위에 있는 화면 들어내면`pop` 이전 화면으로 돌알갈 수 있다는 특징



### 화면 구성

* screens 폴더 밑에 스택 내비게이션 화면으로 사용할 화면 만들자

* src/screens/Home.js

  ```react
  import React from "react";
  import { Button } from 'react-native';
  import styled from "styled-components/native";
  
  const Container = styled.View`
    align-items: center;
  `;
  const StyledText = styled.Text`
    font-size: 30px;
    margin-bottom: 10px;
  `;
  
  const Home = () => {
    return (
      <Container>
        <StyledText>Home</StyledText>
        <Button title="go to the list screen"/>
      </Container>
    )
  };
  
  export default Home;
  ```

  * 첫 화면으로 사용할 Home 화면 구성함
  * 화면 확인 위한 텍스트와 다음 화면 List 화면으로 이동하기 위한 버튼으로 화면 구성

* src/screens/List.js

  ```react
  import React from "react";
  import { Button } from "react-native";
  import styled from "styled-components/native";
  
  const Container = styled.View`
    flex: 1;
    justify-content: center;
    align-items: center;
  `;
  const StyledText = styled.Text`
    font-size: 30px;
    margin-bottom: 10px;
  `;
  
  const items = [
    { _id: 1, name: 'React Native'},
    { _id: 2, name: 'React Navigation'},
    { _id: 3, name: 'SinsunAi'},
  ];
  
  const List = () => {
    const _onPress = item => {};
  
    return (
      <Container>
        <StyledText>List</StyledText>
        {items.map(item => (
          <Button 
            key={item.id}
            title={item.name}
            onPress={() => _onPress(item)}
          />
        ))}
      </Container>
    )
  }
  
  export default List;
  ```

  * 화면에서 사용할 임시 목록 생성
  * 항목 수 만큼 버튼 생성하도록 작성

* src/screens/Item.js

  ```react
  import React from "react";
  import styled from "styled-components/native";
  
  const Container = styled.View`
    flex: 1;
    justify-content: center;
    align-items: center;
  `;
  const StyledText = styled.Text`
    font-size: 30px;
    margin-bottom: 10px;
  `;
  
  const Item = () => {
    return (
      <Container>
        <StyledText>Item</StyledText>
      </Container>
    )
  };
  
  export default Item;
  ```

  * 목록의 상세 정보 보여주는 컴포넌트

* navigations 폴더 안에 Stack.js 파일 생성하고 생성된 컴포넌트 이용해 스택 내비게이션 구성

* src/navigations/Stack.js

  ```react
  import React from "react";
  import { createStackNavigator } from "@react-navigation/stack";
  // components
  import Home from "../screens/Home";
  import List from "../screens/List";
  import Item from "../screens/Item";
  
  const Stack = createStackNavigator();
  
  const StackNavigator = () => {
    return (
      <Stack.Navigator>
        <Stack.Screen name="Home" commponent={Home} />
        <Stack.Screen name="List" commponent={List} />
        <Stack.Screen name="Item" commponent={Item} />
      </Stack.Navigator>
    )
  }
  
  export default StackNavigator;
  ```

  * createStackNavigator 함수를 이용해 스택 내비게이션 생성
  * 생성된 스택 내비게이션에는
    * 화면을 구성하는 Screen 컴포넌트
    * Screen 컴포넌트를 관리하는 Navigator 컴포넌트가 있음

  * Navigtor 컴포넌트 안에 Screen 컴포넌트를 자식 컴포넌트로 작성하고
  * 앞에서 만든 컴포넌트를 Screen 컴포넌트의 component 로 지정
  * name에는 화면의 이름 작성
    * Screen 컴포넌트의 name은 반드시 서로 다른 값을 가져야 함



* 이제 App 컴포넌트에서 완성된 스택 내비게이션 사용해보자

* src/App.js

  * ```react
    import React from "react";
    import { NavigationContainer } from "@react-navigation/native";
    import StackNavigation from "./navigations/Stack";
    
    const App = () => {
      return (
        <NavigationContainer>
          <StackNavigation />
        </NavigationContainer>
      )
    };
    
    export default App;
    ```

  * `NavigationContainer` 컴포넌트를 이용해 작성된 스백 내비게이션을 감싸도록 App 컴포넌트 수정



---

* 여기서 실행했는데

* ```
  Error: Couldn't find a 'component', 'getComponent' or 'children' prop for the screen 'Home'. This can happen if you passed 'undefined'. You likely forgot to export your component from the file it's defined in, or mixed up default import and named import when importing.
  ```

* 위와 같은 오류 발생

* 보통 모듈 import 시 구조 분해를 사용할 때 많이 난다는데 나는 아무리 봐도 아닌데...

* 한시간의 검색과 삽질 후

* ```react
        <Stack.Screen name="Home" commponent={Home} />
        <Stack.Screen name="List" commponent={List} />
        <Stack.Screen name="Item" commponent={Item} />
  ```

* commponent 라는 단어가 없다는 것을 깨닫는다

* ㅎㅎ...;;

---



* 스택 내비게이션 첫 번째 화면은 Navigator 컴포넌트의 첫 번째 자식 Screen 컴포넌트

  * 배치 순서에 따라 달라진다는 뜻

* 컴포넌트 순서 변경 방법 외에도 `initailRouteName` 속성을 이용할 수 있음

  ```react
      <Stack.Navigator initialRouteName="List">
        <Stack.Screen name="Home" component={Home} />
        <Stack.Screen name="List" component={List} />
        <Stack.Screen name="Item" component={Item} />
      </Stack.Navigator>
  ```

  

### 화면 이동

* 화면을 이동해보자

* **Screen 컴포넌트의 `component`로 지정된 컴포넌트는 화면으로 이용되고 `navigation`이 `props`로 전달**

* Home 화면에서 props로 전달되는 navigation을 사용해 버튼 클릭 시 List 화면으로 이동하게 해보자

* `src/screens/Home.js`

  ```react
  const Home = ({ navigation }) => {
    return (
      <Container>
        <StyledText>Home</StyledText>
        <Button
          title="go to the list screen"
          onPress={() => navigation.navigate('List')}
        />
      </Container>
    )
  };
  ```

  * `navagation`에 있는 `navigate` 함수를 이용해 원하는 화면의 이름을 전달하면 해당 화면으로 이동
  * 단, 전달되는 화면의 이름은 Screen 컴포넌트의 name값 중 하나를 입력해야 함

* 만약 이동하는 화면이 이전 화면의 상세 화면이라면

  * 상세 화면은 `어떤 내용을 렌더링해야 하는지` 전달받아야 함
  * `navigate`함수를 이용할 때 두 번째 파라미터에 객체를 전달해 이동하는 화면에 필요한 정보를 함께 전달하는 기능이 있음

* 이번엔 `navigate` 함수를 이용하여

  * List 화면에서 목록 클릭 시
  * 해당 항목으로 이동하게 해보자

* `src/screens/List.js`

  ```react
  ...
  const List = ({ navigation }) => {
    const _onPress = item => {
      navigation.navigate('item', { id: item._id, name: item.name });
    };
  
  ...
  ```

  * Item 화면으로 이동하며
    * 항목의 id / name 함께 전달하도록 작성
    * 전달된 내용은 컴포넌트의 props 로 전달되는 `route`의 `params`를 통해 확인 가능

* Item 화면에 전달되는 params 이용해

  * 화면에 항목의 id와 name 출력해보자

* `src/screens/Item.js`

  ```react
  const Item = ({ route }) => {
    return (
      <Container>
        <StyledText>Item</StyledText>
        <StyledText>ID: {route.params.id}</StyledText>
        <StyledText>Name: {route.params.name}</StyledText>
      </Container>
    )
  };
  ```

* 이제 각 item 의 내용들이 잘 출력된다.



### 화면 배경색 수정하기

* `src/screens/Home.js`

  ```react
  const Container = styled.View`
    background-color: #ffffff;
    align-items: center;
  `;
  ```

  * 이렇게 하면 콘텐츠가 있는 부분만 흰색으로 바뀜
  * 화면 전체 영역 채우려면 flex: 1 속성을 부여할 수 있지만
  * 상황에 따라 화면 전체 차지 못하는 경우도 있음
  * 이런 상황에서는 리액트 내비게이션 설정 수정하여 해결 가능

* `src/navigations/Stack.js`

  ```react
      <Stack.Navigator
        initialRouteName="Home"
        screenOptions={{ cardStyle: { backgroundColor: '#ffffff' } }}
      >
        <Stack.Screen name="Home" component={Home} />
        <Stack.Screen name="List" component={List} />
        <Stack.Screen name="Item" component={Item} />
      </Stack.Navigator>
  ```

  * cardStyle을 이용하면 스택 내비게이션 화면 배경색 수정 가능

  * 화면 배경색은 일반적으로 동일하게 사용

    * 화면마다 설정하기 보단
    * Navigator 컴포넌트의 screenOption에 설정해서 화면 전체 적용이 편함

  * 만약 특정 화면만 배경색 다르게 하고 싶다?

    * Screen 컴포넌트에서 설정
    * 화면으로 사용되는 컴포넌트에서 설정

    

### 헤더 수정

* 스택 내비게이션의 헤더는
  * 뒤로 가기 버튼 제공
  * 타이틀을 통해 현재 화면 알려줌
* 이번엔 리액트 내비게이션에서 제공하는 다양한 속성 이용해 스택 내비게이션 헤더 변경 방법 아라보자



#### 타이틀 수정

* 헤더 타이틀은 Screen 컴포넌트의 `name` 속성을 기본값으로 사용

* 헤더 타이틀 변경 가장 쉬운 방법: `name`을 원하는 값으로 변경하는 것

* `src/navigations/Stack.js`

  ```react
      <Stack.Navigator
        initialRouteName="Home"
        screenOptions={{ cardStyle: { backgroundColor: '#ffffff' } }}
      >
        <Stack.Screen name="Home" component={Home} />
        <Stack.Screen name="List" component={List} />
        <Stack.Screen name="Detail" component={Item} />
      </Stack.Navigator>
  ```

  * Item 화면을 나타내는 Screen 컴포넌트의 name 속성을 Detail 로 변경
  * name의 값이 변경되었으므로 Item 화면으로 이동할 때 navigate 함수에 전달하는 첫 번째 파라미터 값도 변경되어야 함

* `src/screens/List.js`

  ```react
  ...
  const List = ({ navigation }) => {
    const _onPress = item => {
      navigation.navigate('Detail', { id: item._id, name: item.name });
    };
  
  ...
  ```

  * name 속성을 변경하는 것은 간편
  * but, name 속성을 이용하는 곳 찾아다니며 모두 수정해야 하는 단점

* name 속성 변경 시의 단점을 피하며 화면 타이틀 변경하려면

  * headerTitle 속성 이용

* `src/navigations/Stack.js`

  ```react
      <Stack.Navigator
        initialRouteName="Home"
        screenOptions={{ cardStyle: { backgroundColor: '#ffffff' } }}
      >
        <Stack.Screen name="Home" component={Home} />
        <Stack.Screen
          name="List"
          component={List}
          options={{ headerTitle: 'List Screen'}}
        />
        <Stack.Screen name="Detail" component={Item} />
      </Stack.Navigator>
  ```

  * List 화면의 타이틀 List Screen으로 변경

