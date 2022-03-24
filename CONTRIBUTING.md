# CONTRIBUTING

## 블로그 포스트를 작성할 사람

1. 사전 설정

    1. 이 repository를 본인의 계정으로 fork해주세요! 저장소 우측 상단에 fork 버튼이 있습니다.

    2. fork한 repository를 본인의 컴퓨터로 clone하세요

    3. (선택) 포스트 작성을 위한 별도의 브랜치를 생성하세요

        ```bash
        ex) git checkout -b post/leemir
        ```

2. 블로그 포스트 작성하기

    1. `_posts` 폴더에 포스트를 markdown형식으로 작성해주세요.
    2. 포스트 상단의 속성을 설정해주세요. (영어로 된 부분은 그대로 두고 한글 부분을 변경하시면 됩니다! 이해가 안가시면 다른 분들의 포스트를 참고해주세요.)
        * `layout: post`
        * `title: 포스트 제목`
        * `authors: [작성자명]`
        * `tags: [태그1, 태그2, 태그3]`
        * `image: 포스트 커버 이미지`
        * `featured: true`
    3. 포스트 작성 중, 이미지에 캡션 달기
        1. 다음과 같이 작성해주세요(띄어쓰기 주의)

        ```markdown
            ![image](../assets/images/xxxx/xxxx)
            *캡션으로 달고 싶은 메시지*
        ```

    4. VS Code 확장(`Ctrl`+`Shift`+`x`)에서 `markdownlint`를 설치해 규칙에 맞게 작성했는지 확인해주세요.

3. 작성한 포스트 Local Server에서 확인하기 (필수 아님)

    * 작성한 포스트가 실제 블로그에서 어떻게 보여지는지 확인하고 싶다면 아래의 순서대로 진행해주세요.
    1. Local 환경에서 블로그를 실행하려면 `Ruby`를 설치해야 합니다. `ruby -v`,`gem -v`, `gcc -v`, `make -v`등의 명령어로 환경이 갖추어졌는지 확인해주세요.
        * `Ruby` 등의 설치가 필요할 경우 [Jekyll 공식 문서](https://jekyllrb.comdocs/installation/)를 참고해 설치해주세요.
        * `Jekyll`은 `Ruby Gem`으로써, Github에서 제공하는 Github Pages 호스팅에 적합한 static site generator입니다. 
    2. VS Code에서 터미널을 열어주세요.
    3. `bundler install`을 입력해주세요.
    4. `bundler exec jekyll serve`를 입력하면 Local Server가 시작됩니다. 터미널에표시되는 `Server address`로 접속해주세요.

4. 원격 저장소로 push

    * 처음에 fork했던 본인의 원격 저장소로 push합니다. 별도의 설정을 안했다면 `origin`으로 되어있습니다.

      ```bash
      ex) git push origin [브랜치 이름]
      ```

5. PR을 작성해주세요!

    * ***이 레포지토리의 master 브랜치로 Pull Request를 날려주세요!***
    * (주의) 상위 레포지토리인 [wowthemesnet](https://github.com/wowthemesnet)/**mediumish-theme-jekyll** 로 날리시면 큰일납니다.
    * PR이 블로그팀에 의해 merge되기 전까지는 브랜치를 따로 옮겨서 작업하지 않는 이상 `push`만 하면 알아서 현재 PR에 추가되니, 블로그팀이 수정 요청을 할 경우 수정 내용을 `commit` 후, `push`까지 해주시면 됩니다.

6. 동기화해주세요!

    * fork한 지 오래됐다면 PR을 날릴 때 conflict가 일어날 가능성이 높습니다. 항상 포스트를 작성하기 전에는 pull 받아주세요!

      ```bash
      ex) git pull upstream master

      (만약, git remote -v를 입력했는데 upstream이 없다면 아래 명령어를 입력해주세요)

      git remote add -t master upstream https://github.com/GDSC-University-of-Seoul/gdsc-university-of-seoul.github.io.git
      ```

      ​

## 블로그 포스팅 수식 사용하는 방법

md파일 작성 시 use_math:true를 추가해주세요!

[수식 참고 사이트](https://ko.wikipedia.org/wiki/%EC%9C%84%ED%82%A4%EB%B0%B1%EA%B3%BC:TeX_%EB%AC%B8%EB%B2%95#%EA%B5%AC%EB%B3%84_%EB%B6%80%ED%98%B8)

```
---
layout: post
title: 포스팅 제목
authors: [github 아이디]
tags: 
image: 
featured: true
use_math: true
---
```

## 블로그 author 추가하는 방법(블로그팀만)

1. `_data` 폴더에 `author.yml`을 수정해주세요.
    1. author 속성은 다음과 같습니다.

    ```markdown
        [닉네임]:
            name: [이름]
            display_name: [표시되는 이름]
            email: [본인 이메일]
            github: [Github 닉네임]
            role: [역할, lead || core || normal ]
            member: [현재 활동 여부 boolean]
            alumni: [alumni 여부 boolean]
            blog_team: [블로그 팀 테두리 입히기]
            web: [블로그 주소(선택)]
    ```
