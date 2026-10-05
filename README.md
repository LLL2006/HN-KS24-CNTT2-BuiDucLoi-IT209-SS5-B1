# Báo Cáo Thực Hành: Khôi Phục Commit Đã Mất Bằng Git Reflog

## 1. Thông Tin Chung
- **Học viên:** Bùi Đức Lợi
- **Khóa học:** DevOps in Action
- **Bài tập:** Session 05 - Bài 1: Khôi phục commit đã mất bằng Git Reflog
- **Đường dẫn thư mục:** `homework/session_05/ex1/`

---

## 2. Mô Tả Bối Cảnh Sự Cố
- Học viên thực hiện chỉnh sửa mã nguồn và tạo commit: `"Them tinh nang quan trong"`.
- Do sơ suất khi thao tác, lệnh sau đã được thực thi trên Terminal:
  ```bash
  git reset --hard HEAD~1
Hậu quả:

Con trỏ HEAD và nhánh hiện tại bị lùi lại 1 commit.

File feature.txt bị xóa sạch khỏi Working Directory.

Lệnh git log --oneline không còn hiển thị commit chứa tính năng quan trọng vừa làm.

## 3. Giải Pháp Khôi Phục Bằng Git Reflog
### 3.1. Kiểm Tra Lịch Sử Hành Động
Để tìm lại "dấu vết" của commit đã mất, học viên sử dụng lệnh `git reflog`:

```bash
git reflog
```

**Kết quả:**
```
0251ce2 (HEAD -> master) HEAD@{0}: commit: Them tinh nang quan trong
f650e37 HEAD@{1}: commit: Initial commit
```

**Phân tích:**
* `0251ce2`: ID của commit chứa nội dung cần khôi phục.
* `HEAD@{0}`: Vị trí hiện tại (đã mất).
* `HEAD@{1}`: Vị trí ngay trước khi reset (vị trí cần quay lại).
### 3.2. Thực Hiện Khôi Phục
Học viên sử dụng commit ID tìm được từ reflog để đưa nhánh hiện tại về lại trạng thái trước đó.

```bash
git reset --hard 0251ce2
```
### 3.3. Xác Nhận Kết Quả
Sau khi reset, học viên kiểm tra lại trạng thái của dự án:

1. **Kiểm tra lịch sử commit:**
```bash
git log --oneline
```

**Kết quả:**
```
0251ce2 (HEAD -> master) Them tinh nang quan trong
f650e37 Initial commit
```
* *Nhận xét:* Commit chứa nội dung đã mất đã xuất hiện trở lại trong lịch sử.

2. **Kiểm tra nội dung file:**
```bash
cat feature.txt
```

**Kết quả:**
```
Day la tinh nang quan trong
```
* *Nhận xét:* Nội dung của file đã được khôi phục thành công.

---

## 4. Hậu Quả và Bài Học
**Hậu quả:**
* Con trỏ HEAD và nhánh hiện tại bị lùi lại 1 commit.
* File feature.txt bị xóa sạch khỏi Working Directory.
* Lệnh git log --oneline không còn hiển thị commit chứa tính năng quan trọng vừa làm.
