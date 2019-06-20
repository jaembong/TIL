# Electron + React desktop app을 위한 Boiler Plate

리눅스에서 데스크톱 앱을 개발할 일이 생겨 알아보다 `electron`을 알게 되었다. 그리고 UI개발에 리액트를 이용할수 있다는것을 알게 되고 `electron-react-boilerplate`를 사용해보았다.

1. 설치

```bash
$ git clone --depth 1 --single-branch --branch master https://github.com/electron-react-boilerplate/electron-react-boilerplate.git your-project-name
```

코드를 클론해 클론한 위치에서 앱을 개발한다.

```
$ yarn
```

dependency들을 설치한다.

2. 개발 모드

```bash
$ yarn dev
```

브라우저로 앱을 구동해 볼수있다. 크롬 개발자툴 이용가능

3. Package

```bash
$ yarn package
```

실행환경에 맞게 빌드 및 패키징을 한다. 윈도우 같은 경우에는 exe로 출력되고, 우분투에서는 appimage 및 deb으로 출력되었다.

참고:

https://github.com/electron-react-boilerplate/electron-react-boilerplate
