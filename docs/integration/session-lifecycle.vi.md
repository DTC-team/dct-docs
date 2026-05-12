# Vòng đời phiên

Shop cấp một cookie với `httpOnly`, `secure`, `sameSite=none`, `partitioned` khi handshake thành công.

| Thuộc tính | Giá trị |
|------------|---------|
| Thời hạn | **24 giờ** |
| Tự động làm mới trong thời hạn | Có (token API được làm mới trong suốt, không lộ ra ngoài) |
| Sau khi hết hạn | Shop chuyển hướng về `/sign-in` của chính nó — là ngõ cụt với người dùng đang được nhúng từ đối tác |

## Hành vi khuyến nghị cho đối tác (v1)

> Mở Shop bằng một URL handshake **vừa tạo mới** mỗi lần người dùng vào giao diện Shop trong ứng dụng của bạn. Không cache URL hay phụ thuộc vào phiên được giữ qua các lần khởi động ứng dụng.

## Lộ trình

Một sự kiện `shop.auth_expired` (`postMessage` cho `iframe`, JS bridge cho `WebView`) sẽ cho phép host đối tác thực hiện lại handshake mà không gây gián đoạn nhìn thấy được với người dùng. Chưa cam kết thời điểm.
