# Bài tập Session 04 - Ex1: Local Repository & Identity Config
## Danh sách lệnh đã thực hiện
### Bước 1: Chuẩn bị thư mục làm việc 
1. Mở Terminal / Git Bash tại thư mục bạn muốn chứa dự án
2. Tạo thư mục mới cho bài tập và di chuyển vào đó:
`mkdir session_04_ex1
cd session_04_ex1`

### Bước 2: Khởi tạo Local Git Repository
Chạy lệnh sau để khởi tạo kho Git trống trong thư mục hiện tại:
`git init`

Kết quả mong đợi: Hiển thị thông báo Initialized empty Git repository in <đường dẫn thư mục>/.git/

### Bước 3: Cấu hình danh tính tác giả cấp độ Local 
Tuân thủ nghiêm ngặt yêu cầu không dùng --global, chỉ cấu hình áp dụng cho riêng kho này:
`git config --local user.name "Tên của bạn"
git config --local user.email "email.cua.ban@example.com"`

Nếu bạn bỏ qua tham số --local, Git mặc định vẫn sẽ lưu cấu hình ở cấp độ local khi bạn đang đứng trong thư mục repo, tuy
nhiên ghi rõ --local để đảm bảo không ảnh hưởng đến cấu hình chung của máy tính

### Bước 4: Kiểm tra cấu hình đã thiết lập
Chạy các lệnh kiểm tra theo yêu cầu đề bài:
```aiignore
# Kiểm tra tên tác giả local
git config --local user.name

# Kiểm tra email tác giả local
git config --local user.email

# Xem toàn bộ cấu hình local của repo
git config --local --list
```

Kết quả mong đợi: Các lệnh in ra chính xác tên và email bạn vừa khai báo, không có giá trị mặc định từ cấu hình global.

### Bước 5: Tạo tệp tin đầu tiên, thêm vào Staging Area và Commit
1. Tạo tệp tin mới bất kỳ trong thư mục dự án, ví dụ README.md:
`echo "# Bài tập Git Session 04 - Ex1" > README.md`
2. Kiểm tra trạng thái thư mục làm việc:
`git status`
3. Thêm tệp vào vùng chuẩn bị:
`git add README.md`
4. Tiến hành commit đầu tiên với thông điệp rõ nghĩa:
`git commit -m "Initial commit, add project README"`

### Bước 6: Xác nhận lịch sử Commit
Chạy lệnh xem lịch sử commit theo định dạng tắt:
`git log --oneline`