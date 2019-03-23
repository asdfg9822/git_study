# git_study

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

github의 경우 릴리즈 탭에 자동으로 추가되며, 바로 소스코드를 다운받을 수도 있다.
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