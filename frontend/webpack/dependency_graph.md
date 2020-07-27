# webpack

## Dependency Graph
- 한개의 파일이 다른 것에 의존할 때마다, 웹팩은 이것을 dependency로 여긴다.
- 이를 통해 웹팩은 이미지들이나 웹 폰트 같은 non-code assets을 가질 수 있게 되고, 이러한 non-code assets을 어플리케이션의 dependencies로 제공할 수 있다.
- 웹팩이 어플리케이션을 처리할 때는 커맨드라인 또는 configuration file에 정의된 모듈 리스트에서 시작한다.
- 이 entry points부터 시작해서 웹팩은 어플리케이션에 필요한 모든 모듈들을 포함한 dependency graph를 재귀적으로 만든 다음, 이러한 모든 모듈을 브라우저에 로드할 소수의 번들로 묶는다.


***
