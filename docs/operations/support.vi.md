# Hỗ trợ

| Kênh | Liên hệ |
|------|---------|
| Onboarding & nghiệp vụ | `integration@bluecom.com.vn` |
| Sự cố kỹ thuật / production | `<TBD ops contact>` |
| Trang trạng thái | `<TBD>` |

## Cần đưa gì vào báo cáo sự cố

- `partnerCode` và môi trường (staging / production).
- Timestamp (kèm timezone) của request bị lỗi.
- `userId` (trong hệ thống của bạn) liên quan, nếu có.
- HTTP status và error code từ phản hồi.
- User-agent của trình duyệt/WebView (cho các sự cố phía client).

Việc này rút ngắn thời gian triage đáng kể — Bluecom có thể đối chiếu với `auth_provider_configs` và log của dịch vụ auth.
