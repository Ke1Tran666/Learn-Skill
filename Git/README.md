# Git & GitHub — Bảng tra nhanh

> Cheat sheet dùng để học nhanh và xử lý các tình huống Git/GitHub thường gặp trong project thực tế.

---

## 1. Quy trình Git cơ bản

```text
Working Directory
      |
      | git add
      v
Staging Area
      |
      | git commit
      v
Local Repository
      |
      | git push
      v
GitHub / Remote Repository
```

| Mục đích | Lệnh | Ghi chú |
|---|---|---|
| Xem trạng thái | `git status` | Lệnh nên dùng nhiều nhất |
| Xem file đã sửa gì | `git diff` | Xem thay đổi chưa stage |
| Đưa file vào staging | `git add <file>` | Stage 1 file |
| Stage toàn bộ | `git add .` | Cẩn thận file không mong muốn |
| Commit | `git commit -m "message"` | Tạo checkpoint |
| Xem lịch sử | `git log --oneline` | Dễ đọc hơn `git log` |
| Xem cây branch | `git log --oneline --graph --all` | Rất hữu ích khi branch phức tạp |

---

## 2. Branch

```text
main
 |
 A---B
      \
       C---D   feature/auth
```

| Mục đích | Lệnh |
|---|---|
| Xem branch local | `git branch` |
| Xem tất cả branch | `git branch -a` |
| Tạo branch | `git branch feature/auth` |
| Tạo và chuyển branch | `git switch -c feature/auth` |
| Chuyển branch | `git switch feature/auth` |
| Đổi tên branch | `git branch -m ten-moi` |
| Xóa branch local | `git branch -d feature/auth` |
| Xóa cưỡng chế branch local | `git branch -D feature/auth` |
| Xóa branch remote | `git push origin --delete feature/auth` |

### Workflow khuyên dùng

```bash
git switch main
git pull
git switch -c feature/ten-chuc-nang
```

Code xong:

```bash
git status
git add .
git commit -m "Add feature ..."
git push -u origin feature/ten-chuc-nang
```

Sau đó tạo **Pull Request** trên GitHub.

---

## 3. Remote / GitHub

| Mục đích | Lệnh |
|---|---|
| Xem remote | `git remote -v` |
| Thêm remote | `git remote add origin <url>` |
| Lấy thông tin mới từ GitHub | `git fetch` |
| Pull code mới | `git pull` |
| Push branch | `git push` |
| Push branch lần đầu | `git push -u origin <branch>` |
| Clone repository | `git clone <url>` |

### `fetch` khác `pull`

```text
git fetch
GitHub ---> origin/main
             |
             X  Không tự merge vào main local
```

```text
git pull
GitHub ---> fetch ---> merge/rebase ---> branch local
```

Khi chưa chắc chắn, nên:

```bash
git fetch
git status
git log --oneline --graph --all
```

rồi mới quyết định merge/rebase.

---

## 4. Merge

Giả sử:

```text
main
 A---B
      \
       C---D feature/login
```

Merge:

```bash
git switch main
git merge feature/login
```

Sau merge:

```text
A---B---C---D
            main
```

| Mục đích | Lệnh |
|---|---|
| Merge branch | `git merge <branch>` |
| Hủy merge đang conflict | `git merge --abort` |

---

## 5. Stash

Dùng khi đang sửa code nhưng chưa muốn commit mà cần đổi branch.

```text
Code đang sửa
     |
     | git stash
     v
   Kho tạm
     |
     | git stash pop
     v
Code trở lại
```

| Mục đích | Lệnh |
|---|---|
| Cất code tạm | `git stash` |
| Cất kèm mô tả | `git stash push -m "auth changes"` |
| Xem danh sách stash | `git stash list` |
| Lấy stash gần nhất và xóa khỏi list | `git stash pop` |
| Lấy stash nhưng giữ lại | `git stash apply` |
| Xóa một stash | `git stash drop stash@{0}` |
| Xóa toàn bộ stash | `git stash clear` |

---

## 6. Conflict

Git conflict thường có dạng:

```text
<<<<<<< HEAD
Code ở branch hiện tại
=======
Code từ branch đang merge
>>>>>>> feature/auth
```

Cách xử lý:

1. Mở file conflict.
2. Chọn code cần giữ.
3. Xóa các dòng:
   - `<<<<<<< HEAD`
   - `=======`
   - `>>>>>>> ...`
4. Kiểm tra code.
5. Stage file.
6. Tiếp tục thao tác Git.

Sau merge:

```bash
git add .
git commit
```

Sau cherry-pick:

```bash
git add .
git cherry-pick --continue
```

Sau rebase:

```bash
git add .
git rebase --continue
```

---

## 7. Undo / Khôi phục

| Tình huống | Lệnh | Mức độ |
|---|---|---|
| Bỏ thay đổi chưa `git add` | `git restore <file>` | An toàn nếu chắc không cần code |
| Bỏ file khỏi staging | `git restore --staged <file>` | Không mất code |
| Bỏ commit cuối, giữ code staged | `git reset --soft HEAD~1` | Khá an toàn |
| Bỏ commit cuối, giữ code unstaged | `git reset HEAD~1` | Khá an toàn |
| Xóa commit + code | `git reset --hard HEAD~1` | Nguy hiểm |
| Hoàn tác commit đã push | `git revert <commit>` | Khuyên dùng trên branch chung |

### Nguyên tắc

Nếu commit **đã push lên GitHub và người khác có thể đã pull**, ưu tiên:

```bash
git revert <commit>
```

Thay vì:

```bash
git reset --hard
git push --force
```

---

## 8. Cherry-pick

Dùng khi muốn lấy **một commit cụ thể** từ branch khác.

```text
feature/profile
A---B---C
        ^
        commit cần lấy

feature/auth
A---B
     |
     cherry-pick C
     v
A---B---C'
```

```bash
git switch feature/auth
git cherry-pick <commit-id>
```

Nếu conflict:

```bash
git add .
git cherry-pick --continue
```

Hủy cherry-pick:

```bash
git cherry-pick --abort
```

---

## 9. Rebase

Dùng để đưa commit của branch mình lên trên commit mới nhất của branch khác.

```text
Trước:

main:    A---B---C
              \
feature:       D---E

Sau rebase:

main:    A---B---C
                  \
                   D'---E'
```

```bash
git switch feature/auth
git fetch
git rebase origin/main
```

Nếu conflict:

```bash
git add .
git rebase --continue
```

Hủy:

```bash
git rebase --abort
```

> Không nên rebase tùy tiện branch chung mà nhiều người đang sử dụng.

---

# 10. Lỗi thường gặp và cách fix

## Lỗi: `non-fast-forward`

Ví dụ:

```text
! [rejected] main -> main (non-fast-forward)
```

### Nguyên nhân

Remote có commit mà local chưa có.

### Cách xử lý an toàn

```bash
git fetch
git status
git pull
```

Nếu conflict thì resolve conflict rồi commit.

Có thể dùng:

```bash
git pull --rebase
```

nếu workflow của team dùng rebase.

> Không dùng `git push --force` chỉ để "cho hết lỗi".

---

## Lỗi: local changes would be overwritten

Ví dụ:

```text
Your local changes to the following files would be overwritten by merge
```

### Nguyên nhân

Bạn đang sửa file nhưng Git cần ghi đè file đó khi pull/switch/merge.

### Cách 1 — Commit

```bash
git add .
git commit -m "WIP: save current changes"
git pull
```

### Cách 2 — Stash

```bash
git stash
git pull
git stash pop
```

---

## Lỗi: `CONFLICT (content)`

Ví dụ:

```text
CONFLICT (content): Merge conflict in src/App.jsx
```

### Fix

```bash
git status
```

Mở file conflict → sửa → sau đó:

```bash
git add src/App.jsx
git commit
```

Nếu muốn hủy merge:

```bash
git merge --abort
```

---

## Lỗi: `Unmerged paths`

Ví dụ:

```text
Unmerged paths:
  both modified: src/App.jsx
```

Nghĩa là conflict **chưa được resolve hoàn toàn**.

Fix:

```bash
git status
```

Sửa từng file conflict.

Sau đó:

```bash
git add <file>
```

Kiểm tra lại:

```bash
git status
```

---

## Lỗi sau `git stash pop`

Ví dụ:

```text
Auto-merging src/App.jsx
CONFLICT (content): Merge conflict in src/App.jsx
```

### Nguyên nhân

Code hiện tại và code trong stash sửa cùng khu vực.

### Fix

Resolve giống merge conflict:

```bash
git status
```

Sửa file → rồi:

```bash
git add .
```

Sau đó commit nếu cần:

```bash
git commit -m "Resolve stash conflicts"
```

---

## Lỗi: `detached HEAD`

Ví dụ:

```text
You are in 'detached HEAD' state
```

Thường do checkout trực tiếp commit:

```bash
git checkout abc123
```

### Nếu chỉ xem code

Quay lại branch:

```bash
git switch main
```

### Nếu đã code và muốn giữ

```bash
git switch -c feature/recover-work
```

Sau đó commit.

---

## Commit nhầm branch

Ví dụ commit đáng lẽ ở `feature/auth` nhưng lại commit trong `feature/profile`.

### Bước 1 — Lấy commit ID

```bash
git log --oneline
```

Ví dụ:

```text
abc123 Fix authentication
```

### Bước 2 — Chuyển sang đúng branch

```bash
git switch feature/auth
```

### Bước 3 — Cherry-pick

```bash
git cherry-pick abc123
```

### Bước 4 — Nếu muốn xóa commit khỏi branch cũ

Nếu chưa push:

```bash
git switch feature/profile
git reset --hard HEAD~1
```

Nếu đã push/public, cân nhắc `git revert`.

---

## Muốn hủy merge đang làm

```bash
git merge --abort
```

---

## Muốn hủy cherry-pick

```bash
git cherry-pick --abort
```

---

## Muốn hủy rebase

```bash
git rebase --abort
```

---

# 11. `git status` — lệnh cứu mạng

Trước khi làm thao tác nguy hiểm:

```bash
git status
```

Sau khi thao tác:

```bash
git status
```

Khi gặp lỗi:

```bash
git status
```

Nó cho biết:

- đang ở branch nào
- branch ahead/behind bao nhiêu commit
- file nào modified
- file nào staged
- file nào untracked
- file nào conflict
- có đang merge/rebase/cherry-pick không

---

# 12. Cây quyết định xử lý nhanh

```text
Gặp lỗi Git
   |
   v
git status
   |
   +--> Có modified chưa commit?
   |       |
   |       +--> Muốn giữ lâu dài -> commit
   |       |
   |       +--> Muốn cất tạm -> stash
   |
   +--> Có unmerged paths?
   |       |
   |       +--> Resolve conflict
   |              |
   |              +--> git add
   |
   +--> Đang merge?
   |       |
   |       +--> tiếp tục -> commit
   |       +--> hủy -> git merge --abort
   |
   +--> Đang rebase?
   |       |
   |       +--> git rebase --continue
   |       +--> git rebase --abort
   |
   +--> Đang cherry-pick?
           |
           +--> git cherry-pick --continue
           +--> git cherry-pick --abort
```

---

# 13. Workflow thực tế đề xuất

```text
GitHub main
    |
    | git pull
    v
Local main
    |
    | git switch -c feature/...
    v
Feature branch
    |
    | code
    | git add
    | git commit
    | git push
    v
GitHub feature branch
    |
    | Pull Request
    v
Review / Merge
    |
    v
GitHub main
```

Lệnh:

```bash
git switch main
git pull

git switch -c feature/auth-session

# Code...

git status
git add .
git commit -m "Add Spring Security session authentication"

git push -u origin feature/auth-session
```

Sau khi PR được merge:

```bash
git switch main
git pull
```

---

# 14. Những lệnh nên thuộc lòng

```bash
git status
git diff
git add .
git commit -m "..."
git log --oneline
git branch
git switch
git switch -c
git fetch
git pull
git push
git merge
git stash
git stash pop
```

Sau đó học:

```bash
git restore
git reset
git revert
git cherry-pick
git rebase
```

---

# 15. Bài thực hành

## Lab 1 — Commit cơ bản

```bash
mkdir git-practice
cd git-practice
git init
```

Tạo `README.md`, sau đó:

```bash
git status
git add README.md
git commit -m "Initial commit"
git log --oneline
```

---

## Lab 2 — Branch

```bash
git switch -c feature/login
```

Tạo:

```text
login.txt
```

Commit:

```bash
git add .
git commit -m "Add login feature"
```

---

## Lab 3 — Merge

```bash
git switch main
git merge feature/login
```

Xem:

```bash
git log --oneline --graph --all
```

---

## Lab 4 — Stash

Sửa `README.md` nhưng chưa commit:

```bash
git status
git stash
git status
git stash list
git stash pop
```

---

## Lab 5 — Conflict

Tạo 2 branch và sửa cùng một dòng trong cùng một file.

Sau đó merge để Git sinh conflict.

Yêu cầu:

```bash
git status
```

Resolve file rồi:

```bash
git add .
git commit
```

---

## Lab 6 — Commit nhầm branch

1. Commit một thay đổi ở branch A.
2. Lấy commit ID.
3. Chuyển branch B.
4. Dùng:

```bash
git cherry-pick <commit-id>
```

---

# 16. Checklist trước khi push

```text
[ ] git status
[ ] Đúng branch chưa?
[ ] Có file nhạy cảm (.env, password...) không?
[ ] git diff
[ ] Test code
[ ] Commit message rõ ràng
[ ] git push
[ ] Kiểm tra Pull Request
```

---

# 17. Quy tắc vàng

> **Không hiểu Git đang ở trạng thái nào → chạy `git status`.**

> **Không chắc remote có gì mới → `git fetch` trước.**

> **Code chưa muốn commit nhưng cần đổi branch → `git stash`.**

> **Commit nhầm branch → nghĩ đến `git cherry-pick`.**

> **Commit đã public → ưu tiên `git revert` thay vì sửa lịch sử.**

> **Không dùng `--force` khi chưa hiểu chính xác hậu quả.**

---

## Gợi ý cấu trúc branch

```text
main
├── feature/auth
├── feature/profile
├── feature/dashboard
├── feature/service-order
├── fix/login-session
└── refactor/api-client
```

Tên commit ví dụ:

```text
Add Spring Security session login
Fix profile API authentication
Refactor auth storage
Update service order table
Resolve login session conflict
```
