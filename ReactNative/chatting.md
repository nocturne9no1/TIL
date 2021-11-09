# Chatting Application

* 채팅 동작을 위한 최소한의 기능
  * 로그인 / 회원가입
    * 이메일과 비번 이용한 로그인/회원가입
  * 프로필
    * 나의 정보 확인 및 변경
  * 채널 생성
    * 채널 생성 기능
  * 채널 목록
    * 생성된 채널들의 목록 조회
  * 채널
    * 실시간으로 메시지를 송수신하는 독립된 공간

## 프로젝트 준비

```bash
expo init react-native-simple-chat
```

### navigation

* 지금부터 만들 채팅 앱은 크게 세 부분으로 나눌 수 있음
  * 로그인 등 인증 화면
  * 채팅방 목록 확인 화면
  * 메시지 주고 받는 화면
* 화면 유기적으로 연결되어 있으며 이동 잦음

```bash
npm install @react-navigation/native
```

```bash
expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view
```

* 현재 프로젝트는 총 6개 화면으로 구성됨

  1. 로그인
  2. 회원가입
  3. 프로필
  4. 채팅방 목록
  5. 채팅방 생성
  6. 채팅방

  

  * 스택 내비
  * 탭 내비
  * 활용하여 화면 구조 만들 것임

```bash
npm install @react-navigation/stack @react-navigation/bottom-tabs
```

```bash
npm install styled-components
```



* `src/theme.js`

  ```react
  import { Colors } from "react-native/Libraries/NewAppScreen";
  
  const colors ={
    white: '#ffffff',
    black: '#000000',
    grey_0: '#d5d5d5',
    grey_1: '#a6a6a6',
    red: '#e84118',
    blue: '#3679fe',
  };
  
  export const theme = {
    background: colors.white,
    text: colors.black,
  };
  ```

  * 공통으로 사용할 색 정의
  * 배경 글자 색 미리 정의

* `src/App.js`

  ```react
  import React from "react";
  import { StatusBar } from "expo-status-bar";
  import { ThemeProvider } from "@react-navigation/native";
  import { theme } from "./theme";
  
  const App = () => {
    return (
      <ThemeProvider theme={theme}>
        <StatusBar barStyle="dark-content" />
      </ThemeProvider>
    );
  };
  
  export default App;
  ```

  

* `App.js`

  ```react
  import App from "./src/App";
  
  export default App;
  ```

* 폴더 생성

  * components: 컴포넌트 관리
  * contexts: Context API 파일 관리
  * navigations: 내비게이션 파일 관리
  * screens: 화면 파일 관리
  * utils: 프로젝트에서 이용할 기타 기능 관리



## 파이어베이스

* 파이어베이스는 인증, DB, 등 다양한 기능 제공하는 개발 플랫폼
* 파이어베이스가 제공하는 기능 이용하면 서버 DB 직접 구축 안해도 개발 가능



* 파이어베이스 이용 위해선 콘솔에서 프로젝트 생성해야 함
* 생성 뒤 웹 메뉴로 들어가 앱 등록을 마친 뒤
* 나오는 firebaseConfig 값을 프로젝트 루트 폴더에 firebase.json 에 적어줌



### 인증

* 인증 메뉴에서 "이메일/비밀번호" 부분 화라성화

### 데이버베이스

* 여기서는 생성되는 채널과 각 채널에서 발생하는 메시지를, 파이어베이스의 데이터베이스를 이용하여 관리
* 데이터베이스는 `파이어스토어`와 `실시간 데이터베이스` 두 가지 종류 제공
* 여기서는 파이어스토어 이용할 것임



* firebase 콘솔 파이어스토에서 `asia-northeast3` 선택 후 db 생성

### Storage

* 스토리지는 서버 코드 없이 사용자의 사진, 동영상 등을 저장할 수 있는 기능을 쉽게 개발할 수 있도록 기능 제공
* 여기서는 채팅 앱에 가입한 사용자의 사진을 저장하고 가져오는 기능 만들 예정



* 이상하다 책에는 만들라 돼있는데 나는 그냥 돼있넹

### Install Library

* 리액트 네이티브에서 파이어베이스 사용 위해 라이브러리 설치 필요

```bash
expo install firebase
```

* 라이브러리 설치 후 `utils` 폴더 아래에 `firebase.js` 파일 생성

* `src/utils/firebase.js`

  ```react
  import * as firebase from "firebase";
  import config from "../../firebase.json";
  
  const app = firebase.initializeApp(config);
  ```

* 이제 firebase 사용 준비 완료



## 앱 아이콘과 로딩 화면

* 프로젝트 기능과 화면 개발에 앞서 앱 아이콘과 로딩 화면 먼저 변경해보자
* 앱 아이콘으로 사용할
  * 1024 x 1024 크기의 `icon.png` 파일 
  * 로딩 화면으로 사용할 1242 x 2436 크기의 `splash.png` 파일 생성해
  * assets 폴더에 자동으로 생성된 파일들과 교체하고 App 컴포넌트를 다음과 같이 수정

* `src/App.js`

  ```react
  import React, { useState } from "react";
  import { StatusBar } from "expo-status-bar";
  import { Image } from "react-native";
  
  import { AppLoading } from "expo";
  import { Asset } from "expo-asset";
  import * as Font from "expo-font";
  
  import { ThemeProvider } from "@react-navigation/native";
  import { theme } from "./theme";
  
  const cacheImages = (images) => {
    return images.map((image) => {
      if (typeof image === "string") {
        return Image.prefetch(image);
      } else {
        return Asset.fromModule(image).downloadAsync();
      }
    });
  };
  const cacheFonts = (fonts) => {
    return fonts.map((font) => Font.loadAsync(font));
  };
  
  const App = () => {
    const [isReady, setIsReady] = useState(false);
  
    const _loadAssets = async () => {
      const imageAssets = cacheImages([require("../assets/splash.png")]);
      const fontAssets = cacheFonts([]);
  
      await Promise.all([...imageAssets, ...fontAssets]);
    };
    return isReady ? (
      <ThemeProvider theme={theme}>
        <StatusBar barStyle="dark-content" />
      </ThemeProvider>
    ) : (
      <AppLoading
        startAsync={_loadAssets}
        onFinish={() => setIsReady(true)}
        onError={console.warn}
      />
    );
  };
  
  export default App;
  
  ```

  * 앞으로 사용할 이미지와 폰트를 미리 불러와 사용할 수 있도록 `cacheImages`와 `cacheFonts` 함수 작성
    * 이를 이용해 `_loadAssets` 함수 구성
    * 이미지나 폰트 미리 불러오려면 애플리케이션을 사용하는 환경에 따라 이미지나 폰트가 느리게 적용되는 문제 개선 가능
  * 애플리케이션은 미리 불러와야 하는 항목들을 모두 불러오고 화면이 렌더링 되도록
    * `AppLoading` 컴포넌트의 `startAsync`에 `_loadAssets` 함수를 지정하고
    * 완료되었을 때 `isReady` 상태를 변경해서 화면이 렌더링 되도록 작성

  * 여기서 실행 시 오류 남

    ```bash
    expo install expo-app-loading
    ```

    * 저거 없어서 오류나는 듯?
    * 저거 받은 후
    * `import { AppLoading }` 에서 중괄호 빼야함
    * 모듈에 export default `AppLoading` 으로 돼있기 때문



## 인증 화면

* 이번에는 파이어베이스 인증 기능 이용해 로그인 화면과 회원가입 화면 만들어보자
* 인증을 위해 이멜과 비번이 필요
  * 로그인 및 회원가입 화면에서는 이메일과 비밀번호 필수로 입력
  * 회원가입 시 사용자가 서비스에서 사용할 이름과 프로필 사진을 받도록 화면 구성



### Navigation

* 먼저 로그인 화면과 회원가입 화면으로 사용할 컴포넌트를 `screen` 폴더 밑에 만듬
* 먼저 로그인 화면 작성해보자

* `src/screens/Signup.js`

  ```bash
  import React from "react";
  import styled from "styled-components/native";
  import { Text, Button } from "react-native";
  
  const Container = styled.View`
    flex: 1;
    justify-content: center;
    align-items: center;
    background-color: ${({ theme }) => theme.background};
  `;
  
  const Login = ({ navigation }) => {
    return (
      <Container>
        <Text style={{ fontSize: 30 }}>Login Screen</Text>
        <Button title="Signup" onPress={() => navigation.navigate("Signup")} />
      </Container>
    );
  };
  
  export default Login;
  ```

* 그 다음은 회원가입

* `src/screens/Signup.js`

  ```react
  import React from "react";
  import styled from "styled-components/native";
  import { Text } from "react-native";
  
  const Container = styled.View`
    flex: 1;
    justify-content: center;
    align-items: center;
    background-color: ${({ theme }) => theme.background};
  `;
  
  const Signup = () => {
    return (
      <Container>
        <Text style={{ fontSize: 30 }}>Signup Screen</Text>
      </Container>
    );
  };
  
  export default Signup;
  ```

* `src/screens/index.js`

  ```react
  import Login from "./Login";
  import Signup from "./Signup";
  
  export { Login, Signup };
  ```

* 이제 화면 준비 완료

* 스택 내비게이션 작성 ㄱㄱ

* `src/navigations/AuthStack.js`

  ```react
  import React, { useContext } from "react";
  import { ThemeContext } from "styled-components/native";
  import { createStackNavigator } from "@react-navigation/stack";
  import { Login, Signup } from "../screens";
  
  const Stack = createStackNavigator();
  
  const AuthStack = () => {
    const theme = useContext(ThemeContext);
    return (
      <Stack.Navigator
        initialRouteName="Login"
        screenOption={{
          headerTitleAlign: "center",
          cardStyle: { backgroundColor: theme.backgroundColor },
        }}
      >
        <Stack.Screen name="Login" component={Login} />
        <Stack.Screen name="Signup" component={Signup} />
      </Stack.Navigator>
    );
  };
  
  export default AuthStack;
  ```

  * 첫 화면 로그인 화면으로 하고
  * 로그인 화면과 회원가입 화면 가진 내비게이션 작성
  * 스타일드 컴포넌트에서 제공하는 `ThemeContext`와 `useContext` Hook 함수를 이용해 theme을 받아옴
  * 헤더의 타이틀 위치를 안드로이드와 iOS에서 동일한 위치에 렌더링하기 위해 headerTitleAlign 값 center로 설정

* `src/navigations/index.js`

  ```react
  import React from "react";
  import { NavigationContainer } from "@react-navigation/native";
  import AuthStack from "./AuthStack";
  
  const Navigation = () => {
    return (
      <NavigationContainer>
        <AuthStack />
      </NavigationContainer>
    );
  };
  
  export default Navigation;
  ```

  * `NavigationContainer` 컴포넌트를 사용하고
  * 자식 컴포넌트로 `AuthStack` 내비게이션 사용

* 작성된 내비게이션 렌더링되도록 App 컴포넌트 다음과 같이 수정

* `src/App.js`

  ```react
  ...
  import Navigation from "./navigations";
  
  ...
  
  return isReady ? (
      <ThemeProvider theme={theme}>
        <StatusBar barStyle="dark-content" />
        <Navigation />
      </ThemeProvider>
    )
  
  ...
  ```

  

