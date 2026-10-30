# BẢN ĐẶC TẢ KHÔNG GIAN CỘNG TÁC DỰ ÁN TRANG TRẠI THÔNG MINH (GREEN-TECH)



## PHẦN 1: README.MD — CẤU TRÚC LƯU TRỮ VÀ PHÂN QUYỀN

### 1. Cấu trúc Thư mục Dự án (Hybrid Workflow & Storage)

Dự án áp dụng mô hình **Hybrid Workflow** (kết hợp lưu trữ cục bộ Local SSD và tự động đồng bộ Cloud với tính năng *Files On-Demand* để tối ưu hóa dung lượng ổ cứng, đồng thời lưu trữ lịch sử phiên bản để phòng ngừa rủi ro phần cứng):

```text
green-tech-smart-farm/
├── docs/                 # Tài liệu kỹ thuật, SRS, hướng dẫn vận hành
├── src/                  # Mã nguồn phần mềm và firmware cảm biến (Folder sensors/ nằm ở đây)
├── data/                 # Dữ liệu thu thập và tệp cấu hình bảo mật (.env)
├── config/               # Cấu hình hệ thống và thông số phần cứng
└── backup/               # Bản sao lưu dự phòng định kỳ

```

### 2. Quy định Phân quyền Truy cập (Access Control & Permissions)

* **Mã nguồn và Cấu hình bảo mật (`src/`, `.env`):**
* **Chủ sở hữu (Owner):** Trưởng dự án (Project Manager / Tech Lead).
* **Đội ngũ Kỹ thuật (Dev Team):** Quyền `Editor` (Chỉnh sửa trực tiếp, quản lý mã nguồn).
* **Bảo mật tệp `.env`:** Chứa mật khẩu cảm biến và API keys, thiết lập **Restricted** tuyệt đối, chỉ Dev Team mới có quyền truy cập, **tuyệt đối không** chia sẻ dưới mọi hình thức bên ngoài hoặc cấp quyền mở rộng.


* **Báo cáo tài chính & Tiến độ cho Nhà đầu tư (Investor):**
* Mức quyền: **Viewer (Chỉ xem)**, phạm vi **Restricted** (chia sẻ theo email định danh), bật tính năng chặn tải xuống/sao chép đối với tài liệu nhạy cảm chiến lược.


* **Đối tác cung cấp thiết bị (Supplier):**
* Mức quyền: **Commenter (Nhận xét / Góp ý)**, phạm vi **Restricted**, kết hợp sử dụng chế độ đề xuất (*Suggesting Mode*) để góp ý kỹ thuật thông số cảm biến mà không làm thay đổi trực tiếp file gốc.


* **Bàn giao dự án (Transfer Ownership):** Khi bài tập nhóm kết thúc hoặc hoàn thành giai đoạn bàn giao, Trưởng dự án thực hiện thao tác **Transfer Ownership** file/thư mục gốc sang tài khoản của giảng viên hoặc người quản lý kế tiếp trong cửa sổ *Share Settings*.

### 3. Cấu trúc Kênh Giao tiếp (Enterprise Communication Channels)

Áp dụng văn hóa giao tiếp bất đồng bộ (Asynchronous Communication) và chống trôi tin nhắn trên Lark/Slack:

* **`#01-thong-bao-chung`**: Phát sóng thông báo cốt lõi, deadline, quyết định của trưởng nhóm (Chỉ Admin/Trưởng nhóm được đăng bài để tránh nhiễu thông tin).
* **`#02-ky-thuat-cam-bien`**: Thảo luận chuyên sâu về code cảm biến, xử lý bug, kết nối phần cứng (Sử dụng tính năng *Reply in Thread* để giữ khung chat sạch đẹp).
* **`#03-quan-ly-task`**: Theo dõi công việc, tích hợp chuyển tin nhắn thảo luận thành Task có Deadline bằng 1-click.
* **`#04-giai-tri-watercooler`**: Nơi chia sẻ thông tin ngoài lề, memes, giải trí xả stress của nhóm.

---

## PHẦN 2: KIỂM THỬ — QUY TRÌNH KHÔI PHỤC NHANH KHI XÓA NHẦM FOLDER `SENSORS`

Giả định một thành viên trong lúc dọn dẹp thư mục mã nguồn đã lỡ tay xóa sạch folder `sensors` (chứa toàn bộ mã nguồn cảm biến quan trọng của dự án). Quy trình khôi phục nhanh chóng và an toàn nhất được thực hiện qua các bước sau:

1. **Khôi phục trực tiếp từ Thùng rác Cloud (Cloud Trash Bin / Recycle Bin):**
* Truy cập vào giao diện Web của Cloud Workspace (Google Drive / OneDrive).
* Mở mục **Thùng rác (Trash / Recycle Bin)** ở thanh menu bên trái.
* Tìm đến folder `sensors` vừa bị xóa nhầm, nhấp chuột phải và chọn **Khôi phục (Restore)**. Hệ thống sẽ tự động đưa folder trở lại đúng vị trí ban đầu trong thư mục `src/` cùng toàn bộ cấu trúc file bên trong.


2. **Đồng bộ ngược về Local (Auto Sync Recovery):**
* Ngay sau khi folder được khôi phục thành công trên Cloud, ứng dụng đồng bộ tự động (*Auto Sync*) chạy ngầm trên máy tính của các thành viên sẽ nhận diện thay đổi và tự động tải lại (Sync down) toàn bộ folder `sensors` về ổ cứng Local SSD, đảm bảo tiến độ code của đội ngũ kỹ thuật không bị gián đoạn.


3. **Kiểm tra Lịch sử Phiên bản (Version History) nếu file bị chỉnh sửa đè:**
* Trong trường hợp file mã nguồn bên trong bị lỗi do xung đột phiên bản, nhấp chuột phải vào file code, chọn **Lịch sử phiên bản (Version history)** và chọn mốc thời gian ổn định trước khi xảy ra sự cố để khôi phục nhanh chóng.