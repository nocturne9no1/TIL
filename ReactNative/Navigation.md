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
  
  * List 화면 타이틀 List Screen으로 변경
  * 개별 화면 설정 수정하고 싶을 때 Screen 컴포넌트의 options이용



#### 스타일 수정하기

* 헤더 스타일 수정 속성은

  * 헤더 배경색 등을 수정하는 `headerStyle`
  * 헤더 타이틀 컴포넌트의 스타일 수정하는 `headerTitleStyle`이 있음

* `src/navigations/Stack.js`

  ```react
  ...
  const StackNavigation = () => {
    return (
      <Stack.Navigator
        initialRouteName="Home"
        screenOptions={{ 
          cardStyle: { backgroundColor: '#ffffff' },
          headerStyle: {
            height: 110,
            backgroundColor: '#95a5a6',
            borderBottomWidth: 5,
            borderBottomColor: '#34495e',
          },
          headerTitleStyle: { color: '#ffffff', fontSize: 24 },
        }}
      >
  ...
  ```

  * headerStyle 이용해 헤더 스타일 변경
  * headerTitleStyle 이용해 타이틀 스타일 변경

* 안드로이드에서는 iOS와 달리 타이틀이 중앙 정렬되지 않음

* 타이틀 정렬 양 플랫폼 동일하게 하려면

  * headerTitleAlign 속성 이용
  * left, center 두 값 중 한가지만 설정 가능
  * iOS는 center
  * 안드는 left가 기본값으로 설정

* `src/navigation/Stack.js`

  ```react
      <Stack.Navigator
        initialRouteName="Home"
        screenOptions={{ 
          cardStyle: { backgroundColor: '#ffffff' },
          headerStyle: {
            height: 110,
            backgroundColor: '#95a5a6',
            borderBottomWidth: 5,
            borderBottomColor: '#34495e',
          },
          headerTitleStyle: { color: '#ffffff', fontSize: 24 },
          headerTitleAlign: 'center',
        }}
      >
  ```

  * `headerTitleAlign: center` 로 설정



#### 타이틀 컴포넌트 변경

* 만약 타이틀에 문자열 아닌 다른 것 렌더링 하고 싶다면?

* 헤더 타이틀 변경 위해 문자열 지정했던 `headerTitle` 속성에 컴포넌트 반환하는 함수 지정하면 

  * 타이틀 컴포넌트 반환하는 컴포넌트로 변경 가능

* `src/navigations/Stack.js`

  ```react
  ...
  import { MaterialCommunityIcons } from '@expo/vector-icons';
  ...
      <Stack.Navigator
        initialRouteName="Home"
        screenOptions={{ 
          cardStyle: { backgroundColor: '#ffffff' },
          headerStyle: {
            height: 110,
            backgroundColor: '#95a5a6',
            borderBottomWidth: 5,
            borderBottomColor: '#34495e',
          },
          headerTitleStyle: { color: '#ffffff', fontSize: 24 },
          headerTitleAlign: 'center',
          headerTitle: ({ style }) => (
            <MaterialCommunityIcons name="react" style={style} />
          ),
        }}
      >
  ```

  * 함수 파리미터로 전달되는 style 이용해
    * headerTitleStyle에 지정한 스타일과 동일한 스타일 적용되도록 작성
  * 반환되는 컴포넌트는 vector-icons에서 제공하는 컴포넌트 이용해 리액트 로고 렌더링되도록 작성



#### 버튼 수정하기

* 스택 내비게이션에서 화면 이동하면 헤더 왼쪽에 이전 화면으로 이동하는 뒤로 가기 버튼 나타남

* 첫 화면처럼 이전 화면 없는 경우에는 버튼 안생김

* 뒤로 가기 버튼 이용 방법 외에

  * 왼쪽 → 오른쪽 스와이프 제스쳐 이용하는 방법 있음

* 헤더 왼쪽에 뒤로 가기 버튼 생성되는 것 동일

  * but, iOS와 안드 모습에 차이 있음
  * 안드는 버튼 타이틀 안보여줌
  * iOS는 이전 화면 타이틀을 버튼 타이틀로 보여주기
  * 가 가장 큰 차이

* `headerBackTitleVisible` 이용하면 두 플랫폼 버튼 타이틀 렌더링 여부 동일하게 설정 가능

* `src/navigations/Stack.js`

  ```react
        <Stack.Screen name="Home" component={Home} />
        <Stack.Screen
          name="List"
          component={List}
          options={{ headerTitle: 'List Screen'}}
          options={{
            headerTitle: 'List Screen',
            headerBackTitleVisible: true,
          }}
        />
        <Stack.Screen name="Detail" component={Item} />
  ```

  * 이제 안드에서도 버튼 타이틀 나타남

* 버튼 타이틀 나타나지만

* 이전 화면의 이름이 아닌 다른 값 이용하고 싶다?

  * headerBackTitle 이용

* `src/navigations/Stack.js`

  ```react
        <Stack.Screen
          name="List"
          component={List}
          options={{ headerTitle: 'List Screen'}}
          options={{
            headerTitle: 'List Screen',
            headerBackTitleVisible: true,
            headerBackTitle: 'Prev',
          }}
        />
  ```

  * `headerBackTitle`에 빈 문자열 입력하면 버튼 타이틀에 Back이라는 문자열 나타남
  * 버튼 타이틀에 빈 값 주고 싶다면 `headerBackTitle` 아닌 `headerBackTitleVisible`이용하여 타이틀 보이지 않도록 해야함에 주의



#### 버튼 스타일 수정하기

* 버튼 타이틀도 헤더 타이틀과 같이 원하는 스타일 지정 가능

* `headerBackTileStyle` 이용하면 글자 색 뿐 아니라 글자 크기 등 다양한 스타일 지정 가능

  * but, 버튼의 타이틀에만 적용

* 버튼 타이틀과 이미지 색 동일하게 변경하려면 `headerTintColor` 이용

* `headerTintColor`에 지정된 색은 버튼 뿐 아니라 헤더 타이틀에도 적용

  * but, `headerTitleStyle` 혹은 `headerBackTitleStyle` 이 우선순위 높으므로
  * `headerTintColor` 에 설정한 색으로 나타나게 하고 시다면 다른 스타일과 겹치지 않도록 작성하는 것이 중요

* `src/navigations/Stack.js`

  ```react
        <Stack.Screen
          name="List"
          component={List}
          options={{ headerTitle: 'List Screen'}}
          options={{
            headerTitle: 'List Screen',
            headerBackTitleVisible: true,
            headerBackTitle: 'Prev',
            headerTitleStyle: { fontSize: 24 },
            headerTintColor: '#e74c3c',
          }}
        />
  ```

  * `headerTintColor` 값 설정하고 `headerTitleStyle` 재정의하여 헤더 타이틀에도 함께 적용하도록 수정



#### 버튼 컴포넌트 변경

* 두 플랫폼 뒤로 가기 버튼 아이콘에 동일한 아이콘 렌더링 하려면?
  * `headerBackImage` 에 컴포넌트 반환하는 함수를 전달해서 두 플랫폼이 동일한 이미지 렌더링할도록 변경 가능

* `src/navigations/Stack.js`

  ```react
  ...
  import { Platform } from 'react-native';
  ...
        <Stack.Screen
          name="List"
          component={List}
          options={{ headerTitle: 'List Screen'}}
          options={{
            headerTitle: 'List Screen',
            headerBackTitleVisible: true,
            headerBackTitle: 'Prev',
            headerTitleStyle: { fontSize: 24 },
            headerTintColor: '#e74c3c',
            headerBackImage: ({ tintColor }) => {
              const style = {
                marginRight: 5,
                marginLeft: Platform.OS === 'ios' ? 11 : 0,
              };
              return (
                <MaterialCommunityIcons 
                  name="keyboard-backspace"
                  size={30}
                  color={tintColor}
                  style={style}
                />
              );
            },
          }}
  ```

  * `headrBackImage`의 함수 파라미터에 전달되는 `tintColor`값 이용해 아이콘 색 지정
  * 두 플랫폼 버튼 위치 동일하게 만들기 위해 플랫폼에 따라 스타일 다르게 적용

* 뒤로 가기 버튼 이미지가 아니라 헤더의 왼쪽 버튼 전체를 변경하고 싶다?

  * `headerLeft`에 컴포넌트를 반환하는 함수 지정
  * 동일한 방법으로 `headerRight`에 컴포넌트를 반환하는 함수 지정하면 헤더의 오른쪽에 원하는 컴포넌트 렌더링 가능

* `src/screens/Item.js`

  ```react
  import React, { useLayoutEffect } from "react";
  import styled from "styled-components/native";
  import { MaterialCommunityIcons } from '@expo/vector-icons';
  
  const Container = styled.View`
    flex: 1;
    justify-content: center;
    align-items: center;
  `;
  const StyledText = styled.Text`
    font-size: 30px;
    margin-bottom: 10px;
  `;
  
  const Item = ({ navigation, route }) => {
    useLayoutEffect(() => {
      navigation.setOptions({
        headerBackTitleVisible: false,
        headerTintColor: '#ffffff',
        headerLeft: ({ onPress, tintColor }) => {
          return (
            <MaterialCommunityIcons 
              name="keyboard-backspace"
              size={30}
              style={{ marginLeft: 11 }}
              color={tintColor}
              onPress={onPress}
            />
          )
        },
        headerRight: ({ tintColor }) => (
          <MaterialCommunityIcons 
            name="home-variant"
            size={30}
            style={{ marginRight: 11 }}
            color={tintColor}
            onPress={() => navigation.popToTop()}
          />
        )
      })
    }, [])
    return (
      <Container>
        <StyledText>Item</StyledText>
        <StyledText>ID: {route.params.id}</StyledText>
        <StyledText>Name: {route.params.name}</StyledText>
      </Container>
    )
  };
  
  export default Item;
  ```

  * `useLayoutEffect` Hook은 `useEffect` Hook과 사용법이 동일
  * 거의 같은 방식으로 동작
  * 주요 차이점
    * 컴포넌트가 업데이트된 직후 화면이 렌더링되기 전 실행된다는 점
    * 이 특징 때문에 화면 렌더링하기 전에 변경 부분 있거나 수치 등 측정해야 하는 상황에서 많이 사용
  * `headerLeft`함수의 파라미터에는 다양한 값들 전달
    * 그 중 onPress는 뒤로 가기 버튼 기능 전달
    * 화면 왼쪽 버튼 변경하면서 전혀 다른 기능 설정하는 경우에는 필요 없지만
    * 뒤로 가기 버튼 기능 그대로 기용하고 싶은 경우 유용하게 사용 가능
  * `headerRight` 함수의 파라미터에는 tintColor만 전달
    * onPress에 원하는 행동을 정의해야 함
  * navigation에서 제공하는 다양한 함수 중 `popToTop` 함수는 현재 쌓여 있는 모든 화면을 내보내고 첫 화면으로 돌아가는 기능



#### 헤더 감추기

* 화면 종류나 프로젝트 기획에 따라 헤더 감춰야 하는 상황 있음

* 이런 상황에 이용할 수 있는 설정

  * `headerMode`
  * `headerShown`

* `headerMode`

  * Navigator 컴포넌트의 속성
  * 헤더 렌더링 방법 설정 하는 속성
  * `float`
    * 헤더 상단 유지
    * 하나의 헤더 사용
  * `screen`
    * 각 화면마다 헤더
    * 화면 변경과 함께 나타나거나 사라짐
  * `none`
    * 헤더 렌더링 x 
  * float 은 iOS에서 볼 수 있는 동작 방식
  * screen 은 안드로이드에서 일반적으로 볼 수 있는 방식

* `headerShown`

  * 화면 옵션
  * Navigator 컴포넌트의 screenOptions에 설정하면 전체 화면의 헤더가 보이지 않도록 설정 가능

* 첫 화면인 Home 화면에서만 헤더 보이지 않게 수정 해보자

* `src/navigations/Stack.js`

  ```react
        <Stack.Screen
          name="Home"
          component={Home}
          options={{ headerShown: false }}
        />
  ```

  * 헤더가 사라지면서 노치 디자인에 화면 일부 가림

* `src/screens/Home.js`

  ```react
  const Container = styled.SafeAreaView`
    background-color: #ffffff;
    align-items: center;
  `;
  ```

  * 이제 다시 나온당

  

## Tab Navigation

* Tab Navigation은 보통 화면 위나 아래 위치

* 탭 버튼 누르면 버튼과 연결된 화면으로 이동하는 방식으로 동작

* 탭 내비게이션 사용 위한 추가 라이브러리 설치

  ```bash
  npm install @react-navigation/bottom-tabs
  ```



### 화면 구성

* 3개 버튼과 해당 버튼 연결된 화면으로 구성된 탭 내비게이션 만들거임

* src 폴더 밑에 있는 screens 폴더 내에 TabScreens.js 파일 생성

* `src/Screens/TabScreens.js`

  ```react
  import React from 'react';
  import styled from 'styled-components/native';
  
  const Container = styled.View`
    flex: 1;
    justify-content: center;
    align-items: center;
  `;
  
  const StyledText = styled.Text`
    font-size: 30px;
  `;
  
  export const Mail = () => {
    return (
      <Container>
        <StyledText>Mail</StyledText>
      </Container>
    );
  };
  
  export const Meet = () => {
    return (
      <Container>
        <StyledText>Mail</StyledText>
      </Container>
    );
  };
  
  export const Settings = () => {
    return (
      <Container>
        <StyledText>Settings</StyledText>
      </Container>
    );
  };
  ```

  * 화면 확인 가능한 컴포넌트 3개 생성
  * 한 파일에 했지만 따로 분리 가능

* 생성된 컴포넌트로 탭 내비게이션 만들어보자

* `src/navigations/Tab.js`

  ```react
  import React from 'react';
  import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
  import { Mail, Meet, Settings } from '../screens/TabScreens';
  
  const Tab = createBottomTabNavigator();
  
  const TabNavigation = () => {
    return (
      <Tab.Navigator>
        <Tab.Screen name="Mail" component={Mail} />
        <Tab.Screen name="Meet" component={Meet} />
        <Tab.Screen name="Settings" component={Settings} />
      </Tab.Navigator>
    );
  };
  
  export default TabNavigation;
  ```

  * `createBottomTabNavigator` 함수 이용해 탭 내비게이션 생성
  * 스택 내비게이션과 동일하게
    * Navigator 컴포넌트
    * Screen 컴포넌트 존재
  * 앞에서 만든 컴포넌트들을 Screen 컴포넌트의 component로 지정해 화면으로 사용 및 Navigator 컴포넌트로 감싸줌

* 완성된 탭 내비게이션을 App 컴포넌트에서 써보자

* `App.js`

  ```react
  import React from "react";
  import { NavigationContainer } from "@react-navigation/native";
  import StackNavigation from "./navigations/Stack";
  import TabNavigation from "./navigations/Tab";
  
  const App = () => {
    return (
      <NavigationContainer>
        <TabNavigation />
      </NavigationContainer>
    )
  };
  
  export default App;
  ```

  * 결과를 보면 하단에 3개 버튼 놓인 탭 바가 있고
  * 탭 버튼 클릭 시마다 화면 변경되는 것 확인 가능

* 탭 바에 있는 버튼의 순서

  * Navigator 컴포넌트의 자식으로 있는 Screen 컴포넌트 순서와 동일
  * 첫 번째 자식 컴포넌트를 첫 화면으로 사용
  * 탭 버튼 순서 변경하지 않고 렌더링 되는 첫 화면 변경하고 싶을 때 `initailRouteName` 속성 사용

* `src/navigations/Tabs.js`

  ```react
      <Tab.Navigator initialRouteName="Settings">
        <Tab.Screen name="Mail" component={Mail} />
        <Tab.Screen name="Meet" component={Meet} />
        <Tab.Screen name="Settings" component={Settings} />
      </Tab.Navigator>
  ```



### 탭 바 수정하기

#### 버튼 아이콘 설정하기

* 탭 버튼에 아이콘 렌더링 하는 법

  * `tabBarIcon` 사용
  * `tabBarIcon` 에 설정된 함수에는 color, size, focused 값 포함한 객체가 파라미터로 전달됨

* `src/navigations/Tab.js`

  ```react
  import React from 'react';
  import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
  import { Mail, Meet, Settings } from '../screens/TabScreens';
  import { MaterialCommunityIcons } from '@expo/vector-icons';
  
  const TabIcon = ({ name, size, color }) => {
    return <MaterialCommunityIcons name={name} size={size} color={color}/>
  };
  
  const Tab = createBottomTabNavigator();
  
  const TabNavigation = () => {
    return (
      <Tab.Navigator initialRouteName="Settings">
        <Tab.Screen
          name="Mail"
          component={Mail}
          options={{
            tabBarIcon: props => TabIcon({ ...props, name: 'email' })
          }}
        />
        <Tab.Screen
          name="Meet"
          component={Meet}
          options={{
            tabBarIcon: props => TabIcon({ ...props, name: 'video' })
          }}
        />
        <Tab.Screen
          name="Settings"
          component={Settings}
          options={{
            tabBarIcon: props => TabIcon({ ...props, name: 'phone-settings' })
          }}
        />
      </Tab.Navigator>
    );
  };
  
  export default TabNavigation;
  ```

  * 음... settings 가 외 읎을까...
  * 만약  Screen 컴포넌트마다 탭 버튼 아이콘 지정하지 않고 한곳에서 모든 버튼의 아이콘 관리하고 싶은 경우
    * Navigator 컴포넌트의 screenOptions 속성을 사용해 관리 가능

* `src/navigations/Tab.js`

  ```react
  import React from 'react';
  import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
  import { Mail, Meet, Settings } from '../screens/TabScreens';
  import { MaterialCommunityIcons } from '@expo/vector-icons';
  
  const TabIcon = ({ name, size, color }) => {
    return <MaterialCommunityIcons name={name} size={size} color={color}/>
  };
  
  const Tab = createBottomTabNavigator();
  
  const TabNavigation = () => {
    return (
      <Tab.Navigator
        initialRouteName="Settings"
        screenOptions={({ route }) => ({
          tabBarIcon: props => {
            let name = '';
            if (route.name === 'Mail') name = 'email';
            else if (route.name === 'Meet') name = 'video';
            else name = 'account-settings';
            return TabIcon({ ...props, name });
          }
        })}
      >
        <Tab.Screen name="Mail" component={Mail} />
        <Tab.Screen name="Meet" component={Meet} />
        <Tab.Screen name="Settings" component={Settings} />
      </Tab.Navigator>
    );
  };
  
  export default TabNavigation;
  ```

  * screenOptions에 객체를 반환하는 함수를 설정하고
  * 함수로 전달되는  route를 이용
  * Screen 컴포넌트의  name 속성을 값으로 갖는  route의 name값에 따라 렌더링되는 아이콘이 변경되도록 작성
  * Screen 컴포넌트마다 options에  tabBarIcon을 설정하는 방법과 Navigator 컴포넌트에서 screenOptions를 이용하는 방법의 결과는 동일



#### 라벨 수정하기

* 라벨

  * 버튼 아이콘 아래에 렌더링 되는 텍스트
  * Screen 컴포넌트의  name 값을 기본값으로 사용

* 탭 버튼의 라벨은 tabBarLabel을 이용해 변경 가능

* `src/navigations/Tab.js`

  ```react
        <Tab.Screen
          name="Mail"
          component={Mail}
          options={{
            tabBarLabel: 'Inbox',
            tabBarIcon: props => TabIcon({ ...props, name: 'email' })
          }}
        />
  ```

* 라벨을 버튼 아이콘의 아래가 아닌 아이콘 옆에 렌더링되도록 변경하고 싶다면?

  * `tabBarLabelPosition`의 값을 변경해서 조정 가능
  * below-icon
  * beside-icon 두 값만 설정 가능

* `src/navigations/Tab.js`

  ```react
      <Tab.Navigator
        initialRouteName="Settings"
        screenOptions={{ tabBarLabelPosition: 'beside-icon' }}
      >
  ```

* 라벨없이 아이콘만 쓰고 싶당
  * `tabBarShowLabel` 옵션 사용



#### 스타일 수정하기

* 탭 내비게이션 탭 바 배경은 흰색이 기본

* 우선 화면 배경색 바꾸자

* `src/screens/TabScreens.js`

  ```react
  const Container = styled.View`
    flex: 1;
    justify-content: center;
    align-items: center;
    background-color: #54b7f9;
  `;
  
  const StyledText = styled.Text`
    font-size: 30px;
    color: #ffffff;
  `;
  ```

* 이번엔 탭 바 스타일 변경해보자

* 탭 바 스타일은  `tabBarOptions` 속성에 style의 값으로 스타일 객체 설정하여 변경 가능

* `src/navigations/Tab.js`

  ```react
      <Tab.Navigator
        initialRouteName="Settings"
        screenOptions={{ 
          tabBarLabelPosition: 'beside-icon',
          tabBarShowLabel: false,
          tabBarStyle: {
            backgroundColor: '#54b7f9',
            borderTopColor: '#ffffff',
            borderTopWidth: 2,
          }
        }}
      >
  ```

* 바꾸고 보니 아이콘 색도 회색이어서 안어울리네잉

* 탭 버튼 아이콘 선택되어 활성화됨 / 비활성하됨 상태 각각 activeTintColor & inactiveTintColor 이용해 설정 가능

* `src/navigations/Tab.js`

  ```react
      <Tab.Navigator
        initialRouteName="Settings"
        screenOptions={{ 
          tabBarLabelPosition: 'beside-icon',
          tabBarShowLabel: false,
          tabBarStyle: {
            backgroundColor: '#54b7f9',
            borderTopColor: '#ffffff',
            borderTopWidth: 2,
          },
          tabBarActiveTintColor: '#ffffff',
          tabBarInactiveTintColor: '#0b92e9',
        }}
      >
  ```

* 앞서 설정한 `barTabIcon`에 설정한 함수에는 파라미터로 size, color, focused를 가진 객체가 전달됨

* 이 값 중 focused는 버튼의 선택된 상태를 나타내는 값

* 이 값을 이용하면 버튼의 활성화 상태에 따라 다른 버튼을 렌더링하거나 스타일 변경 가능

* 버튼 활성화 상태에 따라 다른 아이콘 렌더링되도록 변경해보자

* `src/navigations/Tab.js`

  ```react
        <Tab.Screen
          name="Mail"
          component={Mail}
          options={{
            tabBarLabel: 'Inbox',
            tabBarIcon: props => TabIcon({
              ...props,
              name: props.focused ? 'email' : 'email-outline',
            })
          }}
        />
        <Tab.Screen
          name="Meet"
          component={Meet}
          options={{
            tabBarIcon: props => TabIcon({
              ...props,
              name: props.focused ? 'video' : 'video-outline',
            })
          }}
        />
        <Tab.Screen
          name="Settings"
          component={Settings}
          options={{
            tabBarIcon: props => TabIcon({
              ...props,
              name: props.focused ? 'account-settings' : 'account-settings-outline',
            })
          }}
        />
  ```

  

