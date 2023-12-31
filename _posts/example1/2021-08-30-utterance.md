---
layout: post
title: test test
description: >
    댓글기능으로 utterance 적용
sitemap: false
hide_last_modified: false
categories:
  - example1
---

# 댓글기능 utterance 추가하기

블로그에 댓글기능이 없어도 블로그를 운영하는데는 상관이 없지만

댓글 기능이 있음으로 본인이 올린 게시물에 대해 잘못된점을 지적받을수 있고 궁금한점을 질문 받고 토론할수 있을것이다. 이처럼 댓글은 블로그의 게시물 퀄리티를 한층 높여주고 커뮤니티의 기능등 블로그의 순 기능들을 잘 수행하게 해준다.

처음에 블로그를 시작하게 된 이유를 생각해보자.

​

따라서 댓글기능은 꼭 필요한것은 아니지만 한편으로 중요하다고 볼수있다.

댓글기능 구현은 여러방법이 있는데 그중에서 방문자가 가장 쉽게 댓글을 쓸수 있는 방법을 사용할려고 한다.

​

댓글을 쓸려고 해도 가입을 해야하거나 로그인하기가 불편하다면 쓸려다가도 안쓰게 된다.

utterances는 간단히 깃헙 계정이있고 깃헙이 로그인되어있다면 버튼하나로 손쉽게 댓글을 쓸수 있다.


* toc
{:toc .large-only}

## 1_ utterances란
---
🔗 [https://github.com/apps/utterances](https://github.com/apps/utterances)

utterances는 깃허브의 이슈기능을 가지고 댓글을 생성해준다. 게시글 하나가 이슈 하나와 매핑이 되고, 게시글에 댓글을 달면 해당 이슈에 댓글이 달린다. 댓글 창은 iframe으로 동작하며 해당 페이지가 로드될 때, 페이지의 URL, pathname, 혹은 title을 가지고 issue search API 를 통해 해당 이슈에 달린 댓글을 로딩하여 댓글 창에 로딩시켜준다.

만약에 내가 최초로 댓글을 달아서 이슈가 없다면? utterances-bot이 자동적으로 이슈를 생성해준다고 한다.

utterances를 적용하려고 하는 이유는 다음과 같다.

1. <mark>개발자 블로그이니 만큼 따로 번거러운 작업 없이 깃허브 계정만으로도 바로 댓글을 쓸수 있으면 한다.</mark>

2. <mark>익숙한 깃허브의 UI를 보고싶다.</mark>

3. <mark>다음에 또 이런 마이그레이션 작업이 필요할 수 있으니, 게시글과 댓글을 매핑하는 설정이 쉬우면 좋겠다.</mark>

4. <mark>Disqus는 댓글쓰는것이 불편하다.</mark>

#### utterances 장점 모음
​
<code>▶깃허브는 다수 개발자가 가입은 해둔 플랫폼입니다.</code>

-깃허브 앱인 utterances는 깃허브 계정만 있으면 되기 때문에 블로그 운영자와 사용자는 대부분 별도 가입을 하지 않아도 됩니다.

​

<code>▶특별한 관리 부담이 필요치 않습니다.</code>

-운영자 입장에서도 자주 사용하는 플랫폼인 깃허브는 친숙한 환경이기에 설치나 관리에 대한 부담이 없습니다.

​

<code>▶댓글 알림을 받을 수 있습니다.</code>

-github issues를 댓글 쓰레드로 사용하는 utterances는 댓글이 등록되면, 즉 새로운 issue가 등록된 것이므로 메일 알림을 받을 수 있습니다.

-이 때문에 소중한 독자와 소통하는 타이밍을 놓치지 않게 됩니다.

​

<code>▶설치 및 설정이 쉽습니다.</code>

- utterances앱을 깃허브 계정에 추가한 뒤 댓글 저장 용도로 사용될 신규 레포지토리 추가하여 권한을 주면 됩니다.

-이후 댓글 영역에 스크립트 코드 한 줄만 추가해주면 셋팅이 끝납니다.

​

<code>▶Markdown 문법을 이용하여 댓글 작성이 가능합니다.</code>

-github 플랫폼을 이용하기 때문에 당연히 마크다운 문법 사용이 가능합니다.

​

그렇다면 이제 utterance를 적용해보자.

​

## 2_ 시작하기전에
---
먼저 댓글있을 저장소(레파지토리)를 지정해야합니다.

따라서 새로운 레파지토리를 만들어줍니다.


![그림1](/assets/img/blog/githubpages/7-1.jpeg)

저는 이름을 blog-comments-repo로 지어주었습니다.


## 3_ 설치하기
---
**utterance app 설치**

🔗 [https://utteranc.es/](https://utteranc.es/)에서 utterance앱을 설치한다.

설치 버튼을 클릭해 설치를 실행한다.

![그림2](/assets/img/blog/githubpages/7-2.jpeg)


![그림3](/assets/img/blog/githubpages/7-3.jpeg){: width="400" height="400}

처음에는 All repositories로 선택되어있는데 Only select repositories를 선택하고 블로그 댓글저장소(blog-comments-repo)를 골라주고 이후 Install 버튼을 누른다.

![그림4](/assets/img/blog/githubpages/7-4.jpeg)

이후 비밀번호로 한번 확인받는다. 이후 아래와 같은 페이지가 나온다.

![그림5](/assets/img/blog/githubpages/7-5.jpeg){: width="400" height="400}

조금더 내려 configuration의 repo:에 자신의 블로그 댓글 저장소를 입력해준다.


## 4_ configuration
---
![그림6](/assets/img/blog/githubpages/7-6.jpeg){: width="400" height="400}

#### Blog post <--> Issue 매핑 방식을 선택

![그림7](/assets/img/blog/githubpages/7-7.jpeg){: width="400" height="400}

위에서 언급했듯이 utterances는 게시글 하나와 레파지토리의 이슈 하나가 서로 연동되는 시스템이다.

**(post <--   --> issue 매핑)**

이런 연동 방법으로 난 다섯 가지가 있다.

1. pathname

> 포스트의 pathname으로 이슈를 생성한다. 이 포스팅 같은 경우는 /blog/2020/12/18/utterances- 적용으로 이슈가 생성되어 매핑된다.

​

2. page URL

> 게시글의 URL 전체로 이슈를 매핑한다.

​

3. page title

> 게시글의 제목으로 이슈를 매핑한다.

​

4. issue number

> 이슈 번호를 가지고 매핑한다.

​

5. issue title contains specific term

> 게시글 제목에 특정 단어가 들어가 있는지 체크하여 매핑한다.

​

필자는 URL이 바뀔일이 없다고 생각하여 pathname으로 하였다.

#### Theme 와 Enable Utterances

![그림8](/assets/img/blog/githubpages/7-8.jpeg)

테마를 흰색할지 검정색할지등 골라주고 위 코드를 복사해준다.

<strong>
<code class="language-plaintext highlighter-rouge">
_includes/comments.html
</code>
</strong>
 파일에 아래와 같이 복사한 코드를 넣어준다.

![그림9](/assets/img/blog/githubpages/7-9.jpeg)

이제 저장을 하고 터미널에 수번을 했던것처럼 bundle exec jekyll serve를 해준다.

![그림10](/assets/img/blog/githubpages/7-10.jpeg)

짜잔~ 댓글기능이 생겼다.