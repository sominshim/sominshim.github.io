---
layout: post
title: "[git] Git ignore 사용법"
date: 2021-07-14 22:00:0
background: '/img/posts/02.jpg'
---

## .gitignore 이란?
commit하고 싶지 않은 파일들을 gitignore파일을 이용하여 숨길 수 있다.

예를 들어, 
- 보안상의 위험이 있는 파일
- 프로젝트와 관련없는 파일
- 용량이 너무 커서 제외해야 되는 파일

### .gitignore 사용법
1. git의 관리 하에 있는 project 폴더에 .gitignore 파일을 만든다.

2. .gitignore 파일에 올리고 싶지 않은 파일 이름을 작성한다.
    - 특정 파일을 무시하고 싶을 경우
        ```
        raw_data.csv
        intorduction.pdf
        ```

    - 해당 확장자 파일 전부를 무시하고 싶을 경우
        ```
        *.pdf
        *.dll
        ```

    - 해당 경로의 파일 전부를 무시하고 싶을 경우
        ```
        target/
        fold_name/
        ```
---
### 사용 도중에 .gitignore 파일을 만든 경우

    ```
    git rm -r --cached .
    git add .
    git commit -m "git ignore add"
    git push
    ```

