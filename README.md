# git-hack

## 커밋 메시지 바꾸기

rebase 시작

```
# 특정 커밋부터
git rebase -i HEAD~x
# root 커밋부터
git rebase -i --root
```

nano또는 vim, emacs 에서 수정할 커밋들 선택

```
...
pick 492c244 (init)
pick 92c0230 0.0.1
pick 03752c0 :.
pick 1c35c3c asdf
edit 5ab809e asdf
pick fb4c214 asdf
pick 1138de5 asdf
e 4f8aa37 asdf
pick 722b7e3 asdf
pick 3224c25 (주석 추가
...
```

수정할 커밋 edit또는 e로 바꿈. 버릴 커밋은 drop으로 바꿈(drop된 커밋은 수정된 내용까지 완전히 사라짐)
수정 후 파일 저장

하나씩 커밋 수정

```
git commit --amend --author="rollrat <rollrat.cse@gmail.com>" --no-edit     
```

`--no-edit`를 붙이면 `interactive`에 들어가지 않음
커밋 변경 후 해당 커밋 저장

```
git rebase --continue
```

위 사항 반복 후 최종 rebase 완료 메시지 확인

수정된 커밋 최종 확인

```
 > git log --pretty=fuller
commit 1c35c3ceff26af79c47c0fc0b57f7b8b318e3c3f
Author:     rollrat <rollrat.cse@gmail.com>
AuthorDate: Sun Aug 23 17:47:34 2020 +0900
Commit:     rollrat <rollrat.cse@gmail.com>
CommitDate: Sun Aug 23 17:47:34 2020 +0900

    asdf

commit 03752c01fc97fde7454cbf22420b662a12fffd5f
Author:     rollrat <rollrat.cse@gmail.com>
AuthorDate: Sat Aug 22 21:33:03 2020 +0900
Commit:     rollrat <rollrat.cse@gmail.com>
CommitDate: Sat Aug 22 21:33:03 2020 +0900

    :.

commit 92c0230ec692605277348e0b081198c96359b626
Author:     rollrat <rollrat.cse@gmail.com>
AuthorDate: Sat Aug 22 10:36:21 2020 +0900
Commit:     rollrat <rollrat.cse@gmail.com>
CommitDate: Sat Aug 22 10:36:21 2020 +0900

    0.0.1

commit 492c244372ba35ab2ee7f665a43d046a83b3cbae
Author:     rollrat <rollrat.cse@gmail.com>
AuthorDate: Fri Aug 21 14:53:02 2020 +0900
Commit:     rollrat <rollrat.cse@gmail.com>
CommitDate: Fri Aug 21 14:53:02 2020 +0900

    (init)
```

AuthorDate와 CommitDate가 서로 맞지 않다면

```
git filter-branch --env-filter 'export GIT_COMMITTER_DATE="$GIT_AUTHOR_DATE"'
```
