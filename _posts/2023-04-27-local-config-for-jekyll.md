---
layout: single
title: "github blog를 위한 Windows 로컬 환경 - jekyll, bundler"
categories: blog
tag: [github, blog, jekyll, ruby, bundler]
toc: true
toc_sticky: true
toc_label: 목차
---

- [x] 최초 작성일자: 2023-04-27

<!-- <details><summary> 개요 </summary> -->
# 개요

이 글에서는 Github 블로그를 작성하기 위한 로컬 환경에 대해 이야기하겠습니다. <mark style='background:#ffe731'>ruby와 bundler로 jekyll을 설치하여 로컬 서버를 접속하여 내가 작성한 글을 확인하는 환경을 세팅하는 과정</mark>을 진행하기 전에 사전에 미리 준비해야 하는 툴이 있습니다.

- git: 버전관리 툴
- Markdown Editors
  - visual studio code: 무료
  - Typora: 유료
  - Obsidian: 무료
- Ruby
  - jekyll

물론 Visual Studio code나 Obsidian의 경우는 엄밀히 말하면 마크다운 편집기는 아닙니다. 하지만 일단은 글을 작성하기 위해서 어떤 프로그램을 사용할 지 "편집기" 관점에서 쓰자면 다 포함할 수 있습니다. 추후 Visual Studio Code나 Obsidian에 대해 말씀드리겠습니다.

git이나 Markdown Editor가 있다고 가정하고, Ruby 설치부터 jekyll 세팅까지 순차적으로 진행하겠습니다.

<!-- </details> -->
# jekyll, bundler 설치하기

## Jekyll은 무엇인가?

Jekyll은 Static Site Generator로 백엔드 데이터베이스 없이도 간단하고 빠르며 안전한 웹사이트를 만들 수 있습니다.

Github에서는 'Github Pages'를 통해 jekyll로 작동하기 때문에 무료로 자신의 사이트를 포스팅 할 수 있습니다. github pages 만들 때 jekyll이 많이 사용되는 이유는 아무래도 Github 공동설립자인 톰 프레스턴 워너 선생님이 개발한 배경이 있지 않을까 생각합니다. [^1]

[^1]: jekyll (https://en.wikipedia.org/wiki/Jekyll_(software))

물론 jekyll이 루비 기반으로 작성되었기 때문에 다른 언어로 만든 static site generator를 사용하기도 하기도 합니다. javascript로 만든 gatsby도 인기있는 웹페이지 툴입니다. 물론 인지도는 jekyll이 앞섭니다.

## Ruby 설치하기

jekyll은 ruby로 작성했기 때문에 ruby를 설치해야 합니다.
다행히도 github blog를 사용하려고 ruby 언어를 알아서 코드 작성할 필요는 없으니 일단 설치만 하면 70%는 끝난 상태입니다.

루비를 설치하는 사이트는
현재(2023-04-27) 기준으로 ruby 버전은 3.2.2 입니다.

![ruby](/assets/images/download_ruby.png)

설치 창 나올 때 <u>Select Components</u> 파트에서 <mark style='background:#ffe731'>MSYS2 development toolchain을 체크하고 Next 눌러줍니다.</mark>

![select components](/assets/images/check%20MSYS2%20development%20toolchain.png)

설치가 끝났다면 터미널 창이나 명령 프롬포트를 열어서 ruby 버전과 gem 버전이 나오는지 확인이 되면 설치가 끝난 것입니다.

```
$ ruby -v
ruby 3.2.2 (2023-03-30 revision e51014f9c0) [x64-mingw-ucrt]
```

gem은 파이썬의 pip 패키지 처럼 ruby 프로젝트에 포함시켜줄 수 있는 코드 패키지입니다.<br />파이썬에서 패키지 설치할 때 `pip install` 쓰듯이 gem도 동일하게 `gem install` 사용합니다.

```
$ gem -v
3.4.10
```

위의 버전은 2023-04-27 기준으로 최신 버전입니다.

## jekyll 및 bundler 설치

gem 을 사용해서 jekyll과 bundler를 설치해줍니다.

```
gem install jekyll bundler
```

bundler까지 설치했다면 [user].github.io repository로 이동합니다.

```
cd <user>.github.io
```

여기서 bundler 명령어 사용하면 해당 repo 내에 있는 Gemfile을 통해 추가 라이브러리나 소프트웨어를 설치합니다. <br />
현재 사용하고 있는 테마가 minimal-mistakes인데, Gemfile을 읽어서 gemspec을 수행한 다음에, `minimal-mistakes-jekyll.gemspec` 파일 내에 있는 라이브러리 버전이나 소프트웨어 버전 등을 체크하여 추가 설치합니다.

```
bundler install
```

## Local Server 확인하기

이제 github.io repo에서 로컬로 사이트 올려봅시다.
현재 경로가 github.io repo에 있다 가정한 다음 `bundler exec`를 치면 됩니다.

```
bundler exec jekyll serve
```

이렇게 되면 `127.0.0.1:4000` 접속하면 내 github page가 나올 것입니다.<br />
마크다운 편집기에서 글을 작성하고 저장한 다음, 로컬에서 새로고침하면 자동으로 업데이트 해 줍니다.

# 마무리

깃헙 블로그 운영할 때 가장 큰 고비가 되는 영역 중 하나를 완성했습니다. 위의 과정을 한 번에 성공하기 힘듭니다. 저도 버전 충돌로 강제로 업데이트 해야 하거나 지우고 다시 설치하는 방법으로 겨우 해결했습니다.

다음에 블로그 관련 글을 쓴다면 다시 처음으로 돌아가 github pages 생성하는 방법부터 시작하겠습니다. 다른 과정을 제쳐두고 jekyll 관련 내용을 쓰게 된 이유가, `jekyll -v`만 쳤을 때 뱉어낸 에러 메세지를 해결하는 과정을 기억하기 위함이었습니다.

```
$ jekyll -v
Resolving dependencies...
C:/Ruby32-x64/lib/ruby/site_ruby/3.2.0/bundler/resolver.rb:108:in `rescue in solve_versions': Could not find compatible versions (Bundler::SolveFailure)

Because every version of minimal-mistakes-jekyll depends on jekyll-feed ~> 0.1
  and jekyll-feed ~> 0.1 could not be found in locally installed gems,
  minimal-mistakes-jekyll cannot be used.
So, because Gemfile depends on minimal-mistakes-jekyll >= 0,
  version solving has failed.
```

다행히 해결하게 되어 ~~ChatGPT 고마워요!~~ 기념적인 글도 쓸 수 있었습니다.
조금이나마 도움이 되었으면 좋겠습니다.

궁금한 점이나 잘못된 점이 있다면 댓글로 알려주세요.
