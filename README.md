# Bài 8: Chữa Lỗi Bảng Đăng Ký Báo Cáo Viên Không Lọc Được
## *Phần 1: Phân tích lỗi*
### 1. Xác định các lỗi trong bảng
| Vị trí |	Lỗi vi phạm |	Quy tắc |	Hậu quả|
|---|---|---|---|
| A1:E1 |	Tiêu đề bảng nằm chung trong vùng dữ liệu |	Quy tắc 1 |	AutoFilter có thể nhận nhầm tiêu đề bảng là tên cột.|
| Hàng 2–3 |	Có các hàng trống giữa dữ liệu |	Quy tắc 4 |	AutoFilter có thể chỉ nhận một phần dữ liệu, khiến kết quả lọc bị thiếu.|
| A4:E4 |	Hàng chứa “TỔNG SỐ CNTT: 45” nằm trong bảng	| Quy tắc 5 |	Hàng tổng bị xem như một bản ghi không đầy đủ, gây sai lệch khi lọc.|
| B3 |	Tên “Trần Thị Bình” có khoảng trắng thừa ở cuối |	Quy tắc 3 (làm sạch dữ liệu trong một cột) |	Dữ liệu không thống nhất, có thể gây khó khăn khi tìm kiếm và so sánh chuỗi.|
### 2. Tại sao khoảng trắng cuối tên gây lỗi lọc?
- Ô B3 chứa Trần Thị Bình   có khoảng trắng ở cuối, trong khi giá trị cần tìm là Trần Thị Bình.
- Excel và Google Sheets so sánh nội dung chuỗi ký tự. Khoảng trắng thừa có thể khiến hai giá trị được xem là khác nhau, làm cho việc tìm kiếm hoặc lọc theo điều kiện chính xác không khớp như mong muốn.
- Cách khắc phục là sử dụng hàm TRIM() để loại bỏ khoảng trắng thừa.
## *Phần 2: Sửa lỗi & Nghiệm thu*
### 1. Vẽ lại cấu trúc bảng đúng chuẩn
| STT | Họ và tên | Khoa / Viện | Điểm xét duyệt | Trạng thái xét duyệt|
|---|---|---|---|---|
| 1 |	Nguyễn Văn An |	CNTT |	8.5 |	Đã duyệt|
| 2 |	Trần Thị Bình |	CNTT | 7.9 |	Chờ duyệt|
| 3 |	Lê Minh Châu |	Điện tử |	8.2 |	Đã duyệt|

Cách sửa:
- **Hàng đầu tiên:** Chỉ chứa tên các cột, không gộp ô.
- **Mỗi hàng:** Chứa thông tin của một báo cáo viên.
- **Mỗi cột:** Chỉ chứa một loại thông tin.
- **Hàng trống:** Xóa các hàng trống nằm giữa dữ liệu.
- **Hàng tổng:** Chuyển dòng “TỔNG SỐ CNTT: 45” ra ngoài vùng dữ liệu, ví dụ đặt bên dưới bảng và cách bảng bằng một hàng trống.
### 2. Dùng TRIM() và lọc dữ liệu chính xác
**Bước 1: Làm sạch cột Họ và Tên**
Giả sử dữ liệu bắt đầu từ ô B2, nhập công thức vào một cột phụ, ví dụ F2:
```excel
=TRIM(B2)
```
Sau đó kéo công thức xuống hết danh sách 120 báo cáo viên.
Nếu muốn thay thế dữ liệu cũ, sao chép cột đã làm sạch, chọn cột B và dùng Paste special → Values only

**Bước 2: Bật bộ lọc**
- Chọn toàn bộ bảng dữ liệu, bao gồm hàng tiêu đề và 120 bản ghi, không chọn hàng tổng.
- Nhấn Ctrl + Shift + L trong Excel hoặc chọn Data → Create a filter trong Google Sheets.

**Bước 3: Lọc theo hai điều kiện**
- Cột Khoa / Viện: Chỉ chọn CNTT.
- Cột Điểm Xét Duyệt: Chọn điều kiện lớn hơn hoặc bằng 8.0.

Hai điều kiện được áp dụng đồng thời, nghĩa là báo cáo viên phải vừa thuộc khoa CNTT, vừa có điểm xét duyệt từ 8.0 trở lên.
**Bước 4: Nghiệm thu**

Kiểm tra kết quả lọc, bảo đảm không còn hàng tiêu đề phụ, hàng trống hoặc hàng tổng trong vùng dữ liệu. Số kết quả thực tế có thể khác dự kiến khoảng 35 người vì còn phụ thuộc vào dữ liệu thật.
