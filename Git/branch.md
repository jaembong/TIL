# Git Branch

## 리모트 브랜치 생성

1. 로컬에서 생성

    ```bash
    git checkout -b <brnach name>
    ```

2. 리모트와 함께

    ```bash
    # 생성
    git push origin <branch name>
    # 원격과 로컬의 연결
    git branch --set-upstream-to origin/<branch name>
    ```

3. Rename

    ```bash
    # 현재 브랜치 이름 변경(로컬)
    git branch -m <new name>

    # 다른 브랜치 이름 변경 (로컬)
    git branch -m <old name> <new name>

    # 원격 브랜치 이름 변경
    git push origin :<old name> <new name>

    # 이후 로컬과 원격 연결
    git push origin -u <new name>
    ```

    Reference: <https://multiplestates.wordpress.com/2015/02/05/rename-a-local-and-remote-branch-in-git/>