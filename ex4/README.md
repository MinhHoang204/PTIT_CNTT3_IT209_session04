# Bài tập Session 04 - Ex4: .gitignore & git rm --cached
## Các bước thực hiện
### Bước 1: Tái hiện tình huống lỗi
Để thực hành, bạn giả lập lỗi commit nhầm file nhạy cảm như sau:
`echo "api_key=SECRET_123" > credentials.txt
git add credentials.txt
git commit -m "Add project files"`

Lúc này file credentials.txt đang nằm trong lịch sử commit của Git - cần xử lý ngay vì nếu push lên remote công khai, thông
tin bảo mật sẽ bị lộ 

### Bước 2: Gỡ bỏ file khỏi cache theo dõi - KHÔNG xóa vật lý 
Dùng lệnh git rm --cached để bỏ file khỏi vùng theo dõi của Git nhưng vẫn giữ nguyên file trên đĩa cứng:
`git rm --cached credentials.txt`

Ý nghĩa các tùy chọn:
* --cached: chỉ xóa file khỏi index/cache của Git, không đụng đến thư mục làm việc
* Nếu muốn bỏ cả một thư mục, thêm -r: git rm -r --cached ten_thu_muc/

### Bước 3: Cấu hình .gitignore để Git bỏ qua file này vĩnh viễn
1. Tạo file .gitignore và thêm tên file cần bỏ qua:
`echo "credentials.txt" >> .gitignore`

2. Thêm và commit file .gitignore cùng thay đổi gỡ bỏ:
`git add .gitignore
git commit -m "Remove credentials.txt from tracking and add .gitignore"`

### Bước 4: Sửa thông điệp commit gần nhất bằng --amend
Commit vừa tạo ở Bước 3 có message chưa "sạch" (vì vẫn còn dính dáng đến file bảo mật). Sửa lại bằng:
`git commit --amend -m "Update project config, ignore sensitive files"`

Giải thích:
* git commit --amend ghi đè lên commit cuối cùng, thay thế toàn bộ nội dung commit cũ
* Nếu chỉ muốn sửa message mà không đổi nội dung staged, dùng --amend như trên là đủ 

### Bước 5: Kiểm tra theo yêu cầu đề bài
**Kiểm tra trạng thái file:**
`git status`

Mong đợi: credentials.txt không xuất hiện trong danh sách Staged/Modified - file vẫn tồn tại trên máy nhưng Git không còn 
theo dõi.

**Kiểm tra commit gần nhất:**
`git log -n 1`

Mong đợi: Hiển thị commit với message đã sửa: `Update project config, ignore sensitive files`