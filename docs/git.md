# git

## orphan branch

### 정의

하나의 저장소에서 다른 브랜치나 커밋으로부터 단절된 새로운 history를 가지는 브랜치를 의미한다.
다른 브랜치와 독립적으로 운영할 수 있다.

### 생성 방법

1. 브랜치 생성

   ```
   git checkout --orphan ${orphan-branch-name}
   ```

2. Staged 상태인 모든 파일을 제거한다.

   ```
   git rm --cached -r .  // Unstage 상태로 변경
   git clean -f .   // 모든 파일 제거
   git clean -fd .   // 모든 폴더 제거
   ```

3. 브랜치를 커밋/푸시한다.

   ```
   git commit --allow-empty -m "initial commit"
   git push origin ${orphan-branch-name}
   ```

## worktree

동일한 저장소에 연결된 여러 작업 트리를 관리한다.
