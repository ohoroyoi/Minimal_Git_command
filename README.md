# All_about_Git_command
Git을 사용하면서 자주 사용하는 명령어들에 대해 정리한 repository입니다.

</br>

## Basic
#### branch 생성하기
```
git checkout -b [branch name]
```

#### branch 간 이동하기
```
git checkout [branch name]
```

#### 변경사항 확인하기
```
git diff
```

#### commit log 보기
```
git log
```

---

</br>

## Useful command
#### commit 한 개 취소하기
```
git reset HEAD^
```
or
```
git revert HEAD
```

#### commit message 수정하기
```
git commit --amend
```

#### 여러 commit을 하나로 합치기(squash)
```
git rebase -i HEAD~[commit 개수]
```
`.gitconfig`에서 설정해둔 editor 창이 나타난다. 기준이 될 맨 위의 한 commit만 `pick`으로 두고 나머지는 `squash`라는 명령어로 바꿔준다. `:wq` 명령어를 통해 저장하고 종료한다. 그러면 또 다른 editor 창이 나타나는데, commit message를 설정하는 editor이다. 원하는 commit message를 입력하고 `:wq` 명령어를 통해 저장하고 종료해주면 squash 가 된다.

#### local git repository에 remote repository 등록하기
```
git remote add —track master upstream [remote github repository address]
```

#### master branch를 uptream의 latest version으로 update시키기
```
git pull --ff upstream master
```

#### 파일의 변경 이력을 무시해서 stage에서 임시로 제외하기
```
git update-index --assume-unchanged [파일명]
```

#### 파일의 변경 이력을 무시해서 stage에서 임시로 제외한 상황을 되돌리기
```
git update-index --no-assume-unchanged 파일명
```

#### 특정 branch 생성하며 remote에 push하기
```
git push origin feature-LINEREDIS-640-3
```

#### git log graph로 출력하기
```
git log --graph
```

#### git history 출력하기
```
git reflog
```

</br>

---

</br>

## 상황에 따른 git command 집합
### 상황 1. conflict가 발생하는 상황
```
git merge upstream/master
(resolve conflict in editor)
git add src
git commit
git rebase upstream/master
(resolve conflict in editor again)
git add src
git rebase --continue
git push -f upstream YOUR_BRANCH_NAME
```
or
```
git fetch upstream
git rebase upstream/master
(resolve conflict)
git add .
git rebase --continue
git push -f origin [YOUR_WORKING_BRANCH_NAME]
```

</br>

---

</br>

## 알아두면 쓸모있는 Git Tip

### Git command alias
`Git`을 설치한 디렉토리에는 `.gitconfig` 파일이 존재한다. 이 파일에서 자주 사용하는 명령어에 대해서 alias를 지정해줄 수 있다.
``` .gitconfig
[alias]
    g = git
    st = status
    co = checkout
    ad = add
    cm = commit -m
    acm = commit -am
    ph = push
    rb = rebase -i
    fh = fetch
    df = diff
    br = branch -a
    lg = log --graph --abbrev-commit --decorate --format=format:'%C(cyan)%h%C(reset) - %C(green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(yellow)%d%    C(reset)' --all
    re = reset HEAD\\^
    fu = fetch upstream
    rum = rebase upstream/master
    pom = push origin master
    list = config --get-regexp alias
    readme = !git add . && git commit -m "Update README.md" && git push origin master
    docs = !git add . && git commit -m "Update" && git push origin master
    update = !git fetch upstream && git rebase upstream/master && git push origin master
```

</br>

### Commit Log format

* 제목과 본문을 빈 행으로 분리한다
* 제목 행을 50자로 제한한다
* 제목 행 첫 글자는 대문자로 쓴다
* 제목 행 끝에 마침표를 넣지 않는다
* 제목 행에 명령문을 사용한다
* 본문을 72자 단위로 개행한다
* 어떻게 보다는 무엇과 왜를 설명한다

- 제목
  - 대문자, 동사로 시작. 앞에 'If applied, this commit will '가 생략된 것으로 간주
  - 가급적 50자 안쪽
  - 마침표 생략
- 본문
  - 3번째 줄부터 시작 (두번째 줄은 비움)
  - 최대줄 너비는 80자. 이상은 줄바꿈

### 추천 동사(personal)
- `Add` : 새로운 기능 또는 api 추가
  - 예) Add API creating PDF
- `Remove` : 제거
  - 예) Remove unused local variables
- `Enhance` : 기능 또는 성능의 향상
  - 예) Enhance performance in select queries
- `Fix` : 버그,  오타, 스타일의 수정
  - 예) Fix typos in Javadoc
  - 예) Fix styles for standards of Naver Corp
- `Upgrade` : 라이브러리 버전 업그레이드
  - 예) Uprade commons-dbcp to 2.3.1
- `Document` : 문서화
- `Refactor` : 리팩토링
- `Update` : 다른 주변 상황에 맞추어서 갱신
  - 예) Update README.md for 1.0 release
- `Polish` : 잡다한 수정 묶음 (다른 적절한 문구가 없을 경우 사용)


#### Reference>
* [How to Write a Git Commit Message](https://item4.github.io/2016-11-01/How-to-Write-a-Git-Commit-Message)
