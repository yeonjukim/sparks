# webpack
[document](https://webpack.js.org/concepts/)

## concepts
- 모던 자바스크립트 어플리케이션을 위한 static module bundler(정적 모듈 번들러)
- 웹팩이 어플리케이션을 처리할 때, 내부적으로 프로젝트에서 필요로 하는 모든 모듈들을 매핑하는 dependency graph를 구축하고 하나 이상의 번들을 생성한다.

## 웹팩이 필요한 이유
- 너무 많은 자바스크립트 파일을 로드할 경우 네트워크 병목현상이 발생한다.
- 복잡한 어플리케이션을 개발할 때 script가 많아지면 관리하기 힘들어진다: 모듈화 필요

## 장점
- 여러 파일의 자바스크립트 코드를 압축하여 최적화 할 수 있기 때문에 로딩에 대한 네트워크 비용이 감소한다.
- 모듈 단위로 개발 가능, 가독성이 좋고 유지보수가 쉽다.
- 라이브러리 종속 순서를 신경쓰지 않아도 된다.
- babel-loader를 통해 최신 자바스크립트 문법을 지원하지 않는 브라우저에서 사용할 수 있는 코드로 쉽게 변환시켜 준다.

## 시작하기
- Node.js가 설치된 환경에서 실행된다.
- npm(node package manager)으로 설치할 수 있다.

__1. 프로젝트 디렉토리 생성 및 package.json 파일 생성__
  ```
  mkdir webpack-demo
  cd webpack-demo
  npm init -y
  ```
__2. webpack-cli(커맨드라인에서 웹팩을 실행할 수 있는 툴) 설치__
  ```
  npm install webpack webpack-cli --save-dev
  ```
  - 웹팩 프로젝트 구조
  ```
  webpack-demo
  |-- package.json
  |-- index.html
  |-- /src
      |-- index.js
  ```

__3. indxe.js, index.html 파일 작성__
  - src/index.js
  ```
    function component() {
    const element = document.createElement('div');

      // Lodash, currently included via a script, is required for this line to work
      element.innerHTML = _.join(['Hello', 'webpack'], ' ');

      return element;
    }

    document.body.appendChild(component());
  ```
  - index.html
  ```
  <!doctype html>
  <html>
    <head>
      <title>Getting Started</title>
      <script src="https://unpkg.com/lodash@4.16.6"></script>
    </head>
    <body>
      <script src="./src/index.js"></script>
    </body>
  </html>
  ```

__4. package.json 파일 수정__
  - main 속성을 삭제하고 private 속성 추가
```
{
      "name": "webpack-demo",
      "version": "1.0.0",
      "description": "",
      "private": true,
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "keywords": [],
      "author": "",
      "license": "ISC",
      "devDependencies": {
        "webpack": "^4.20.2",
        "webpack-cli": "^3.1.2"
      },
      "dependencies": {}
}
```

***
