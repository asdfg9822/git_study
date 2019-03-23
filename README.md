# git_study

git 작업을 위한 최소한의 사용법/명령어 정리

### git branch

### git checkout

checkout 명령어로 브랜치를 변경할 수 있다.

```
git checkout [브랜치명]
```

브랜치가 없다면 -b 옵션으로 브랜치를 생성함과 동시에 브랜치를 변경할 수 있다.
```
git checkout -b [브랜치명]
```

> checkout을 하기 위해서는 커밋되지 않은 수정사항을 커밋(commit), 임시보관(stash), 폐기(discard) 해야 한다

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