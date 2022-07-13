---
layout: single
title: "macOS에서 git 설정"
categories: Git/Github
tag: git, github
---

$ git --version<br>
git이 설치되었는지 확인 및 버전 확인

$ git 설치 후 설정<br>
$ git config --global user.name "나의 사용자 이름"<br>
$ git config --global "내 이메일 주소"


--global 옵션으로 설정하면 사용자 홈에 저장되며 git을 설정할 때 최초 한번만 입력해도 된다. 나중에 이름이나 이메일을 변경한다면 이 명령어를 다시 입력해야 한다.

 

**SSH 등록 및 SSH를 이용한 git clone**<br>
-SSH 등록<br>
-SSH 키 생성 => 생성된 공개키 복사 => github Settings => SSH and GPG<br>
-keys => New SSH key에 공개키 붙여넣기<br>
-Clone<br>
-그 후 Code버튼의 SSH탭 선택 => 복사 => 터미널에 git clone 명령어 후 붙여넣기<br>