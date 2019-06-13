# Multer

파일 업로드시 사용되는 nodejs 의 미들웨어.

## 설치

1. Yarn

   ```bash
   $ yarn add multer
   ```

2. NPM

    ```bash
   $ npm install multer
    ```

## 기본 사용법

파일전송을 위해서 `content-type` 은 `multipart/form-data` 로 한다.

```javascript
const express = require('express');
const multer = require('multer');

const app = express();

const upload = multer({
    storage: diskStorage({
        destination: function(req, file, cb) {
            cb(null, '/files');
        },
        filename: function(req, file, cb){
            cb(null, originalname);
        }
    })
});
app.post('/files', upload.any(), function(req, res, next){
    // next middleware
});
```

storage 필드는 diskStorage 지정시 destination 필드의 경로에 filename 필드의 파일명으로 저장한다.

storage 필드를 memoryStorage로 지정시 req.files.buffer로 파일 정보가 반환 된다.
