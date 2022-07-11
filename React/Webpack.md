# Webpack

이 글은 웹팩 공식문서(https://webpack.js.org/)를 간단하게 번역하였습니다.

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



## Core Concepts

### Entry

Entry Point, 즉 시작지점은 웹팩이 내부 의존성 그래프의 빌딩 시작 지점을 나타냅니다. 웹팩은 시작지점에 직간접적으로 의존하는 다른 모듈들과 라이브러리들을 찾아낼 것입니다.

* Default Value: `./src/index.js`

* 다음과 같이 변경 가능합니다.

  * `webpack.config.js`

  * ```js
    module.exports = {
      entry: './path/to/my/entry/file.js'
    }
    ```

### Output

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

### Loaders

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

### Plugins

`loaders`가 모듈들의 타입을 변경시키는 동안, `plugins`는 번들 최적화/에셋 관리/환경 변수 주입 등의 tasks의 넓은 범위에 영향을 줄 수 있습니다.

`plugins`를 사용하기 위해, `webpack.config.js`의 `plugins` 배열에 해당 `pulgin`을 추가하고 `require()` 해야 합니다. 대부분의 `plugins`는 `option`을 통해 사용자화 할 수 있습니다. `plugins`는 환경 설정에서 다른 목적들로 인해 여러번 사용될 수 있기 때문에, `new` 연산자를 통해 인스턴스를 생성해야 합니다.

```js
const HtmlWebpackPlugin = require('html-webpack-plugin');
const webpack = require('webpack');  // 빌트인 plugins 접근 위해서

module.exports = {
  ...
  plugins: [new HtmlWebpackPlugin({ template: './src/index.html' })],
};
```

### Mode

`Mode` 인자를 `development`/`production`/`none`으로 세팅함으로써, 각 환경에 해당하는 웹팩 빌트인 최적화를 사용할 수 있습니다.

* Default Value: `production`

```js
moduel.exports = {
  mode: 'production',
};
```

### Browser Compatibility

웹팩은 ES5 버전 이상의 모든 브라우저를 지원합니다(IE8 이하 는 지원 ㄴㄴ). 웹팩은 `import()`와 `require.ensure()`구문을 위해 `Promise`가 필요합니다. 만약 구시대의 브라우저에 대한 지원이 필요하다면 `polyfill`을 사용해야 합니다.

### Enviroment

웹팩 ver.5 는 Node.js version 10.13.0+ 에서 실행됩니다.

























