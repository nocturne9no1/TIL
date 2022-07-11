# Webpack

이 글은 웹팩 공식문서(https://webpack.js.org/)를 참고하였습니다.

## Concepts

### 웹팩이란 무엇일까?

웹팩은 모던 자바스크립트 어플리케이션을 위한 스태틱 모듈 번들러입니다. 웹팩이 우리들의 어플리케이션을 작업할 때, 내부적으로 하나 혹은 그 이상의 시작 지점과 여러 모듈들의 집합인 의존성 그래프를 만들고 하나 혹은 여러개의 번들로 만듭니다.

우리가 자주 보는

```js
import 이거 from 저기서
```

와 같은 구문에서 from의 위치끼리 엮이고 엮여서 하나의 dependancy graph를 만드는 것입니다.

### 왜 필요할까?

만약 웹팩과 같은 번들러가 없다면 우리는 하나의 html, js 파일에서 작업하게 될 수도 있습니다. 물론 `<script>`와 같은 태그를 이용하여 불러올 수 있습니다.

하지만 더 중요한 점은 **모듈화** 시켜서 작업 공간의 분리를 통해

* 가독성 향상
* 유지보수의 용이함
* 컴포넌트화

등이 가능합니다.



### Core Concepts

#### Entry

Entry Point, 즉 시작지점은 웹팩이 내부 의존성 그래프의 빌딩 시작 지점을 나타냅니다. 웹팩은 시작지점에 직간접적으로 의존하는 다른 모듈들과 라이브러리들을 찾아낼 것입니다.

* Default Value: `./src/index.js`

* 다음과 같이 변경 가능합니다.

  * `webpack.config.js`

  * ```js
    module.exports = {
      entry: './path/to/my/entry/file.js'
    }
    ```

#### Output

output 프로퍼티는 웹팩이 하나 혹은 그 이상의 번들들을 **어디에**/**어떤 이름으로** 저장할 지 지정합니다.

* Default Value: `./dist/main.js`

* 다음과 같이 지정할 수 있습니다.

  * `webpack.config.js`

  * ```js
    const path = require('path');  // file system 접근을 위한 모듈 불러오기
    
    module.exports = {
      entry: './path/to/my/entry/file.js',
      output: {
        path: path.resolve(__dirname, 'dist'),  // 현재 디렉토리에 dist 폴더 붙인 경로
        filename: 'my-first-wepack.bundle.js'
      }
    }
    ```

#### Loaders

웹팩은 자바스크립트나 JSON 파일만 읽을 수 있습니다.

`Loaders`는

* 웹팩이 다른 타입의 파일을 작업할 수 있게 해주고 
* 읽을 수 없던 파일을 우리들의 어플리케이션에 알맞은 유효한 모듈로 바꾸고
* 의존성 그래프에 추가해줍니다.

`Loaders`는 `webpack configuration`에서 두 가지 프로퍼티를 가집니다.

* `test`: 어떤 파일(들)이 바뀌어야 하는지
* `use`: 로더가 trasforming 하는데 사용됨을 나타냄

다음과 같이 `webpack.config.js`에 등록됩니다.

```js
module.exports = {
  ...
  module: {
    rules: [{ test: /\.txt$/, use: 'raw-loader' }],
  }
}
```

위와 같은 환경 설정은 다음을 의미합니다.

> 웹팩 컴파일러야, 니가 `require()` 이나 `import` 구문 보다가 '.txt' 파일을 발견하면 `raw-loader` 써가지고 번들링 하기전에 추가해줭

#### Plugins

