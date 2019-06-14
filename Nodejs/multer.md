# Multer

파일 업로드시 사용되는 nodejs 의 미들웨어.

## 설치

Yarn

```bash
    $ yarn add multer
```

NPM

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
    // 파일 저장 위치
    storage: diskStorage({
        // 경로
        destination: function(req, file, cb) {
            cb(null, '/files');
        },
        // 저장될 파일 이름
        filename: function(req, file, cb){
            cb(null, file.originalname);
        }
    }),
    limits: { fileSize: 30 * 1024 * 1024 }
}).any();
app.post(
    '/files',
    function (req, res, next) {
            upload(req, res, function(err) {
                // catch error
                if (err) {
                    logger.error('[Multer][File] -> ' + err);
                    res.status(500).send(err);
                    return;
                }
                else{
                    next();
                }
            })
        },
    },
    // next middleware or endpoint
});
```

storage 필드는 diskStorage 지정시 destination 필드의 경로에 filename 필드의 파일명으로 저장한다.
storage 필드를 memoryStorage로 지정시 req.files.buffer로 파일 정보가 반환 된다.

## GridFS 와 사용

[multer-gridfs-storage](https://www.npmjs.com/package/multer-gridfs-storage) 을 통해 쉽게 GridFS와 사용 가능하다.

```javascript
config = {
    DB_URL: '<mongodb url>',
}

// storage
const storage = new GridFSStorage({
    url: config.DB_URL,
    file: (req, file) => ({
        bucketName: config.FILE_BUCKET_NAME,
        filename: file.originalname,
    })
});

const upload = multer({
    storage: storage,
}).any();

app.post(
    '/files',
    function (req, res, next) {
            upload(req, res, function(err) {
                // catch error
                if (err) {
                    logger.error('[Multer][File] -> ' + err);
                    res.status(500).send(err);
                    return;
                }
                else{
                    next();
                }
            })
        },
    },
    function (req, res, next) {
        // next middleware or endpoint
    }
});
```

req.files 내용

```json
{
        "fieldname": "test3",
        "originalname": "jdiskreport-1_4_1.zip",
        "encoding": "7bit",
        "mimetype": "application/x-zip-compressed",
        "id": "5d0354e05986fd43ac67a835",
        "filename": "jdiskreport-1_4_1.zip",
        "metadata": null,
        "chunkSize": 261120,
        "size": 864613,
        "md5": "9380a6ba68bd21e0f09b58297eb5a44a",
        "uploadDate": "2019-06-14T08:03:45.556Z",
        "contentType": "application/x-zip-compressed"
}
```

참조 :

1. <https://github.com/expressjs/multer>
2. <https://www.npmjs.com/package/multer-gridfs-storage>
