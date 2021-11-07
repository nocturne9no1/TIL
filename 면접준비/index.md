# 직무 면접 준비

* 이곳에 목록을 정리하고 추후 하나씩 markdown으로 정리한 뒤 블로그에 올린다
* 목록에는 점점 추가 될 수 있고 완료 한 것은 취소선 처리 할 것이다.

## Javascript

### 몹시 몹시 중요

#### 호이스팅에 대해 설명하시오

https://gmlwjd9405.github.io/2019/04/22/javascript-hoisting.html

#### 클로저는 무엇인가? 원리와 왜 사용하는가?

https://hyunseob.github.io/2016/08/30/javascript-closure/

### 몹시 중요

#### this의 용법을 아는대로 설명하시오

https://poiemaweb.com/js-this

#### Javascript는 어떤 언어인가?

* 싱글 스레드 언어

##### 하지만 실제 사용시에는 멀티 스레드처럼 사용하는데 어떻게 사용하나?

##### 비동기적으로 실행이 되는 것을 동기적으로 코딩하는 방법이 있나?

https://realmojo.tistory.com/109

https://boxfoxs.tistory.com/294

#### Event Loop 에 대해 알고 있나요?

https://im-developer.tistory.com/113

#### Event Bubbling 에 대해 설명해주세요

##### 이벤트 버블링은 기본적으로 child -> parent 인데 반대로 구현하는 법은?

##### 이벤트 버블링을 막기위한 방법은?

##### 이벤트 버블링을 잘 활용하면 어떻게 사용할 수 있을까요?

https://joshua1988.github.io/web-development/javascript/event-propagation-delegation/

#### TypeScript에 대해 사용해 본 적이 있나요? 어떤지 말씀해주세용

https://hyunseob.github.io/2018/08/12/do-you-need-to-use-ts/

#### 실행 문맥에 대해 설명해 주세요

https://poiemaweb.com/js-execution-context

### 중요

#### HTML이 렌더링 중에 Javascript 가 실행되면 렌더링이 멈추는데 그 이유는?

https://webclub.tistory.com/630

https://realmojo.tistory.com/96

#### 현재 Javascript 프레임워크를 사용하는 것과 그 선택을 한 이유?

##### 프로젝트를 진행할 때 어떤 Javascript 프레임워크를 선택할 것인가? 그 이유는?

##### 최근 사용되는 Javascript 프레임워크에 대해 차이점과 장단점은? 언제 어떻게 사용해야 하는가?

* 이 질문은 엔지니어마다 주관적
* 제대로 숙고하여 답변해야 함

https://www.popit.kr/%EB%B2%88%EC%97%AD%EA%B8%80-react-vs-angular-%EB%91%98-%EC%A4%91-%EC%96%B4%EB%96%A4-%EA%B2%83%EC%9D%B4-%EB%8B%B9%EC%8B%A0%EC%9D%98-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%97%90-%EC%95%8C%EB%A7%9E/

https://brunch.co.kr/@hee072794/112

#### require와 import 의 차이점

https://blueshw.github.io/2017/05/16/ES-require-vs-import/

#### Javascript 성능 최적화를 위해 어떤 것을 적용해 보았나요?

https://engineering.huiseoul.com/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%9E%91%EB%8F%99%ED%95%98%EB%8A%94%EA%B0%80-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B4%80%EB%A6%AC-4%EA%B0%80%EC%A7%80-%ED%9D%94%ED%95%9C-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%88%84%EC%88%98-%EB%8C%80%EC%B2%98%EB%B2%95-5b0d217d788d?gi=74c940ef3d22

https://itstory.tk/entry/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%97%90%EC%84%9C-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%88%84%EC%88%98%EC%9D%98-4%EA%B0%80%EC%A7%80-%ED%98%95%ED%83%9C

#### Vue & React

##### Vue 와 React의 차이점은?

##### Vue 혹은 React를 사용해봤다면 상태관리는 어떻게 구현하였나요?

##### (Vue면접관) 라이프 사이클에 대해 설명해주세요

##### Vue에서 양방향 데이터가 일어나는 원리에 대해 말씀해주세요

https://medium.com/@erwinousy/%EB%82%9C-react%EC%99%80-vue%EC%97%90%EC%84%9C-%EC%99%84%EC%A0%84%ED%9E%88-%EA%B0%99%EC%9D%80-%EC%95%B1%EC%9D%84-%EB%A7%8C%EB%93%A4%EC%97%88%EB%8B%A4-%EC%9D%B4%EA%B2%83%EC%9D%80-%EA%B7%B8-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%B4%EB%8B%A4-5cffcbfe287f

https://ko.classicfoxvalley.com/collate/redux-vs-vuex-for-state-management-in-vue-js-d57692/

https://medium.com/witinweb/vue-js-%EB%9D%BC%EC%9D%B4%ED%94%84%EC%82%AC%EC%9D%B4%ED%81%B4-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-7780cdd97dd4

https://kr.vuejs.org/v2/guide/reactivity.html

#### 무작위 데이터에 대해 테스트는 어떻게 진행하나요?

https://www.json-generator.com/

#### ES6에서 Arrow 함수를 언제 쓰나요? 왜 쓰나요?

https://poiemaweb.com/es6-arrow-function

#### `let` `var` `const`  차이점

https://gist.github.com/LeoHeo/7c2a2a6dbcf80becaaa1e61e90091e5d

## Web 전반

### 몹시 몹시 중요

#### 브라우저 렌더링 원리

##### 홈페이지가 사용자에게 보이는 순서에 대해 설명하시오

https://d2.naver.com/helloworld/59361

##### 검색창에 구글을 쳤을 때 어떻게 되는가요?

https://www.linkedin.com/pulse/what-happens-when-you-type-googlecom-any-other-url-buitrago-vargas

#### GET, POST가 어떻게 다르게 쓰이는가?

https://www.w3schools.com/tags/ref_httpmethods.asp

### 몹시 중요

#### 브라우저 저장소에 대해 차이점을 설명하시오

https://velog.io/@ejchaid/localstorage-sessionstorage-cookie%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90

*  (LocalStorage, SessionStorage, Cookie)

#### Restful API에 대해서 아는대로 설명하시오

https://javaplant.tistory.com/18

* GET, PUT, POST, PATCH, OPTION, DELETE

### 중요

#### SPA와 서버사이드 렌더링의 차이점은?

https://goodgid.github.io/Server-Side-Rendering-and-Client-Side-Rendering/

#### CORS를 대처하는 방법과 우회하는 방법

https://brunch.co.kr/@adrenalinee31/1

#### MVVM 모델에 대해 설명해 주세요

https://beomy.tistory.com/43

### 보통

#### HTTP 0.9/1.0 차이를 설명하시오

https://medium.com/platform-engineer/evolution-of-http-69cfe6531ba0

## HTML

## CSS

### 몹시 몹시 중요

#### CSS 에서 margin과 padding에 대해 설명하시오

#### position을 어떻게 사용하는지에 설명하시오

### 몹시 중요

### 중요

#### SASS, SCSS를 사용해 본적이 있나요? 기존 CSS와 비교할 때 어떤면이 좋은가요?

https://heropy.blog/2018/01/31/sass/#sasswa-scssneun-caijeomeun-mweongayo

### 보통

#### CSS에는 Box-model 이라는 것이 있다. 이때 width 값을 차지하는 크기는 어떻게 되는가?

https://www.w3schools.com/css/css_boxmodel.asp



## ETC.

#### 이진트리에 대해 말하고 종류는 어떻게 되는가? 실제 적용해본 경험은?

https://ratsgo.github.io/data%20structure&algorithm/2017/10/21/tree/

#### Git을 사용해본 적이 있는가? 사용했다면 어떤식으로 사용했는지 말씀해주세요

https://woowabros.github.io/experience/2017/10/30/baemin-mobile-git-branch-strategy.html

#### 협업에 대해 어떻게 생각하나요?

#### 스켈레톤 UI에 대해 적용해본 적이 있는가?

https://www.sitepoint.com/how-to-speed-up-your-ux-with-skeleton-screens/

https://vuetifyjs.com/en/components/skeleton-loaders/

#### 프론트엔드 주제를 가지고 발표해야 한다면 바로 가능한게 있나요?



