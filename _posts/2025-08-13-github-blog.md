---
title: "[GitHub Blog] GitHub Blog 간단하게 로컬 환경에서 실행하기 (with. Docker Desktop)"
date: 2025-08-13 17:47:00 +0900
categories: [etc]
tags: [github blog]
---



GitHub Blog를 Ruby, Jekyll 및 Bundler 설치 없이 로컬 환경에서 실행하는 방법에 대해서 설명하고자 합니다.



<br/><br/>



---

# 🤔 Ruby, Jekyll 및 Bundler를 설치하는 이유

GitHub Blog를 만들려고 찾아보면 멋있는 테마는 거의 Jekyll로 만들어진 것을 확인할 수 있습니다. 이러한 이미 만들어진 Jekyll 테마를 이용해서 만들려고 하면 Ruby, Jekyll 및 Bundler를 설치해야 합니다.

*Jekyll 테마를 이용해서 GitHub 블로그를 만들기 때문에 Jekyll를 설치하는 것은 납득이 가는데 Ruby랑 Bundler는 왜 설치해야 하는가?*라는 의문점이 생겨서 찾아봤습니다. 그 결과, Jekyll는 Ruby 기반으로 동작하는 정적 사이트 생성기로 Ruby의 런타임을 거쳐야 실행할 수 있고, Bundler는 이러한 Ruby의 패키지를 관리하는 도구이기 때문에, Bundler도 설치해야 하는 것입니다.

<br/>

*저러한 설치 과정을 거치면서까지 로컬 환경에서 GitHub Blog를 실행해봐야 하나?* 라는 생각이 들어서, 처음에는 설치하지 않고 글을 작성하고 나면 바로 push해서 결과를 확인하려고 했습니다. 그렇다보니 중간에 오류가 있어도 push가 되어서 블로그가 정상적으로 작동하지 않는 문제점이 발생했습니다... 🥲 (역시 중간에 오류가 생기는지 확인하는 절차가 필요합니다...)

그래서 Ruby 설치하고, Bundler 설치하고, Jekyll를 설치하려고 했는데....

제가 사용하는 Jekyll 테마를 살펴보니 Getting Started에 친절하게 Docker Desktop을 활용해서 Ruby 설치 없이 로컬에서 실행할 수 있는 방법을 알려주고 있었습니다. (무엇이든지 설명서를 읽고 사용해야 해...🤣)

<br/>

Docker Desktop을 활용해서 로컬에서 실행하는 방법은 다음과 같습니다.

```
1. 도커를 설치한다.
2. Visual Studio를 설치하고, Dev Containers라는 확장 프로그램을 설치한다.
3. GitHub Blog Repository를 Visual Studio로 열어준다.
4. Dev Container가 설치될 때까지 기다려준다.
```

4단계로 간단하지만, 사진과 같이 설명이 있으면 좀 더 쉬워지므로 기록해두고자 합니다.



<br/><br/>



---

# ⚙️ Docker Desktop 및 Visual Studio 설치하기

Docker Descktop이랑 Visual Studio를 설치하는 것은 해당 공식 홈페이지에 가서 다운로드 받으시면 됩니다. 이때, Windows를 사용하시는 분들이 Docker Desktop을 설치하려고 하면 AMD64와 ARM64 이 두 가지 종류가 있다는 것을 확인할 수 있습니다. 둘 중에서 자신의 Windows PC의 CPU 아키텍처와 맞는 것으로 설치하면 되는데, 모르시는 분들은 아래 명령어를 CMD에 실행해서 확인할 수 있습니다.

```shell
echo %PROCESSOR_ARCHITECTURE%
```

<br/>

Visual Studio를 설치하셨다면, 확장 프로그램에서 **Dev Containers**라는 확장 프로그램을 설치하시면 됩니다. Dev Containers라는 확장 프로그램까지 다 설치하셨다면, 자신의 GitHub Blog repository를 Visual Studio로 여시면 자동으로 해당 GitHub Blog를 로컬 환경에서 실행할 수 있는 Docker Container를 설치해줍니다.

모든 것이 정상적으로 설치되었다면 GitHub Blog를 로컬 환경에서 실행할 수 있는 환경 설정은 끝났습니다!



<br/><br/>



---

# 💎 GitHub Blog 로컬 환경에서 실행하기

해당 GitHub Blog repository를 Visual Studio에서 열으면 자동으로 Dev Container가 실행되는 것을 확인할 수 있습니다.

![Desktop View](/assets/img/2025-08-13-github-blog/Dev%20Container%20실행%20중.png)
_Dev Container 실행 중_

<br/>

Dev Container가 실행되는 것을 확인했으면, Visual Studio에서 터미널을 열어서 다음 명령어를 실행하여 Ruby 서버를 실행시키면 됩니다.

```shell
bundle exec jekyll serve
```

<br/>

정상적으로 실행했다면 http://127.0.0.1:4000으로 접속하면 아래와 같이 GitHub Blog을 확인할 수 있습니다.

![Desktop View](/assets/img/2025-08-13-github-blog/로컬%20환경에서의%20GitHub%20Blog.png)
_로컬 환경에서의 GitHub Blog_



<br/><br/>



---

Docker Container를 설치하는 과정에서 AMD64와 ARM64의 차이점에 대해서 살펴보는 기회가 되었습니다.

AMD64와 ARM64는 컴퓨터의 CPU 아키텍처를 나타내는 것으로,
- AMD64는 전통적인 PC와 서버에 주로 사용되는 64비트 아키텍처로 성능이 강력하고 전력 소모가 상대적으로 높다는 특징을 지니고 있으며, 대부분의 테스크톱, 노트북, 서버에 사용되고 있으며
- ARM64는 전력 효율이 높아 배터리 소모가 적고, 모바일 기기나 저전력 장치에 적합하다는 특징을 지니고 있으며, 주로 스마트폰, 태블릿, 임베디드 시스템 등에서 사용되고 있다.

<br/>

이상 Docker Container을 이용해 GitHub Blog를 로컬 환경에서 실행하는 방법이었습니다.

감사합니다! 😊


<br/>


## 참고자료

- [Docker 설치시 Windows 설치버전 중 AMD64와 ARM64](https://arc-viewpoint.tistory.com/entry/Docker-%EC%84%A4%EC%B9%98%EC%8B%9C-Windows-%EC%84%A4%EC%B9%98%EB%B2%84%EC%A0%84-%EC%A4%91-AMD64%EC%99%80-ARM64#google_vignette)

많은 도움이 되었습니다.  
감사합니다 🥰
