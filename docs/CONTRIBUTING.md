# Quy trình làm việc với Git & GitHub

Tài liệu này mô tả cách hai thành viên đưa code vào repo FoodMap. Áp dụng cho mọi thay đổi: code, layout, tài liệu.

## Vì sao phải làm như vậy

`main` là bản chính thức của app và **luôn phải build được** (giảng viên chấm trên đó). Ruleset **"Protect main"** trên GitHub chặn mọi thay đổi vào `main` trừ khi có đủ:

1. Thay đổi đi qua **Pull Request** (không push thẳng được).
2. **CI xanh**: job `build` tự build APK debug và chạy unit test.
3. **1 approval** của thành viên còn lại, và mọi comment review đã được resolve.
4. Nhánh đã **cập nhật theo `main` mới nhất**.

Ngoài ra ruleset còn cấm force-push và cấm xoá `main`. Repo chỉ cho phép **Merge commit** (không squash, không rebase) để mọi commit của từng thành viên đều nằm trên `main`, vì môn học chấm lịch sử commit. Nhánh tự bị xoá sau khi merge.

## Tóm tắt

```
pull main → switch -c feature/x → code + commit → push -u → mở PR
→ CI xanh → người kia approve → Merge pull request → switch main + pull → xoá nhánh cũ
```

## Các bước chi tiết

### 1. Lấy `main` mới nhất

Có thể người kia vừa merge một PR, nên luôn bắt đầu từ bản mới nhất.

```bash
git switch main
git pull
```

### 2. Tạo nhánh cho tính năng

Tên nhánh: `feature/<tên-ngắn>`, viết thường, nối bằng `-`. **Mỗi nhánh một tính năng.**

```bash
git switch -c feature/checkin-camera
```

Lệnh này tạo nhánh mới từ `main` và chuyển sang nhánh đó. Từ đây mọi commit nằm trên nhánh mới, `main` không bị ảnh hưởng.

### 3. Code và commit thường xuyên

Mỗi phần nhỏ chạy được thì commit một lần. Môn học chấm lịch sử commit, và mỗi người phải có commit của chính mình.

```bash
git add .
git commit -m "feat(checkin): open CameraX preview"
```

Định dạng message: `<type>(<scope>): <summary>`

| type | Dùng khi |
|---|---|
| `feat` | Thêm tính năng |
| `fix` | Sửa lỗi |
| `refactor` | Sắp xếp lại code, không đổi hành vi |
| `docs` | Tài liệu |
| `test` | Thêm / sửa test |
| `chore` | Cấu hình, build, CI |

`scope` là phần bị ảnh hưởng, ví dụ `checkin`, `search`, `room`, `readme`.

Trước khi push, nên tự build và test ở máy để CI không báo đỏ:

```bash
./gradlew assembleDebug testDebugUnitTest     # Windows: .\gradlew.bat assembleDebug testDebugUnitTest
```

### 4. Push nhánh lên GitHub

```bash
git push -u origin feature/checkin-camera     # lần đầu
git push                                      # các lần sau
```

> `git push origin main` sẽ bị từ chối ("Changes must be made through a pull request"). Đó là ruleset đang hoạt động đúng.

### 5. Mở Pull Request

- **Trên web:** vào repo, bấm **Compare & pull request** trên banner vàng.
- **Bằng lệnh:** `gh pr create --base main --title "feat(checkin): capture photo with CameraX"`

**Tiêu đề PR sẽ thành tiêu đề của merge commit trên `main`**, nên phải viết đúng định dạng `type(scope): summary`. Message của từng commit trong nhánh cũng lên `main` nguyên vẹn, vì vậy hãy viết chúng cẩn thận ngay từ bước 3.

Mô tả PR viết bằng tiếng Việt, gồm:

- Đã thay đổi gì.
- Cách test trên emulator.
- Có đụng file dùng chung không (`entity/`, `dao/`, `AppDatabase`, `util/`). Nếu có, người kia phải review kỹ.
- Luồng chính mà mình phải giải thích được khi vấn đáp.

### 6. CI tự chạy

Mỗi lần mở PR hoặc push thêm commit, GitHub Actions chạy job `build` (workflow `.github/workflows/android-ci.yml`).

- ✅ Xanh: đạt.
- ❌ Đỏ: bấm **Details** để xem log, sửa trên **chính nhánh đó**, commit rồi `git push`. CI sẽ chạy lại, không cần mở PR mới.

### 7. Review và approve

Người review mở tab **Files changed**, comment vào từng dòng nếu cần, rồi bấm **Review changes** và chọn:

- **Comment:** chỉ góp ý.
- **Request changes:** yêu cầu sửa.
- **Approve:** đồng ý merge.

Lưu ý:

- **Không tự approve PR của mình được**, phải là người kia.
- Mọi luồng comment phải được **Resolve conversation** trước khi merge.
- **Push thêm commit sau khi đã được approve thì approval cũ bị huỷ**, phải xin duyệt lại.

### 8. Merge pull request

Khi đủ điều kiện, nút **Merge pull request** chuyển xanh. Bấm vào rồi **Confirm merge**. Mọi commit của nhánh được đưa lên `main` nguyên vẹn (giữ tác giả và thời gian), kèm thêm 1 merge commit đánh dấu PR. Nhờ vậy trang Commits và Contributors của repo thể hiện đúng đóng góp của từng người.

Nhánh trên GitHub tự bị xoá sau khi merge. Nếu bật **Auto-merge** trên PR, GitHub sẽ tự merge ngay khi đủ điều kiện.

### 9. Dọn dẹp ở máy

```bash
git switch main
git pull
git branch -d feature/checkin-camera    # xoá nhánh đã merge ở máy
git fetch --prune                       # xoá các nhánh remote đã bị xoá khỏi danh sách
```

Quay lại bước 2 cho tính năng tiếp theo.

## Tình huống hay gặp

### `main` có thay đổi mới khi đang làm nhánh

PR sẽ báo nhánh đã cũ. Bấm **Update branch** trên PR, hoặc làm ở máy:

```bash
git fetch
git merge origin/main
git push
```

### Bị conflict

Git đánh dấu chỗ xung đột bằng `<<<<<<<`, `=======`, `>>>>>>>`. Mở bằng Android Studio (**Git → Resolve Conflicts**), chọn phần cần giữ, rồi:

```bash
git add .
git commit
git push
```

Chia việc theo feature (`ui/checkin` của Đạt; `ui/home`, `ui/search`, `ui/restaurant`, `ui/favorite` của Diễn) giúp hạn chế conflict. Conflict thường chỉ xảy ra ở file dùng chung, nên khi sửa các file đó hãy báo trước cho người kia.

### Lỡ commit thẳng vào `main` ở máy

Push sẽ bị từ chối, nhưng commit vẫn nằm trong `main` ở máy. Chuyển nó sang nhánh mới:

```bash
git switch -c feature/ten-tinh-nang     # nhánh mới giữ commit đó
git branch -f main origin/main          # đưa main ở máy về đúng bản trên GitHub
git push -u origin feature/ten-tinh-nang
```

Sau đó mở PR như bình thường.

### Cần merge gấp khi người kia chưa duyệt được

Admin repo có ô **"Merge without waiting for requirements to be met (bypass rules)"** trên PR. Ô này bỏ qua **cả CI**, nên chỉ dùng khi CI đã xanh và thật sự gấp (ví dụ sát hạn nộp). Không dùng thường xuyên, vì lịch sử review là bằng chứng làm việc nhóm.

## Không bao giờ commit

- `local.properties`, API key, `google-services.json`, file keystore (`*.jks`, `*.keystore`).
- Thư mục `build/`, `.gradle/`, `.idea/` (đã có trong `.gitignore`).
