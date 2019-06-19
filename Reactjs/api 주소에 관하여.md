# API 주소에 관하여

개발중이던 앱을 localhost에서 다른 PC로 옮겨서 시험 가동중에 알게된 사실.

개발중이던 앱은 React Client <-> Nodejs Server 형태였다. 그리고 두 앱은 같은 위치에 있었다.

이에 React app 에서 서버로 요청을 보낼때 API주소를 입력하는데 `'localhost:<port>'` 의 형태로 설정해뒀었다.

개발중인 PC에서 사용시는 문제가 없었으나 다른 PC나 서버에 있는 경우 위의 `localhost`는 리액트 앱이 실행중인 컴퓨터를 참조하게 되고 결국 원하는 Nodejs 서버에 요청을 보내지 못하게 된다.

급한대로 `localhost`를 서버가 구동중인 PC의 IP로 변경 하여 해결했다.
