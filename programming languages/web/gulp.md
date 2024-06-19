# gulp

* 참고링크
  * https://gulpjs.com/docs/en/getting-started/quick-start



## Quick Start

* node, npm, npx 설치해야함

* ```bash
  npx mkdirp my-project
  ```

* 폴더안에서 `npm init`

* ```bash
  This utility will walk you through creating a package.json file.
  It only covers the most common items, and tries to guess sensible defaults.
  
  See `npm help init` for definitive documentation on these fields
  and exactly what they do.
  
  Use `npm install <pkg>` afterwards to install a package and
  save it as a dependency in the package.json file.
  
  Press ^C at any time to quit.
  package name: (gulp-p) practice
  version: (1.0.0)
  description: gulp practice
  entry point: (index.js)
  test command: test
  git repository:
  keywords: gulp
  author: hk.kong
  license: (ISC)
  ```

* 위와 같이 나옴 하나씩 입력

* install gulp

  * ```bash
    npm install --save-dev gulp
    ```

  * verify my gulp version

  * ```bash
    gulp --version
    // CLI version: 2.3.0
    // Local version: 4.0.2
    ```

* create a gulpfile

  * create a file named `gulpfile.js` in my project root

  * and write contents below

  * ```js
    function defaultTask(cb) {
      // place code for your default task here
      cb();
    }
    
    exports.default = defaultTask
    ```

* test

  * run gulp command

  * ```bash
    gulp
    ```

  * ```bash
    $ gulp
    [21:00:13] Using gulpfile E:\PT\gulp-p\gulpfile.js
    [21:00:13] Starting 'default'...
    [21:00:13] Finished 'default' after 1.6 ms
    ```



## JavaScript and Gulpfiles

* gulp는 내가 알고 있던 javascript 지식을 쓰게함
* 몇몇 유틸리티는 커맨드라인이나 파일시스템에 접근하는데도 자바스크립트 사용가능
  * 내가 알기로는 JS는 보안상의 이유로 원래 파일시스템 접근 허용 ㄴㄴ

### Gulpfile explained

* gulpfile은 내 프로젝트 폴더에 `gulpfile.js`로 명명된 것
  * 이건 `gulp`커맨드 입력하면 알라서 실행됨
  * 이 파일안에서, 나는 gulp API (`src()`, `dest()`, `series()`, `parallel()`) 볼 수 있음
  * 바닐라 자스나 노드 모듈도 사용가능
  * 모든 exported functions는 gulp's task system에 등록됨

### Transpilation

* 난 걸프를 transilation 언어로도 쓸 수 있음
  * TS 나 Babel 같은것들
  * `gulpfile.js` 에서 extension 바꿔야함
  * 궁금하면 더 찾아보라는데 사이트 링크 박살남

### Splitting a gulpfile

* 많은 유저들이 모든 로직을 걸프파일에 넣는걸로 시작함
  * 이게 너무 크다? 각 파일로 분할 가능
* 각 작업은 각 파일로 분리 가능
  * 그런다음 gulpfile에다가 합치기위해 `import`
  * 구조적으로 유지하도록하고 독립적으로 각 작업을 테스트할 수 있음 조건에 따라
* node's moudle resolution은 내가 `gulpfile.js`를 `index.js`를 포함한 `gulpfile.js`로 명명된 폴더와 대체될 수 있게한다(????)
  * 이 폴더는 작업들을 위한 개개의 모듈을 담을 수 있다.
  * 내가 만일 trnaspiler를 쓰고 있다면, 폴더와 파일이름을 따라서 지어라
  * 뭔 말인지 모루겠네



## Creating Tasks

* 각 gulp 작업은 js 비동기 함수임
  * a function that accepts an error - 에러를 수반할 수도 있는??
  * 첫 콜백/반환 stream, promise, event emitter, child process, obsevable...
  * 몇몇 플랫폼의 제한때문에 동기 작업은 지원 안됨



### Exporting

* 작업은 `public` 과 `private`로 나뉨
  * Public tasks
    * gulpfile 로 부터 exported
    * gulp command로 run 가능
  * Private tasks
    * `series()` or `parallel()` composition의 부분으로 내부적으로 자주 쓰임
    * ????
* private task는 다른 작업과 비슷하게 보임
  * 하지만 end-user(최종적으로 보는 유저인가)는 독립적으로 실행 불가
  * task를 pulicg하게 등록하기위해 gulpfile을 export

```js
const { series } = require('gulp');

// The `clean` function is not exported so it can be considered a private task.
// It can still be used within the `series()` composition.
function clean(cb) {
  // body omitted
  cb();
}

// The `build` function is exported so it is public and can be run with the `gulp` command.
// It can also be used within the `series()` composition.
function build(cb) {
  // body omitted
  cb();
}

exports.build = build;
exports.default = series(clean, build);
```

* clean 함수는 exported 되지 않아서 private task로 간주됨
  * 여전히 `series()` composition에서 쓰임
* build 함수는 exported 됨, 따라서 이건 pulbic하고 `gulp` 커맨드로 실행 가능
  * 이것도 `series()` composition 내부에서 쓰임
  * ????