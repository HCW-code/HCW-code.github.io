---
layout: single
title: "[Git] 브랜치 관리"
categories: Git/Github
tag: [branch, git]
toc: true

---

### Git Branch

브랜치란 독립적으로 어떤 작업을 진행하기 위한 개념이다.

- 한 소스코드에서 동시에 다양한 작업을 할 수 있게 해준다.
- 소스코드의 한 시점과 동일한 상태를 만들고, 브랜치를 넘나들며 작업을 수행할 수 있다.
- 각각의 브랜치에서 생긴 변화가 다른 브랜치에 영향을 주지 않고 독립적으로 코딩을 진행할 수 있다.

hot fix, release, develop, feature 등 다양한 브랜치를 만들고 작업을 하다 보면 다음 이미지와 비슷한 Git graph가 만들어진다.
<center>
<img src="../../images/2022-10-17-blockchain_36th/image-20221017171900886.png" alt="image-20221017171900886" style="zoom: 50%;" />
</center>
#### 브랜치 종류

**통합 브랜치(Integration Branch)**

배포될 소스 코드가 기록되는 브랜치

Github Repository를 생성하게 되면 기본적으로 main 브랜치가 생긴다. 해당 프로젝트의 모든 기능이 정상적으로 작동하는 상태의 소스코드가 담겨있다.

**피처 브랜치(Feature Branch)**

기능 추가, 버그 수정과 같이 단위 작업을 위한 브랜치

통합 브랜치로부터 만들어내며, 피처 브랜치에서 하나의 작업이 완료되면 다시 통합 브랜치에 병합하는 방식으로 진행된다. 토픽 브랜치라고도 한다.

#### 브랜치 명령어 모음

새로운 브랜치 생성

```shell
git branch [새로운 브랜치 이름]
```

새로운 브랜치 생성 후 해당 브랜치로 전환

```shell
git switch -c 새로운 브랜치 이름
git checkout -b 새로운 브랜치 이름
```

브랜치 전환

```shell
git switch 브랜치 이름
git checkout 브랜치 이름
```

브랜치 목록 확인

```shell
git branch
```

브랜치 목록과 각 브랜치의 최근 커밋 확인

```shell
git branch -v
```

브랜치 병합

- master 브랜치로 dev 브랜치를 병합할 때

```shell
git checkout master 마스터 브랜치로 이동
git merge dev 병합
```

로그에 모든 브랜치를 그래프로 표현

```shell
git log --branches --graph --decorate
```

아직 commit 하지 않은 작업을 스택에 임시로 저장

```shell
git stash
```

