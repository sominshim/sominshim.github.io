---
layout: single
title:  "How to mirror Gitlab to GitHub"
categories: [Git]
tags: [Git]

toc: true
toc_sticky: true
toc_label: "목차"

---



"미러링한다"는 말은 "복사한다"는 의미이다. 

예를 들어 깃랩에 있는 레파지토리를 깃허브로 미러링하면 깃랩의 브랜치, 태그 그리고 커밋까지 깃허브 레파지토리에 그대로 복사된다. 

잔디도 심어진다 !!

<br/>

세 가지 미러링 방법이 있다.

1. **Push**: GitLab → 다른 위치
2. **Pull**: 다른 위치 → GitLab
3. **Bidirectional**: GitLab ↔︎ 다른 위치, 충돌이 발생할 수 있음.

<br/>

### Mirror a repository when:

- GitLab 프로젝트 사본을 다른 위치에 남겨두고 싶을 때, GitLab 레파지토리를 **Push mirror**한다.
-  GitLab 프로젝트는 비공개이지만 일부 구성 요소는 공개하여 공유할 수 있다. 기본 레파지토리를 **Push mirror**하고 공개하려는 부분만 Push mirror한다. 이는 오픈 소스 커뮤니티에 기여하고, 프로젝트의 민감한 부분을 보호할 수 있다.
- 프로젝트의 표준 버전이 다른 곳에 있을 때 **Pull mirror** 한다. 모든 외부 소스와 레파지토리를 가져와 GitLab에서 사용할 수 있게 된다.

<br/>

오늘은 **Push mirror**하는 방법에 대해 알아보자.

<br/>

>  미러링 조건

- 프로젝트 관리자여야 한다.
- mirror가 ssh://로 연결되는 경우, 서버에서 호스트 키를 감지할 수 있거나 로컬 복사본 키가 있어야 한다.

<br/>

## on GitHub

### 1. Create a repository on GitHub

해당 repository에 미러링을 할 것이다. 

### 2. Access token

[GitHub Docs](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) 를 참고하여 엑세스 토큰을 생성하고 복사해둔다.

<br/>

## go to GitLab

### 1. **미러링할 프로젝트**의 Settings > Repository 

<img src="../../images/2022-03-22-How to mirror gitlab to github/스크린샷 2022-03-22 오후 3.00.04-7936930.png" alt="스크린샷 2022-03-22 오후 3.00.04" style="zoom:50%;" />

### 2. Mirroring repositories 의 ```Expand``` 버튼을 클릭한다.

<img src="../../images/2022-03-22-How to mirror gitlab to github/스크린샷 2022-03-22 오후 3.01.13.png" alt="스크린샷 2022-03-22 오후 3.01.13" style="zoom:33%;" />

### 3. Git repository URL, Password 입력하면 끝!

<img src="../../images/2022-03-22-How to mirror gitlab to github/kdt-gitlab.elice.io_ai_track_class_03_data_project_003-part3-ottservice_team7_project-template_-_settings_repository (1)-7936941.png" alt="kdt-gitlab.elice.io_ai_track_class_03_data_project_003-part3-ottservice_team7_project-template_-_settings_repository (1)" style="zoom:33%;" />

- Git repository URL 입력  

  ```https://gitlab.company.com//<username>//<project-name>.git```

  → ```https://<username>@gitlab.company.com//<username>//<project-name>.git```

  ```https://``` 뒤에 ```<username>@``` 추가해야 한다.

- Password 칸에 미리 복사해둔 엑세스 토큰 입력  

<br/>



## Reference

[GitLab Docs](https://docs.gitlab.com/ee/user/project/repository/mirror/)