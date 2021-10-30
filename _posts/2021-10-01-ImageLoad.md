---
layout: single
title:  "GitBlog에 이미지 간단하게 업로드하는 방법"
categories: [GitHub Pages]
tags: [Blog]

# toc: true
# toc_sticky: true
# toc_label: "Contents"

# author_profile: false
# sidebar:
#     nav: "docs"
---



## **Typora 문서 편집기 이용**

- **markdown 문법이 적용**된 글을 실시간으로 볼 수 있다.

- 이미지를 **drag and drop** 하면 자동으로 images 폴더에 이미지 파일이 복사된다.

먼저, [Typora](https://typora.io/) 사이트에서 프로그램을 설치한다.


<center>서식 → 이미지 → 전역 이미지 설정</center>

<center><img src="../../images/2021-10-01-ImageLoad/스크린샷 2021-10-29 오후 2.26.58.png" alt="screen shot image" /></center>

Copy image to custom folder 선택 후,
경로를 **"../images/${filename}"**로 설정한다.

그리고 원하는 위치에 이미지를 복사 붙여넣기 또는 drag and drop 한다.

![스크린샷 2021-10-29 오후 2.39.10](../../images/2021-10-01-ImageLoad/스크린샷 2021-10-29 오후 2.39.10.png)

위와 같이 images 폴더에 해당 포스트 이름으로 이미지 폴더가 생성되고, 그 안에 이미지가 자동으로 업로드 되는 것을 확인할 수 있다.

이제부터 이미지를 삽입할 때 일일이 저장하고 경로 설정하는 번거로움은 덜었다.

