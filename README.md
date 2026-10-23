# TXMD5 Lite Sessions Viewer

Xem dữ liệu phiên TXMD5 + thống kê chuỗi/cầu.

## ⚠️ Cảnh báo
- Repo PUBLIC → **token `at=...` trong `index.html` bị lộ**, ai cũng dùng được.
- Nếu API chặn CORS → trang tự hiển thị **DỮ LIỆU DEMO** (bấm nút 🧪 Demo để xem thủ công).

## Deploy GitHub Pages
1. Push `index.html` lên repo.
2. Settings → Pages → Branch `main` / root → Save.
3. Mở `https://<user>.github.io/<repo>/`.

## Deploy Render.com (static site)
1. Vào https://render.com → New → Static Site.
2. Connect repo GitHub.
3. Build Command: *(để trống)*
4. Publish Directory: `.`
5. Create → đợi 1 phút → có URL `.onrender.com`.

## Fix CORS bằng Cloudflare Worker (nếu API chặn)
```js
const TOKEN = 'YOUR_TOKEN';
export default {
  async fetch() {
    const r = await fetch(
      `https://wtxmd52.tele68.com/v1/txmd5/lite-sessions?cp=R&cl=R&pf=web&at=${TOKEN}`
    );
    return new Response(await r.text(), {
      headers: {
        'Access-Control-Allow-Origin': '*',
        'Content-Type': 'application/json'
      }
    });
  }
};
