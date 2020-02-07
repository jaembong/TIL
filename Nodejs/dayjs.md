# dayjs

momentjs 의 경량화 버전

1. install

    ```bash
    $ yarn add dayjs
    ```

2. 기본 사용

    1. 객체 생성

        ```javascript
        const dayjs = require('dayjs');
        let date = dayjs(new Date(), 'YYYY-MM-DD');
        ```

    2. diff

        ```javascript
        let dateA = dayjs('2019-07-03', 'YYYY-MM-DD');
        let dateB = dayjs(new Date(), 'YYYY-MM-DD');
        let diff = dateA.diff(dateB, 'day');
        console.log(diff);
        ```
