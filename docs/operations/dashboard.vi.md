# Bảng điều khiển đối tác

Bluecom cấp cho mỗi đối tác một tài khoản trên **Bluecom Marketplace** — bảng điều khiển web để giám sát toàn bộ quá trình tích hợp của bạn. Bạn nhận thông tin đăng nhập tại bước 3 của [onboarding](../onboarding/checklist.md).

## Truy cập

| Mục | Giá trị |
|-----|---------|
| URL | `<TBD: marketplace host>` |
| Xác thực | Email + mật khẩu (Better Auth) |
| Cấp tài khoản | Bộ phận vận hành Bluecom tạo một tài khoản admin cho mỗi đối tác; bạn mời thành viên qua **Members** |
| Trình duyệt khuyến nghị | Chromium-based, Firefox, Safari (2 phiên bản mới nhất) |

## Bên trong có gì

Thanh sidebar ánh xạ tới các khu vực vận hành của tích hợp.

| Mục | Hiển thị gì | Ai sử dụng |
|-----|-------------|-----------|
| **Dashboard** | Thanh toán đang chờ, tồn kho eSIM, số đã kích hoạt và đang sử dụng; doanh thu/chi phí/lợi nhuận theo kỳ (7/30/90 ngày, theo quý); bảng xếp hạng (top quốc gia, sản phẩm, thành viên) | Chủ doanh nghiệp, trưởng nhóm vận hành |
| **Products** | Danh mục các gói có sẵn cho kênh của bạn — quốc gia, dung lượng, thời hạn, giá | Sản phẩm, hỗ trợ |
| **eSIM** | Tồn kho eSIM theo từng đơn vị và trạng thái vòng đời | Vận hành, hỗ trợ |
| **Insurance** | Bảo hiểm du lịch bổ sung (nếu bật trên kênh của bạn) | Sản phẩm |
| **Customers** | Người dùng cuối đến qua `partnerCode` của bạn | Hỗ trợ, CX |
| **Orders** | Danh sách đơn và chi tiết từng đơn (trạng thái, thanh toán, fulfilment, kích hoạt) | Hỗ trợ, tài chính |
| **Distribution log** | Nhật ký kiểm toán cho việc cấp phát và giao eSIM | Vận hành |
| **Members** | Quản lý tài khoản marketplace của đội bạn | Admin |
| **Storefront** | Cấu hình storefront gắn với `partnerCode` của bạn | Admin |
| **Webview Insights** | Phễu chuyển đổi và doanh thu từ Shop nhúng — xem bên dưới | Tăng trưởng, analytics |

Thanh trên cùng hiển thị **Balance** hiện tại và đơn vị tiền tệ. Việc nạp thêm được thu xếp với bộ phận vận hành Bluecom.

## Webview Insights — góc nhìn cho tích hợp

Được xây dựng riêng cho các đối tác chạy Shop nhúng. Trang này hiển thị phễu chuyển đổi từ traffic của bạn, không phải traffic tổng của Bluecom.

**Các bước trong phễu:**

1. **Phiên truy cập** — Số phiên được mở (bắt tay thành công).
2. **Ý định mua** — Ý định mua hàng (sự kiện `shop.purchase_intent`).
3. **Đơn đã thanh toán** — Số đơn đã thanh toán.
4. **Đã kích hoạt** — Số eSIM đã kích hoạt.

**Tỷ lệ phái sinh:** tỷ lệ ý định, tỷ lệ chuyển đổi, tỷ lệ kích hoạt.

**Bảng doanh thu:** tổng số đơn và doanh thu chia theo đơn vị tiền tệ.

**Biểu đồ traffic:** số phiên theo thời gian, có thể so sánh theo bộ chọn kỳ.

Cùng một `partnerCode` vận hành cả handshake của Shop lẫn bộ lọc Webview Insights — nên những gì bạn thấy chính xác là những gì người dùng của bạn đã làm.

## Tự phục vụ sau go-live

- Mời thành viên → **Members** → Invite.
- Đổi ngôn ngữ (giao diện `vi` / `en`) → menu người dùng ở góc trên phải.
- Xuất danh sách đơn → **Orders** → lọc → Export (CSV).
- Kiểm tra một người dùng cụ thể đã thanh toán hay chưa → **Customers** → tìm kiếm → lịch sử đơn hàng.

Với những gì chưa expose trên UI, xem [Hỗ trợ](support.md).
