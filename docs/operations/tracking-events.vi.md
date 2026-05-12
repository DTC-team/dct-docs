# Sự kiện theo dõi

Với hình thức nhúng `iframe`, Shop phát `window.parent.postMessage(...)` tại các thời điểm quan trọng trong vòng đời. Sử dụng các sự kiện này để kết nối vào hệ thống analytics của bạn.

## Danh mục sự kiện

| Sự kiện | Khi nào | Payload |
|---------|---------|---------|
| `shop.ready` | Lần render đầu tiên sau bắt tay (handshake) | `{ type, partnerCode, userId }` |
| `shop.error` | Lỗi không thể khôi phục (auth, network) | `{ type, code, message }` |
| `shop.purchase_intent` | Người dùng bấm "Mua" trên một gói | `{ type, sku, price, currency }` |
| `shop.close_request` | Người dùng bấm nút đóng | `{ type }` |
| `shop.payment_success` | Đơn đã thanh toán | `{ type, orderId, sku, amount, currency }` — chờ hoàn thiện ở [payment return](../integration/payment-return.md) |

## Ví dụ listener

```ts
window.addEventListener("message", (event) => {
  // LUÔN xác thực origin so với Shop host đã cấu hình
  if (event.origin !== "https://<shop-host>") return;

  const msg = event.data;
  if (msg?.type === "shop.close_request") {
    document.getElementById("bluecom-iframe")?.remove();
  }
  // xử lý các sự kiện khác
});
```

!!! danger "Xác thực `event.origin`"
    Luôn kiểm tra `event.origin` so với hostname Shop đã cấu hình trước khi tin payload. Nếu không, bất kỳ trang nào cũng có thể giả mạo sự kiện.

## WebView native

Các sự kiện tương tự sẽ được expose qua JavaScript bridge của WebView (`window.webkit.messageHandlers` trên iOS, `Android.postMessage` trên Android). Đặc tả bridge sẽ được công bố cùng spec [payment return](../integration/payment-return.md).
