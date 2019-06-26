# Git Branch

## 리모트 브랜치 생성

1. 로컬에서 생성

    ```git
    git checkout -b <brnach name>
    ```

2. 리모트와 함께

    ```git
    # 생성
    git push origin <branch name>
    # 원격과 로컬의 연결
    git branch --set-upstream-to origin/<branch name>
    ```
