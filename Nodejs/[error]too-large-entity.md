# Rquest entity too large 오류

## 개요

nodejs 서버 운영중 발생 한 오류다. 파일이나 폼 데이터가 express parser 에서 설정된 크기보다 클경우 발생한다. (디폴트1mb)

## 해결

App의 parser limit을 늘려준다.

```javascript
// index.js
app.use(express.json({limit: '50mb'}));
app.use(express.urlencoded({limit: '50mb'}));
```

참고: 

https://stackoverflow.com/questions/19917401/error-request-entity-too-large
