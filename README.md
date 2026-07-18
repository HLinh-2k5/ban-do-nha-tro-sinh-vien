# Bản đồ hỗ trợ tra cứu nhà trọ sinh viên

Website công khai hỗ trợ sinh viên tra cứu nhà trọ trong bán kính 20 km quanh Đại học Cần Thơ. Thông tin do Đoàn Thanh niên tổng hợp để tham khảo; website không phải nền tảng môi giới và không xử lý đặt cọc.

## Kiến trúc

- Giao diện tĩnh: GitHub Pages.
- Dữ liệu: Google Sheet được xuất bản công khai dưới dạng CSV.
- Bản đồ: Leaflet và nền bản đồ OpenStreetMap.
- Lọc, tìm kiếm và gom marker được xử lý ngay trên thiết bị người dùng.
- Không có tài khoản sinh viên, mật khẩu, cơ sở dữ liệu riêng hoặc khóa API trong mã nguồn.

## Các cột Google Sheet

Giữ nguyên tên cột, không đổi dấu hoặc thêm khoảng trắng:

```text
maTro,tenTro,trangThai,giaTien,diaChi,khuVuc,nguoiQuanLy,sdt,mayLanh,coGac,tongSoPhong,soPhongTrong,gioGiac,soNguoiToiDa,ngapKhiMua,ghiChuNgap,lat,lng,linkGoogleMaps,moTa,ngayCapNhat,kiemTraDuLieu
```

Giá trị khuyến nghị:

- `trangThai`: `Còn phòng`, `Hết phòng` hoặc `Tạm ẩn`.
- `mayLanh`, `coGac`: `Có` hoặc `Không`.
- `ngapKhiMua`: `Chưa xác minh`, `Không ghi nhận`, `Có thể ngập` hoặc `Thường ngập`.
- `ghiChuNgap`: mô tả ngắn nguồn xác minh và tình trạng thực tế, ví dụ `Ngập nhẹ trước hẻm sau mưa lớn, khảo sát 07/2026`.
- `giaTien`: chỉ nhập số, ví dụ `1500000`.
- `lat`, `lng`: nên định dạng hai cột là **Văn bản thuần túy** rồi dùng dấu chấm thập phân, ví dụ `10.029900` và `105.770600`. Website vẫn đọc được dấu phẩy thập phân nếu Google Sheet tự đổi theo vùng Việt Nam.

## Lấy tọa độ chính xác

1. Mở Google Maps trên máy tính và tìm đúng địa chỉ nhà trọ.
2. Phóng to, bấm chuột phải đúng vị trí cổng nhà trọ.
3. Bấm dòng tọa độ ở đầu menu để sao chép, ví dụ `10.029900, 105.770600`.
4. Nhập số thứ nhất vào cột `lat`, số thứ hai vào cột `lng`. Định dạng hai cột là **Văn bản thuần túy** để giữ nguyên tọa độ Google Maps.
5. Dán thêm liên kết đầy đủ vào `linkGoogleMaps`, rồi mở thử liên kết để đối chiếu trước khi công bố.

Liên kết rút gọn `maps.app.goo.gl` vẫn dùng cho nút chỉ đường, nhưng quản trị viên nên luôn nhập riêng `lat` và `lng` để ghim chính xác và để website kiểm tra bán kính 20 km.

## Quy trình cập nhật

1. Chỉ cấp quyền chỉnh sửa Google Sheet cho nhóm quản trị đã xác định.
2. Mỗi nhà trọ có một `maTro` duy nhất.
3. Kiểm tra tọa độ, số điện thoại, giá, trạng thái phòng, ngày cập nhật và tình trạng ngập trước khi đặt `kiemTraDuLieu` thành `Hợp lệ`.
4. Bật `Tự động xuất bản lại khi có thay đổi` trong phần **Tệp → Chia sẻ → Xuất bản lên web**.
5. Không đưa CCCD, tài khoản ngân hàng, giấy tờ cá nhân hoặc dữ liệu nội bộ vào Sheet công khai.

## An toàn vận hành

- Bật xác thực hai bước cho cả GitHub và Google.
- Giới hạn số người có quyền `Admin` trên GitHub; quản trị dữ liệu chỉ cần quyền sửa Sheet.
- Mỗi tháng tải một bản sao Sheet để dự phòng.
- Kiểm tra lịch sử thay đổi nếu dữ liệu bị sửa sai; thu hồi ngay quyền của thành viên rời nhóm.
- Không đặt mật khẩu, token hoặc khóa API trong `index.html` hay Google Sheet.
- Website dùng chính sách bảo mật nội dung, làm sạch dữ liệu trước khi hiển thị và chỉ chấp nhận liên kết Google Maps qua HTTPS.

## Triển khai

Thay `index.html` trong nhánh `main`. GitHub Pages sẽ tự triển khai sau vài phút. Khi kiểm tra bản mới, mở URL kèm tham số chống bộ nhớ đệm, ví dụ:

```text
https://hlinh-2k5.github.io/ban-do-nha-tro-sinh-vien/?v=20260719
```
