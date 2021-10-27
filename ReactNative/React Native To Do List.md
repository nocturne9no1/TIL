# React Native To Do List

```bash
npm install styled-components prop-types
```

* styled-components - javascript 에서 css 를 사용할 수 있도록 도와주는 스타일링 프레임워크
* prop-types - prop 의 type을 검사하는 라이브러리



## 기본 기능

### 기본 틀

* src/theme.js

  ```js
  export const theme = {
    background: '#101010',
    itemBackground: '#313131',
    main: '#778bdd',
    text: '#cfcfcf',
    done: '#616161',
  };
  ```

  * theme.js 를 만들어 themeprovider 와 함께 사용하여 app 전체에 색을 변수화 할 수 있음



* src/app.js

  ```react
  import React from 'react';
  import { StyleSheet, Text, View, Button } from 'react-native';
  import styled, { ThemeProvider } from 'styled-components';
  import { theme } from './src/theme';
  
  const Container = styled.View`
    flex: 1;
    background-color: ${({ theme }) => theme.background };
    align-items: center;
    justify-content: center;
  `
  
  export default function App() {
  
    return (
      <ThemeProvider theme={theme}>
        <Container></Container>
      </ThemeProvider>
    );
  }
  ```

  * theme.js 를 이용하여 컨테이너 구성 및 스타일링

  ```react
  const Title = styled.Text`
    font-size: 40px;
    font-weight: 600;
    color: ${({ theme }) => theme.main };
    align-self: flex-start;
    margin: 0px 20px;
  `;
  ```

  * Title 컴포넌트 생성

  ```react
  const Container = styled.SafeAreaView`
    flex: 1;
    background-color: ${({ theme }) => theme.background };
    align-items: center;
    justify-content: flex-start;
  `
  ```

  * 아이폰의 노치 디자인에 의해 가려짐을 방지하기 위해 `SafeAreaView` 사용

  ```react
  export default function App() {
  
    return (
      <ThemeProvider theme={theme}>
        <Container>
          <StatusBar 
            barStyle="light-content"
            backgroundColor={theme.background}
          />
          <Title>TODO List</Title>
        </Container>
      </ThemeProvider>
    );
  }
  ```

  * 또한 안드로이드 환경에서 상태 바에 의해 글자 가려짐 방지를 위해 스타일링 수정



* src/components/Input.js

  ```react
  import React from "react";
  import styled from "styled-components";
  
  const StyledInput = styled.TextInput`
    width: 100%;
    hegith: 60px;
    margin: 3px 0;
    padding: 15px 20px;
    border-radius: 10px;
    background-color: ${({ theme }) => theme.itembackground};
    font-size: 25px;
    color: ${({ theme }) => theme.text}
  `;
  
  const Input = () => {
    return <StyledInput/>;
  };
  
  export default Input;
  ```

  * 커스텀 인풋 창 만들기
  * 만든 후 app.js 에 import



* Dimensions

  * 위에 만든 input 컴포넌트는 양 옆 너무 꽉차서 답답해보임
  * 양 옆 20px 씩 공백 주려면 어케해야 할까?
  * RN에선 크기 다양한 모바일 기기 대응위해 현재 화면 크기 알 수 있는
    * Dimensions
    * useWindowDimensions 제공
  * Dimensions 의 경우 처음 값 크기로 고정되기에
    * 기기를 회전하여 화면 전환되면 변환된 화면 크기와 일치하지 않을수도
    * 이벤트 리스너 등록 통해 화면 크기 변화에 대응할 수 있도록 기능 제공
  * useWindowDimensions 는 RN에서 제공하는 Hooks 중 하나
    * 화면 크기 변경되면 자동 업데이트
  * 아직 Hooks 잘 모르기에 일단 Dimensions 써보자

  ```react
  import { Dimensions } from "react-native";
  
  const StyledInput = styled.TextInput`
    width: ${({ width }) => width - 40}px;
    height: 60px;
    margin: 3px 0;
    padding: 15px 20px;
    border-radius: 10px;
    background-color: ${({ theme }) => theme.itemBackground};
    font-size: 25px;
    color: ${({ theme }) => theme.text}
  `;
  
  const Input = () => {
    const width = Dimensions.get('window').width;
  
    return <StyledInput width={width} />;
  };
  ```

  * `Dimensions.get('window')` 를 통해 { width, height } 값 얻을 수 있다.
  * 후에 width - 40 px 값을 지정해주면 된다.
  
  ```react
  const StyledInput = styled.TextInput.attrs(({ theme }) => ({
    placeholderTextColor: theme.main,
  }))`
    width: ${({ width }) => width - 40}px;
    height: 60px;
    margin: 3px 0;
    padding: 15px 20px;
    border-radius: 10px;
    background-color: ${({ theme }) => theme.itemBackground};
    font-size: 25px;
    color: ${({ theme }) => theme.text}
  `;
  ```
  
  * 스타일드 컴포넌트의 attrs를 이용해 theme에 정의된 색상을 placeholder 색으로 설정
  
  ```react
    return (
      <StyledInput
        width={width}
        placeholder={placeholder} 
        autoCapitalize="none"
        autoCorrect={false}
        returnKeyType="done"
      />
    );
  ```
  
  * autoCaplitalize: 자동 대문자 전환
  * autoCorrect: 자동 수정 기능
  * returnKeyType: 키보드 완료 버튼 설정
    * dont / next 처럼 두 플렛폼 모두 가능 한 것도 있지만
    * iOS 에만 적용되는 none
    * 안드로이드에만 적용되는 join 같은 것도 있음
  * (option) keyboardAppearnace="dark"
    * iOS 키보드 검은색 변경
    * 왜 안되징
  
* app.js

  ```react
    const [ newTask, setNewTask ] = useState('');
  
    const _addTask = () => {
      alert(`ADD: ${newTask}`);
      setNewTask('');
    };
  
    const _handleTextChange = text => {
      setNewTask(text);
    };
  ```

  * 입력 값을 저장하고 보여주기 위해 위와 같은 변수, 함수 지정

  ```react
  <Input
      placeholder="+ Add a Task"
      value={newTask}
      onChangeText={_handleTextChange}
      onSubmitEditing={_addTask}
  />
  ```

  * Input 컴포넌트에 속성 추가

* src/Input.js

  ```react
  const Input = ({ placeholder, value, onChangeText, onSumbitEditing }) => {
    const width = Dimensions.get('window').width;
  ```

  * props 전달

  ```react
  <StyledInput
      width={width}
      placeholder={placeholder} 
      autoCapitalize="none"
      autoCorrect={false}
      returnKeyType="done"
      value={value}
      onChangeText={onChangeText}
      onSumbitEditing={onSumbitEditing}
  />
  ```

  * 전달받은 값 사용

  ```react
  Input.propTypes = {
    placeholder: PropTypes.string,
    value: PropTypes.string.isRequired,
    onChangeText: PropTypes.func.isRequired,
    onSubmitEditing: PropTypes.func.isRequired,
  }
  ```

  * 타입 검사
  * 아직 잘 모르겠움
  * autoCorrect={false} 안됨

* https://fonts.google.com/icons?icon.query=check

  * 여기서 필요한 png 아이콘 받을 수 있음
  * ios 로 받으면 2배 3배를 볼 수 있음
  * 파일명, 파일명@2x, 파일명@3x 로 바꾸어
  * assets 폴더에 icons 폴더 생성하여 집어넣음
  * 이렇게 파일명 동일 이름 사용뒤 뒤에 @2x 같이 붙이면
  * 리액트 네이티브에서 화면 사이즈에 알맞은 크기의 이미지를 자동으로 불러와 사용

* src/images.js

  ```react
  import CheckBoxOutline from '../assets/icons/outline_check_box_outline.png';
  import CheckBox from '../assets/icons/checkbox.png';
  import DeleteForever from '../assets/icons/outline_delete.png';
  import Edit from '../assets/icons/outline_edit_white.png';
  
  export default images = {
    uncompleted: CheckBoxOutline,
    completed: CheckBox,
    delete: DeleteForever,
    update: Edit,
  };
  ```

* src/components/IconButtons.js

  ```react
  import React from "react";
  import { TouchableOpacity } from "react-native";
  import styled from "styled-components/native";
  import PropTypes from 'prop-types';
  import { images } from '../images';
  
  const Icon = styled.Image`
    tint-color: ${({ theme }) => theme.text};
    width: 30px;
    height: 30px;
    margin: 10px;
  `;
  
  const IconButton = ({ type, onPressOut }) => {
    return (
      <TouchableOpacity onPressOut={onPressOut}>
        <Icon source={type} />
      </TouchableOpacity>
    );
  };
  
  IconButton.propTypes = {
    type: PropTypes.oneOf(Object.values(images)).isRequired,
    onPressOut: PropTypes.func,
  }
  
  export default IconButton;
  ```

  * 이미지 종류별로 컴포넌트를 만들지 않고
    * IconButton 컴포넌트 호출 시 원하는 이미지 종류를
    * props에 type으로 전달하도록 작성
    * 아이콘 색은 입력되는 텍스트와 동일한 색 사용하도록 스탕리 적용
    * 사람 손가락 버튼 정확하게 클릭 못할 수 있으므로
    * UX 위해 버튼 주변 클릭 시에도 클릭으로 인식 위해 적정 수준의 margin 적용



* src/components/Task.js

  ```react
  import React from "react";
  import styled from "styled-components/native";
  import PropTypes from 'prop-types';
  import IconButton from "./IconButton";
  import { images } from '../images';
  
  const Container = styled.View`
    flex-direction: row;
    align-items: center;
    background-color: ${({ theme }) => theme.itemBackground};
    border-radius: 10px;
    padding: 5px;
    margin: 3px 0px;
  `;
  
  const Contents = styled.Text`
    flex: 1;
    font-size: 24px;
    color: ${({ theme }) => theme.text};
  `;
  
  const Task = ({ text }) => {
    return (
      <Container>
        <IconButton type={images.uncompleted} />
        <Contents>{text}</Contents>
        <IconButton type={images.update} />
        <IconButton type={images.delete} />
      </Container>
    );
  };
  
  Task.propTypes = {
    text: PropTypes.string.isRequired,
  };
  
  export default Task;
  ```

  * 할 일 내용 props 로 전달돼 오는 값 활용



* app.js

  ```react
  const List = styled.ScrollView`
    flex: 1;
    width: ${({ width }) => width - 40}px;
  `;
  
  ...
  
  <List width={width}>
    <Task text="asdfasdf"/>
  </List>
  ```

  * App.js 에 List 컴포넌트 추가해서 Task 보여줌

### 할 일 추가

* app.js

  ```react
    const [ tasks, setTasks ] = useState({
      '1': { id: '1', text: 'create', completed: false },
      '2': { id: '2', text: 'read', completed: false },
      '3': { id: '3', text: 'update', completed: false },
      '4': { id: '4', text: 'delete', completed: false },
    })
    
    ...
    
            <List width={width}>
            {Object.values(tasks)
              .reverse()
              .map(item => (
                <Task text={item.text} />
              ))
            }
          </List>
  ```

  * 시작값 넣고

  * map 함수 통해 하나씩 랜더링

  * Object 는 뭘까?

  * 여기서 키값 없다는 오류 뜸

  * key

    * 리액트 컴포넌트 배열 렌더링 시

    * 어떤 아이템이 추가, 수정, 삭제되었는지 식별하는 것을 돕는 고유값

    * 리액트에서 특별하게 관리

    * 자식 컴포넌트의 props로 전달되지 않음

    * ```react
      <Task key={item.id} text={item.text} />
      ```

    * Task 컴포넌트를 다음과 같이 바꿔 오류 해결

  ```react
    const _addTask = () => {
      const ID = Date.now().toString();
      const newTaskObject = {
        [ID]: { id: ID, text: newTask, completed: false },
      };
      setNewTask('');
      setTasks({ ...tasks, ...newTaskObject })
    }
  ```

  * 새 할 일 추가를 위한 함수 생성
  * id에 항목 추가되는 시간의 timestamp 를 이용하고
  * 내용 나타내는 text에 input 컴포넌트에 입력된 값 지정
  * completed 는 false로 초기화
  * newTask 값 ''(빈 스트링) 으로 만들어 Input 컴포넌트 초기화
  * 기존 목록 유지한 상태에서 새로운 항목 추가되도록 구성
  * 이제 할 일 추가 됨



### 삭제

* app.js

  ```react
    const _deleteTask = id => {
      const currentTasks = Object.assign({}, tasks);
      delete currentTasks[id];
      setTasks(currentTasks);
    };
  
  ...
  
                <Task key={item.id} item={item.text} deleteTask={_deleteTask}/>
  ```

  * 삭제 버튼 클릭 시 항목 id 이용하여 tasks에서 해당 항목 삭제하는 함수 작성

* src/components/Task.js

  ```react
  const Task = ({ item, deleteTask }) => {
  
    return (
      <Container>
        <IconButton type={images.uncompleted} />
        <Contents>{item.text}</Contents>
        <IconButton type={images.update} />
        <IconButton type={images.delete} id={item.id} onPressOut={deleteTask}/>
      </Container>
    );
  };
  ```

  * Task 컴포넌트에서 props 를 전달받는다

* src/components/IconButton.js

  ```react
  const IconButton = ({ type, onPressOut, id }) => {
    const _onPressOut = () => {
      onPressOut(id);
    }
  
    return (
      <TouchableOpacity onPressOut={_onPressOut}>
        <Icon source={type} />
      </TouchableOpacity>
    );
  };
  
  IconButton.defaultProps = {
    onPressOut: () => {},
  };
  ```

  * IconButton 컴포넌트에서 전달된 함수 이용
  * porps로 onPressOut이 전달되지 않았을 경우에도 문제 발생 않도록
  * defaultProps를 이용해 onPressOut의 기본값 지정
  * 이제 삭제 가능



### 완료 기능

* app.js

  ```react
    const _toggleTask = id => {
      const currentTasks = Object.assign({}, tasks);
      currentTasks[id]['completed'] = !currentTasks[id]['completed'];
      setTasks(currentTasks);
    };
  
  ...
  
          <List width={width}>
            {Object.values(tasks)
              .reverse()
              .map(item => (
                <Task
                  key={item.id}
                  item={item} 
                  deleteTask={_deleteTask}
                  toggleTask={_toggleTask}
                />
              ))
            }
          </List>
  ```

  * 함수 호출 될 때마다 완료 여부 나타내는 completed 값 전환되는 함수 작성

* src.components/Task.js

  ```react
        <IconButton
          type={item.completed ? images.completed : images.uncompleted}
          id={item.id}
          onPressOut={toggleTask}
        />
  ```

  * props로 전달된 toggleTask 함수를 완료 상태를 나타내는 버튼의 onPressOut으로 설정
  * 항목 완료 여부에 따라 버튼 이미지 다르게 나타나도록 수정



* 완료 시에는 수정 버튼 안보이게 해보자

* 추가적으로 미완료 항목과 조금 더 명확하게 구분되도록 디자인 수정

* src/components/Task.js

  ```react
  const Contents = styled.Text`
    flex: 1;
    font-size: 24px;
    color: ${({ theme, completed }) => (completed ? theme.done : theme.text )};
    text-decoration-line: ${({ completed }) =>
      completed ? 'line-through' : 'none'}
  `;
  
  ...
  
      <Container>
        <IconButton
          type={item.completed ? images.completed : images.uncompleted}
          id={item.id}
          onPressOut={toggleTask}
          completed={item.completed}
        />
        <Contents completed={item.completed}>{item.text}</Contents>
        {item.completed || <IconButton type={images.update} />}
        <IconButton 
          type={images.delete} 
          id={item.id} 
          onPressOut={deleteTask}
          completed={item.completed}
        />
      </Container>
  ```

  * 각 item 의 completed 값에 따라 수정 버튼 랜더링 여부를 결정하도록 수정
  * Contents 컴포넌트에 completed 전달 후 완료 여부에 따라 취소선 나오고 글자 색 변경
  * 아이콘 버튼에도 complted 전달함
  * 이제 IconButton 컴포넌트에서 completed 값에 따른 스타일 적용되도록 수정해보자

  

* src/components/IconButton.js

  ```react
  const Icon = styled.Image`
    tint-color: ${({ theme, completed }) => 
      completed ? theme.done : theme.text};
    width: 30px;
    height: 30px;
    margin: 10px;
  `;
  
  const IconButton = ({ type, onPressOut, id, completed }) => {
    const _onPressOut = () => {
      onPressOut(id);
    }
  
    return (
      <TouchableOpacity onPressOut={_onPressOut}>
        <Icon source={type} completed={completed}/>
      </TouchableOpacity>
    );
  };
  ```

  * IconButton 컴포넌트에서도 항목 완료 여부에 따라 아이콘 이미지 색 변경되도록 수정



### 수정 기능

* 수정 버튼 클릭 시 해당 항목이 Input 컴포넌트로 변경되며 내용 수정 할 수 있도록 구현

* 우선 App 컴포넌트에서 수정 완료 된 항목이 전달되면 tasks 에서 해당 항목 변경 함수 작성

* App.js

  ```react
    const _updateTask = item => {
      const currentTasks = Object.assign({}, tasks);
      currentTasks[item.id] = item;
      setTasks(currentTasks);
    };
  
  ...
  
          <List width={width}>
            {Object.values(tasks)
              .reverse()
              .map(item => (
                <Task
                  key={item.id}
                  item={item} 
                  deleteTask={_deleteTask}
                  toggleTask={_toggleTask}
                  updateTask={_updateTask}
                />
              ))
            }
          </List>
  ```

  * update 함수 작성 완료
  * 이제 Task 컴포넌트에서 수정 버튼 클릭 시 항목 현재 내용 가진 input 컴포넌트 렌더링되어 사용자가 수정할 수 있도록 만들것

* src/components/Task.js

  ```react
  const Task = ({ item, deleteTask, toggleTask, updateTask }) => {
    const [ isEditing, setIsEditing ] = useState(false);
    const [ text, setText ] = useState(item.text);
  
    const _handleUpdateButtonPress = () => {
      setIsEditing(true);
    };
  
    const _onSubmitEditing = () => {
      if (isEditing) {
        const editedTask = Object.assign({}, item, { text });
        setIsEditing(false);
        updateTask(editedTask)
      }
    };
  
    return (
      isEditing ? (
      <Input
        value={text}
        onChangeText={text => setText(text)}
        onSubmitEditing={_onSubmitEditing}
      /> 
      ) :
      <Container>
        <IconButton
          type={item.completed ? images.completed : images.uncompleted}
          id={item.id}
          onPressOut={toggleTask}
          completed={item.completed}
        />
        <Contents completed={item.completed}>{item.text}</Contents>
        {item.completed || <IconButton type={images.update} onPressOut={_handleUpdateButtonPress}/>}
        <IconButton 
          type={images.delete} 
          id={item.id} 
          onPressOut={deleteTask}
          completed={item.completed}
        />
      </Container>
    );
  };
  ```

  * 수정 상태 관리 위해 isEditing 변수 생성 -> 수정 버튼 클릭되면 값 변하도록 작성
  * 수정되는 내용 담은 text 변수 생성 -> Input 컴포넌트 값으로 설정
  * 화면 isEditing 값 따라 항목 내용 아닌 Input 컴포넌트 렌더링 되도록 수정
  * Input 컴포넌트에서 완료 버튼 클릭 시 App 컴포넌트에서 전달된 updateTask 함수 호출되도록
  * 수정 끝!



### 입력 취소

* 현재 항목 추가하거나 수정 도중 입력 취소 방법이 없음

* 입력 중 다른 영역 클릭하여 Input 컴포넌트가 포커스 잃으면 입력 중인 내용 사라지고 취소되도록 Input 컴포넌트를 수정해보자

* src/components/Input.js

  ```react
  const Input = ({ placeholder, value, onChangeText, onSubmitEditing, onBlur }) => {
    const width = Dimensions.get('window').width;
  
    return (
      <StyledInput
        width={width}
        placeholder={placeholder} 
        autoCapitalize="none"
        autoCorrect={false}
        returnKeyType="done"
        value={value}
        onChangeText={onChangeText}
        onSubmitEditing={onSubmitEditing}
        onBlur={onBlur}
      />
    );
  };
  ```

  * onBlur props 전달

* App.js

  ```react
    const _onBlur = () => {
      setNewTask('');
    };
  
  ...
  
          <Input
            placeholder="+ Add a Task"
            value={newTask}
            onChangeText={_handleTextChange}
            onSubmitEditing={_addTask}
            onBlur={_onBlur}
          />
  ```

  * Input 컴포넌트 포커스 잃으면 추가 중이던 값 초기화하는 onBlur 함수 추가
  * 이제 Task 컴포넌트에서도 수정 중 포커스 잃으면 초기화되도록 수정

* src/components/Task.js

  ```react
  ...
    const _onBlur = () => {
      if (isEditing) {
        setIsEditing(false);
        setText(item.text);
      }
    };
  
    return (
      isEditing ? (
      <Input
        value={text}
        onChangeText={text => setText(text)}
        onSubmitEditing={_onSubmitEditing}
        onBlur={_onBlur}
      /> 
      ) :
  ...
  ```

  * Task 컴포넌트에서도 수정 상태일 때 Input 컴포넌트의 포커스 잃으면 수정 중 내용을 초기화하고 수정 상태 종료하는 함수 추가



## 부가 기능

### 데이터 저장

* React Native 에서는 AsyncStorage 이용해 로컬에 데이터 저장 및 불러오기 기능 구현 가능

* AsyngStorage 는 비동기로 동작

  * key-value 형태의 데이터를 기기에 저장하고 불러올 수 있는 기능 제공

* ```bash
  expo install @react-native-community/async-storage
  ```

* expo install 은 npm install 과 거의 동일하지만 사용 중인 Expo SDK 버전과 호환되는 버전이 있는지 확인하고 해당 버전 라이브러리를 설치하는 과정이 추가되었다는 차이점이 있음

* app.js

  ```react
  ...
  import AsyncStorage from '@react-native-community/async-storage';
  
  ...
  
    const _saveTask = async tasks => {
      try {
        await AsyncStorage.setItem('tasks', JSON.stringify(tasks));
        setTasks(tasks);
      } catch (e) {
        console.log(e);
      }
    };
  
    const _addTask = () => {
      const ID = Date.now().toString();
      const newTaskObject = {
        [ID]: { id: ID, text: newTask, completed: false },
      };
      setNewTask('');
      _saveTask({ ... tasks, ...newTaskObject })
      // setTasks({ ...tasks, ...newTaskObject })
    }
    
      const _deleteTask = id => {
      const currentTasks = Object.assign({}, tasks);
      delete currentTasks[id];
      _saveTask(currentTasks);
      // setTasks(currentTasks);
    };
  
    const _toggleTask = id => {
      const currentTasks = Object.assign({}, tasks);
      currentTasks[id]['completed'] = !currentTasks[id]['completed'];
      _saveTask(currentTasks);
      // setTasks(currentTasks);
    };
  
    const _updateTask = item => {
      const currentTasks = Object.assign({}, tasks);
      currentTasks[item.id] = item;
      _saveTask(currentTasks);
      // setTasks(currentTasks);
    };
  
  ```

  * tasks 값 변경 시마다 저장해야 하므로 setTasks 세터 함수를 이용하는 곳에서 _saveTasks 함수 호출하도록 수정



### 데이터 불러오기

* App.js

  ```react
    const _loadTasks = async () => {
      const loadedTasks = await AsyncStorage.getItem('tasks');
      setTasks(JSON.parse(loadedTasks || '{}'));
    };
  ```

  * 항목을 저장할 때 사용했던 키와 동일한 키로 데이터 불러오고 객체로 변환, tasks에 입력하는 _loadTasks 함수 작성
  * 작성된 _loadTask 함수가 애플리케이션이 로딩되는 단계에서 실행되고, 첫 화면이 나타나기 전에 불러온 항목이 화면에 렌더링되는 것이 자연스러운 모습일 것임
  * Expo에서 제공하는 AppLoading 컴포넌트를 이용하면 이런 작업 쉽게 구현 가능
  * AppLoading 컴포넌트는 특정 조건에서 로딩 화면 유지되도록 하는 기능
  * 렌더링 하기 전 처리해야 하는 작업 수행하는 데 유용하게 사용
  * AppLoading 컴포넌트를 사용해 첫 화면 렌더링되기 전 _.loadTask 함수 호출되도록 해보자

* App.js

  ```react
  ...
  import { AppLoading } from 'expo';
  
  ...
  const [ isReady, setIsReady ] = useState(false);
  
  return (
      isReady ? (
      <ThemeProvider theme={theme}>
              
          ...
      </ThemeProvider> )
      : (
        <AppLoading 
          startAsync={_loadTasks}
          onFinish={() => setIsReady(true)}
          onError={console.error}
        />
      )
    )
  ```

  * useState 이용해 화면의 준비 상태 관리할 isReady 생성

  * isReady 값에 따라 AppLoading 컴포넌트 이용해 로딩 화면 나타나도록 작성

  * AppLoading 컴포넌트에 설정된 값들 다음과 같은 역할

    * startAsync: AppLoading 컴포넌트가 동작하는 동안 실행될 함수
    * onFinish: startAsync가 완료되면 실행할 함수
    * onError: startAsync에서 오류가 발생하면 실행할 함수

  * ```null
    [@RNC/AsyncStorage]: NativeModule: AsyncStorage is null.
    ```

  * 위와 같은 오류 발생

    * node modules 삭제
    * package.json 에서 async stroage 삭제
    * expo install @react-native-async-storage/async-storage 로 재설치
    * npx expo-codemod sdk41-async-storage './**/*' 통해 import 자동 수정

  * 이후 타입 에러 발생

    * import { AppLoading } from 'expo' 가 아니라
    * expo install expo-app-loading 를 실행해 설치한 뒤
    * import AppLoading from 'expo-app-loading' 으로 수정

  * 작동! ㅠㅠ



### 로딩화면 / 아이콘 변경

* app.json 파일 들어가보면 icon 과 splash 확인 할 수 있음

  ```json
  {
    "expo": {
      "name": "todolist",
      "slug": "todolist",
      "version": "1.0.0",
      "orientation": "portrait",
      "icon": "./assets/icon.png",
      "splash": {
        "image": "./assets/splash.png",
        "resizeMode": "contain",
        "backgroundColor": "#ffffff"
      },
      "updates": {
        "fallbackToCacheTimeout": 0
      },
      "assetBundlePatterns": [
        "**/*"
      ],
      "ios": {
        "supportsTablet": true
      },
      "android": {
        "adaptiveIcon": {
          "foregroundImage": "./assets/adaptive-icon.png",
          "backgroundColor": "#FFFFFF"
        }
      },
      "web": {
        "favicon": "./assets/favicon.png"
      }
    }
  }
  
  ```

  * assets 폴더에서 이미지 바꿔줘도 되지만
  * 각 경로 설정 변경을 통해서도 이미지 로고 변경 가능
  * 로딩 화면 이미지는 다양한 기기에 대응하기 위해 1242 x 2436 으로 준비하는 것이 좋음

