# git

## orphan branch

### 정의

하나의 저장소에서 다른 브랜치나 커밋으로부터 단절된 새로운 history를 가지는 브랜치를 의미한다.
다른 브랜치와 독립적으로 운영할 수 있다.

### 생성 방법

1. 브랜치 생성

   ```bash
   git checkout --orphan ${orphan-branch-name}
   ```

2. Staged 상태인 모든 파일을 제거한다.

   ```bash
   git rm --cached -r .  // Unstage 상태로 변경
   git clean -f .   // 모든 파일 제거
   git clean -fd .   // 모든 폴더 제거
   ```

3. 브랜치를 커밋/푸시한다.

   ```bash
   git commit --allow-empty -m "initial commit"
   git push origin ${orphan-branch-name}
   ```

## worktree

동일한 저장소에 연결된 여러 작업 트리를 관리한다.

## 파일명 대소문자 변경 방법

git은 파일명의 대소문자가 변경될 경우 인식하지 못한다. 해결방법은 아래 두가지이다. 
   
1. git에서 대소문자를 인식하게 변경 
   ```bash 
     git config core.ignorecase false
   ```
2. git mv로 파일명 변경 
   ```bash 
     git mv App.tsx app.tsx 
   ```
## git repository 별로 config 설정하기 

```bash
   git config --local user.name "name"
   git config --local uesr.email "email@gmail.com"
   git config --local --list // 확인하기 
```