

---

# 📝 GitHub 계정 두 개(회사/개인) 사용 기록

## 1. SSH 키 구조

- 회사 계정: `~/.ssh/id_ed25519`
    
- 개인 계정: `~/.ssh/personal_git_key`
    

### `~/.ssh/config`

```text
# 회사 계정
Host github-company
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519

# 개인 계정
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/personal_git_key
```

---

## 2. 연결 테스트

```bash
ssh -T github-company     # → Hi kim-aforce!
ssh -T github-personal    # → Hi younnieCutler!
```

---

## 3. Repo Clone 방법

- 회사 저장소:
    

```bash
git clone git@github-company:kim-aforce/레포.git
```

- 개인 저장소:
    

```bash
git clone git@github-personal:younnieCutler/레포.git
```

---

## 4. 저장소별 사용자 설정

```bash
# 회사 repo에서
git config user.name "kim-aforce"
git config user.email "aforcekim@gmail.com"

# 개인 repo에서
git config user.name "younnieCutler"
git config user.email "ehrktm090@gmail.com"
```

확인:

```bash
git config user.name
git config user.email
```

---

## 5. 전역 기본값(Global) 변경 (선택)

회사 계정을 기본으로 쓰고 싶다면:

```bash
git config --global user.name "kim-aforce"
git config --global user.email "aforcekim@gmail.com"
```

개인 레포 안에서는 위에서 설명한 방식으로 `local` 설정만 덮어쓰면 됨.

---

## 6. 계정 전환 요약

1. **clone 시점** → SSH Host 선택 (`github-company` or `github-personal`)
    
2. **커밋 사용자 정보** → 저장소별 `git config user.email` 확인/수정
    
3. **푸시 시점** → `git push` 하면 자동으로 해당 Host + 해당 계정으로 동작
    

---

👉 이렇게 기록해두면, 나중에 계정 꼬임 생겨도 “1) clone 할 때 host 확인, 2) repo 내부 user.email 확인”만 보면 해결 가능합니다.


## 2. 사용법

레포 디렉토리 안에서:

`git use-company`

→ 회사 계정(`kim-aforce`, `aforcekim@gmail.com`)으로 전환

`git use-personal`

→ 개인 계정(`younnieCutler`, `ehrktm090@gmail.com`)으로 전환

git remote set-url origin git@github-personal:younnieCutler/레포이름.git
회사 레포라면:

bash
코드 복사
git remote set-url origin git@github-company:kim-aforce/레포이름.git