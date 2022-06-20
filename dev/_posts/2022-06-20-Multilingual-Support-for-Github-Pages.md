---
layout: post
title: 다국어를 지원하는 Github 블로그 만들기
subtitle: 바보 같아 보이지만.. 단순하기도 한 방법
category: dev
thumbnail: /assets/img/blog/2022-06-20-github_pages_logo.jpg
sitemap: false
---

Github 블로그를 처음 만든 건 2020년이지만 글을 안쓰고 Resume만 조금씩 업데이트하면서 방치해놓고 있다가
박사과정을 시작하면서 제대로 써보기 시작해야겠다고 마음먹고 Setting을 시작했다.

> 한국어로 쓸지 영어로 쓸지도 아직 결정 못했는데 석사 졸업하고 취업각이 확실하면 한국어로 계속 쓰고
> 진학각이 보이면 영어로 다 고쳐써야지.

라고 썼었는데, 정작 박사 진학을 하고 보니, 영어로만 쓰기엔 내 작문 실력이 심히 취약한 것이었다.

일단 글을 쓰려고 마음을 먹어도 영어로 써야 하니 쉽지 않아서...
한국어로 일단 쓰고, 영어로 번역할 수 있도록, 다국어 지원 블로그를 만들기로 했다.

현재 사용하고 있는 테마는 [Hydejack](https://hydejack.com/) 유료 버전. 당연히 다국어 지원이 될 줄 알았지만, 그런 옵션은 없었다.

&nbsp;

일단 열심히 검색해보니, [한 블로그](https://byeongsupark.github.io/blog/multilingual-github-page/jekyll-with-polyglot)
에서 *PolyGot*이라는 plugin을 활용한 걸 발견했다.

가볍게 트라이 해보려고 했지만, 무려 플러그인도 깔아야 되는 것.

내가 만들기 싫어서 테마도 산 마당에 지금 설치?

라는 생각에 좀 더 바보 같은 방법을 생각해 냈다.

&nbsp;

1. `main` 브랜치에 localization 관련 파일을 제외하고 모두 때려 넣는다.
2. `en` 브랜치를 새로 만들어서 영어 localization 파일과, 영문 블로그 파일을 넣는다.
3. `en` 브랜치를 기준으로 page 빌드하도록 설정해준다.

여기까지 하면, 일단 영문 페이지는 완성.

&nbsp;

1. `ko` 브랜치를 새로 만들어서 한국어 localization 파일과, 한국어 블로그 파일을 넣는다.
2. `ko` 라는 이름으로 repository를 새로 만든다!
3. `ko` 레포지토리에 subtree로 기존 블로그 레포지토리의 `ko`브랜치를 `docs`폴더에 넣는다!
4. `docs` 폴더를 기준으로 page 빌드하도록 설정한다.

이렇게 하면 `~~~.github.io\ko\`에 한국어 버전 블로그가 보여진다!

&nbsp;

좀 더 구체적으로 하나씩 step을 밟아보면...

> 1) `main` 브랜치에 localization 관련 파일을 제외하고 모두 때려 넣는다.
> 2) `en` 브랜치를 새로 만들어서 영어 localization 파일과, 영문 블로그 파일을 넣는다.

굳이 브랜치를 하나 나눠버리는 이유는, 테마 소스코드가 업데이트되면, 업데이트를 수월하게 하기 위함이다.

업데이트가 필요하면, 나중에 언어별 branch에 `main`을 merge하면 간단하니까.

> 3) `en` 브랜치를 기준으로 page 빌드하도록 설정해준다.

![github_page_settings](/assets/img/blog/2022-06-20-github-pages-settings.png)

Github page setting에 들어가보면 `Source`에서 원하는 branch를 선택해서 만들수 있다.
여기서 `en` 브랜치를 선택해준다.

> 4) `ko` 브랜치를 새로 만들어서 한국어 localization 파일과, 한국어 블로그 파일을 넣는다.
> 
> 5) `ko` 라는 이름으로 repository를 새로 만든다!

Github Page는 `<username>.github.io` 레포지토리에 올라간 파일을 `<username>.github.io`에 올려주고,
<br>
다른 레포지토리에 올라간 파일을 `<username>.github.io/<repository_name>`에 올려준다.

`<username>.github.io/ko/`에 한국어 파일이 올라갈 수 있도록 레포지토리를 만든 것이다.

> 6) `ko` 레포지토리에 subtree로 기존 블로그 레포지토리의 `ko`브랜치를 `docs`폴더에 넣는다!
> 
> 7) `docs` 폴더를 기준으로 page 빌드하도록 설정한다.

Git `subtree`는 다른 repository의 결과물을 해당 repository에 가져올 수 있는 방법 중 하나다.

`submodule`이라는 방법도 있는데, `submodule`은 여기에 이 module을 참조한다는 기록만 남기는 반면, `subtree`는 실제 파일을 다 가져오기 때문에 더 적합하다고 생각했다.

Subtree는 다음과 같이 할 수 있다.
> subtree를 가져올 repository를 먼저 추가한다.
> 
> ```shell
> git remote add site https://github.com/<username>/<username>.github.io.git
> ```
> 
> subtree를 활용해서 원래 site의 `ko` 브랜치를 `docs` 폴더에 추가한다.
> ```shell
> git subtree add --prefix docs site ko
> ```
> 결과를 push해서 마무리
> ```shell
> git push origin main
> ```

![github_page_settings_ko](/assets/img/blog/2022-06-20-github-pages-settings-ko.png)

Github page가 페이지를 만들도록 설정할 수 있는 디렉토리는 `/(root)`와 `/docs` 뿐이다.
따라서, 꼭!!!! `docs` 폴더에 subtree를 추가해 놓아야 한다!

&nbsp;

좀 더 멋진 페이지가 되려면, 한국어와 영어 블로그를 전환하는 버튼도 있어야 할 것 같아서,

```html
<a id="_lang-change" class="nav-btn no-hover" href="#" onclick="language_change()">
    <script>
      function language_change() {
        location.href = 'https://eunhocho.github.io' + window.location.pathname.substring(3);
      }
    </script>
    <span><h3 style="margin: 0 0 0">en</h3></span>
</a>

<a id="_lang-change" class="nav-btn no-hover" href="#" onclick="language_change()">
    <script>
        function language_change() {
            location.href = 'https://eunhocho.github.io/ko' + window.location.pathname;
        }
    </script>
    <span><h3 style="margin: 0 0 0">ko</h3></span>
</a>
```

한국어와 영어 메뉴바에 각각 변환 버튼을 추가했다.

이렇게 단순하게 완성.

장점은
1. Plugin 설치를 안해도 잘 된다.
2. 어렵지 않다.

단점은
1. 한국어 영어 바꿀때마다 checkout해서 브랜치 바꾸는 게 좀 귀찮다.
2. 한국어 버전은 추가적으로 `git subtree pull`을 해줘야 해서 좀 귀찮다.

가 있겠다.

머리가 안좋으면 몸이 고생하는 것과 비슷한 것 같다...

아무튼 됐으니까! 이제 연구 관련된 것도 작성 해봐야 겠다.
