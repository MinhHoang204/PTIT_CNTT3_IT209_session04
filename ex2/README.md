# Bài tập Session 04 - Ex2: Branch Management & Merge Conflict
## Các bước đã thực hiện
### Bước 1: Chuẩn bị lại môi trường thực hành
Nếu bạn đang ở thư mục dự án từ Bài 1, hãy tạo thư mục mới cho Bài 2 để track riêng (không bị lẫn với lịch sử cũ):
`mkdir ex2
cd ex2
git init`

### Bước 2: Tạo file README.md và commit khởi tạo trên nhánh main
1. Tạo file README.md với nội dung gốc:
`echo "Hello World" > README.md`

2. Thêm và commit trên nhánh main:
`git add README.md
git commit -m "Base commit, create README on main"`

Nhánh mặc định lúc này là main (hoặc master tùy cấu hình máy, hãy dùng đúng tên nhánh hệ thống của bạn).

### Bước 3: Tạo nhánh feature-update và tách khỏi main
`git branch feature-update
git checkout feature-update`

Lúc này bạn đang đứng trên nhánh feature-update, cả hai nhánh đều trỏ về commit khởi tạo.

### Bước 4: Thay đổi README.md trên nhánh feature-update (gây nền cho xung đột)
1. Chỉnh sửa nội dung README.md, đổi "Hello World" thành "Hello from feature branch":
`echo "Hello from feature branch" > README.md`

2. Commit thay đổi trên nhánh feature-update:
`git add README.md
git commit -m "Update README in feature-update branch"`

### Bước 5: Quay lại nhánh main và thay đổi CÙNG DÒNG đó
1. Chuyển về nhánh main:
`git checkout main`

2. Sửa README.md thành nội dung khác, cùng vị trí dòng:
`echo "Hello from main branch" > README.md`

3. Commit thay đổi này trên nhánh main:
`git add README.md
git commit -m "Update README in main branch"`

Đây chính là điểm mấu chốt tạo ra xung đột: cả hai nhánh cùng sửa nội dung dòng đầu tiên của cùng một file.

### Bước 6: Thực hiện Merge và ghi nhận Conflict
1. Đứng ở nhánh main (đã chuyển từ bước 5), gộp nhánh feature-update vào:
`git merge feature-update`

2. Kết quả mong đợi - Git báo xung đột:
```text
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

### Bước 7: Xử lý Conflict THỦ CÔNG bắt buộc theo yêu cầu 
Đây là ràng buộc quan trọng nhất: bạn không được dùng các nút tự động "Accept Current/Incoming/Both" của IDE, mà phải sửa
trực tiếp các ký hiệu đánh dấu trong file.

1. Mở file README.md bằng trình soạn thảo, bạn sẽ thấy:
```text
<<<<<<< HEAD
Hello from main branch
=======
Hello from feature branch
>>>>>>> feature-update
```

2. Xác định ý nghĩa:
  * `<<<<<<<` HEAD: phần code đang có trên nhánh main (nhánh hiện tại)
  * `=======`: dấu phân cách giữa hai phiên bản
  * `>>>>>>>` feature-update: phần code từ nhánh feature-update đang được merge vào 

3. Quyết định giữ phần nào. Ví dụ: giữ cả hai nội dung, kết hợp thành:
```text
Hello from main branch
Hello from feature branch  
```

4. Xóa hoàn toàn các dòng marker `<<<<<<<, =======, >>>>>>>`, chỉ giữ lại nội dung đã chọn.

### Bước 8: Đánh dấu đã giải quyết và hoàn tất commit gộp
1. Kiểm tra trạng thái và thêm file đã xử lý vào staging:
`git status
git add README.md`

2. Tạo commit gộp (merge commit) để hoàn tất:
`git commit -m "Merge branch feature-update into main, resolve conflict manually"`