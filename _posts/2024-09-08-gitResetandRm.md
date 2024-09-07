---
title: "원격에 업로드한 파일에 .gitignore 적용하기"
date: 2024-09-08
categories: [git]
tags: [github, git]
---

실습파일을 깃허브에 올렸는데 실수로 node_modules 폴더까지 업로드해버린 것을 발견...
깃허브 페이지에서 해당 폴더에 들어가니까 로딩이 엄청 오래 걸려서 node_modules을 .gitignore에 추가해주고 다시 업로드해야 했다.

## 1. .gitignore에 추가하려고 하는 파일/폴더의 상위폴더로 이동

내 경우에는 server/node_modules 였기 때문에 server폴더에서 작업을 진행

```plaintext
git rm --cached - r 파일/폴더 이름
```
node_modules를 삭제하고 싶으면 `git rm --cached -r node_modules` 입력. <br>
여기서 `--cached`를 붙이면 파일이 로컬 저장소에는 그대로 있는 상태로 원격 저장소에서만 삭제된다. <br>
`-r` 은 recursive라는 뜻으로 파일/폴더가 삭제되면 하위에 있는 파일, 서브디렉토리도 모두 삭제된다. <br>

## 2. .gitignore에 반영 후 업로드

.gitignore 만들고 안에 무시할 항목을 적어줬으면 아래의 과정 진행

```plaintext
git add 파일 이름
git commit -m '커밋 메세지'
git push
```




<hr />





처음에는 node_modules를 원격에서 없애려고 `git reset`을 실행했다(<b>절대안돼...</b>)

```plaintext
git reset --hard '커밋 해쉬값'
```
이 명령어를 실행하면 원하는 커밋 위치로 돌아갈 수 있다. 대신 그 이후에 새롭게 작성한 파일 모두 날아간다...<br>
이렇게 날린 파일은 그래도 복구가 가능하다

```plaintext
git reflog 
git reset --hard '커밋 해쉬값'
```
먼저 로컬 저장소의 HEAD 업데이트 기록을 보기 위해 `git reflog` 명령어를 실행하고, `reset` 명령어로 날려버린 해쉬값을 확인한 후 다시 거기로 돌아가면 날린 파일이 모두 복구된다!<br>




.gitignore를 좀 만진 것 뿐인데 아주... 큰 일이 날 뻔했다<br>
앞으로는 git 명령어 쓰기 전에 어떤 결과가 나올지 잘 생각하고 사용해야겠다(branch도 좀 쓰고)






