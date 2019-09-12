# git_study

git 작업을 위한 최소한의 사용법/명령어 정리

### Git 초기 계정 설정

전역 설정
```
git config --global user.name "계정이름"
git config --global user.email "이메일"
```

저장소별 설정
```
git config user.name "계정이름"
git config user.email "이메일"
```

설정 조회
```
git config --global --list
```

저장소별 설정 조회
```
git config --list
```

### 새로운 저장소 초기화

```
git init
```

### 저장소 복제하기
```
git clone [저장소 URL]
```

### 새로운 원격 저장소 추가하기
```
git remote add [원격저장소] [저장소 URL]
```

### git branch

브랜치 생성
```
git branch [브랜치명]
```

존재하는 브랜치 리스트
```
git branch
```

브랜치 삭제
```
git branch -d [브랜치명]
```

### git checkout

checkout 명령어로 브랜치를 변경할 수 있다.

```
git checkout [브랜치명]
```

브랜치가 없다면 -b 옵션으로 브랜치를 생성함과 동시에 브랜치를 변경할 수 있다.
```
git checkout -b [브랜치명]
```

> checkout을 하기 위해서는 커밋되지 않은 수정사항을 커밋(commit), 임시보관(stash), 폐기(discard) 해야 한다.

> 테스트 결과 staged file의 경우 전환할 브랜치에서 동일 파일의 수정이 없으면 전환이 잘된다. stash를 사용하지 않는다면 staged, unstaged 2개의 파일 모두 브랜치 전환시 유지되었다.

> stash 명령어를 쓰면 staged file은 모두 백업되어 보이지 않는다. unstaged file은 유지되었다.


### git stash

작업 중 다른 브랜치로 교체해야하는 경우 작업 중인 파일들을 stash 명령어로 임시보관 할 수 있다.
해당 작업들에 대한 기록이 stashing area로 보관되며 스택 형태로 쌓이게 된다.



작업중인 파일 stash
```
git stash
```

stash 리스트 보기
```
git stash list
```

보관된 stash 적용 (작업파일을 staged 상태로 변경시키지 않음)
```
git stash apply
```

보관된 stash 적용 (작업파일을 staged 상태로 변경)
```
git stash apply --index
```

stash를 적용한 브랜치 생성
```
git stash branch [브랜치명]
```

### 태그 생성하기

git의 태그 생성 방식에는 lightweigth 태그와 annotated 태그 2가지가 있다. lightweight 태그는 커밋의 포인터이다.
annotated 태그는 생성한 사람의 이름, 이메일, 태그 생성일, 태그 메시지를 저장하고 GPG (GNU Privacy Guard)로 서명할 수도 있다.

```
git tag [tag name]
```

annotated 태그를 생성하기 위해서는 -a 옵션을 주면 된다. 일반적으로는 lightweight를 사용하는 것 같다.

로컬 저장소에 태그를 생성하고 원격지에 전송하기 위해서는 push 명령어 사용 시 --tags 옵션을 주어야 한다.
```
git push [원격저장소명] [태그명]
git push [원격저장소명] [로컬브랜치명] --tags
```

github/gitlab의 경우 릴리즈 탭에 자동으로 추가되며, 바로 소스코드를 다운받을 수도 있다.
추가적인 릴리즈 메시지를 작성할 수 있고 추가적인 첨부파일을 올릴 수 있다.

![Github Tag Test](/image/github_tag_test_img.png)

### 변경사항 추출 및 적용하기

git diff 명령어를 사용해서 변경사항을 추출할 수 있다.
patch 명령어로 생성된 patch 파일을 적용할 수 있다.

패치파일 생성
```
git diff --no-prefix > patchfile
```

패치파일 적용
```
patch -p0 < patchfile
```

만약, --no-prefix 옵션을 주지 않았을 경우 p1으로 적용하면 변경된다
```
patch -p1 < patchfile
```

### 커밋 이력 확인하기
tag 추가 등은 나오지 않고 merge, commit 등의 이력만 나온다
```
git log
```

4개만 출력하기
```
git log -4
```

한줄로 출력하기 (간단정보만)
```
git log --oneline
```

그래프 출력 (oneline 옵션 추가해야 보기 좋음)
```
git log --oneline --graph

출력 결과
*   4ad69b1
|\
| * 97c3244 Git 명령어 추가
* | 111c917 Git 명령어 추가
|/
*   2e5a1db Merge remote-tracking branch 'origin/master'
|\
| * 726030a Git 명령어 추가
```

### 로컬 파일 되돌리기
실수로 무언가 잘못한 경우, 아래 명령으로 로컬의 변경 내용을 되돌릴 수 있다 ( 로컬의 변경 내용을 변경 전 상태(HEAD)로 되돌림 )
만약 파일이 staged 상태라면 reset이용하여 staged 상태를 초기화 한 후 이용해야 한다.
```
git checkout -- [파일명/폴더명]
```

전체 되돌리기
```
git checkout -- .
```

### 원격 저장소의 데이터를 로컬에 가져오기만 하기
pull을 실행하면, 원격 저장소의 내용을 가져와 자동으로 병합 작업을 실행하게 된다. 단순히 원격 저장소의 내용을 확인하고 병합은 하고 싶지 않은 경우 fetch를 사용할 수 있다
```
git fetch [원격저장소명]
```

### 원격 저장소의 데이터를 가져와서 병합
```
git pull
```

### Reset과 Revert
reset의 경우 과거 커밋으로 이동하고자 할 때 사용한다. 돌아가고 돌아간 이후의 커밋이력을 모두 삭제한다.
- hard 옵션 : working directory의 내용까지 모두 바꾸는 방법 (테스트 결과 hard 옵션의 경우 특정 파일/폴더를 지정해서 사용할 수 없다.)
- mixed 옵션 : (Default) working diretory의 내용은 그대로 유지
- soft 옵션 : staging area 까지 올라간 상태로 바꾸는 옵션

Revert의 경우에는 reset과 같이 특정 버전으로 되돌아갈 수 있지만, 되돌린 버전 이후의 버전들의 이력이 남아있다.

reset의 경우 방금 병한한 것을 취소할 때 사용할 수 있다. Revert의 경우 조금 시간이 지난 병합을 취소하고 싶을때 사용할 수 있다.

```
*   4ad69b1
|\
| * 97c3244 Git 명령어 추가
* | 111c917 Git 명령어 추가
|/
*   2e5a1db Merge remote-tracking branch 'origin/master'
|\
| * 726030a Git 명령어 추가
```

(TODO, 안됨) 위와 같이 그래프가 있을 때 mainline 옵션을 이용해서 mainline(주축)을 설정할 수 있다.
```
git revert --mainline 1 [커밋ID]
```

### untracked 파일/디렉토리 모두 삭제하기

untracked 파일 모두 삭제하기
```
git clean -f
```

untracked 파일&폴더 모두 삭제하기
```
git clean -fd
```

미리 확인하기
```
git clean --dry-run
```