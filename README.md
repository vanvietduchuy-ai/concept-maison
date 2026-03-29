# 🏨 Concept Maison – Hướng dẫn thiết lập & Deploy

## 📁 Cấu trúc dự án
```
concept-maison-web/
├── index.html      ← Trang đặt phòng cho KHÁCH HÀNG
├── admin.html      ← Trang QUẢN LÝ dành cho nhân viên
└── README.md       ← File hướng dẫn này
```

## 🔄 Cách đồng bộ dữ liệu
Cả 2 trang dùng chung **localStorage** của trình duyệt.
- Khách đặt phòng trên `index.html` → dữ liệu lưu vào localStorage
- Admin mở `admin.html` trên CÙNG trình duyệt → thấy đặt phòng mới ngay
- **Quan trọng**: Cả 2 file phải cùng 1 domain (deploy lên Netlify cùng 1 site)

---

## 💻 HƯỚNG DẪN THIẾT LẬP TRÊN WINDOWS

### BƯỚC 1 – Cài đặt VS Code (Editor)
1. Vào: https://code.visualstudio.com/
2. Tải **Windows Installer (.exe)**
3. Cài đặt bình thường (Next → Next → Finish)

### BƯỚC 2 – Cài đặt Node.js (Cần cho Netlify CLI)
1. Vào: https://nodejs.org/
2. Tải phiên bản **LTS (Long Term Support)**
3. Cài đặt, chọn "Add to PATH" khi được hỏi
4. Mở **Command Prompt** (Windows + R → gõ `cmd`) và kiểm tra:
   ```
   node --version    ← phải hiện v20.x.x
   npm --version     ← phải hiện 10.x.x
   ```

### BƯỚC 3 – Xem trước trang web trên máy (Local)
Cách đơn giản nhất – dùng VS Code:
1. Mở VS Code
2. Cài extension **"Live Server"** (tìm trong Extensions tab Ctrl+Shift+X)
3. Mở thư mục `concept-maison-web` trong VS Code
4. Click chuột phải vào `index.html` → **"Open with Live Server"**
5. Trình duyệt tự mở: `http://127.0.0.1:5500/index.html`
6. Mở tab mới: `http://127.0.0.1:5500/admin.html`

### BƯỚC 4 – Cài Netlify CLI để deploy
Mở **Command Prompt** hoặc **PowerShell**, gõ:
```bash
npm install -g netlify-cli
```
Kiểm tra:
```bash
netlify --version
```

---

## 🚀 DEPLOY LÊN NETLIFY (3 cách)

### Cách 1 – Kéo thả (Đơn giản nhất) ⭐
1. Vào: https://app.netlify.com/ → Đăng ký tài khoản miễn phí
2. Sau khi đăng nhập, kéo thư mục `concept-maison-web` vào ô **"Drag and drop"**
3. Chờ 30 giây → Netlify tự cấp URL (vd: `https://random-name.netlify.app`)
4. Truy cập:
   - Trang khách: `https://your-site.netlify.app/index.html`
   - Trang admin: `https://your-site.netlify.app/admin.html`

### Cách 2 – Dùng Netlify CLI ⭐⭐
```bash
# 1. Đăng nhập vào Netlify
netlify login

# 2. Vào thư mục dự án
cd C:\Users\YourName\concept-maison-web

# 3. Deploy
netlify deploy --dir . --prod

# Netlify sẽ hỏi: "What would you like to link this site to?" → chọn "Create & configure a new site"
```

### Cách 3 – Dùng GitHub + Netlify (Chuyên nghiệp nhất) ⭐⭐⭐
1. Cài **Git**: https://git-scm.com/download/win
2. Tạo tài khoản **GitHub**: https://github.com/
3. Tạo repository mới trên GitHub
4. Upload code lên GitHub:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin https://github.com/username/concept-maison.git
   git push -u origin main
   ```
5. Vào Netlify → **"Import from Git"** → Chọn repo GitHub
6. Mỗi lần push code mới → Netlify tự động deploy!

---

## ⚙️ CÀI ĐẶT TÊN MIỀN RIÊNG (Tuỳ chọn)
1. Mua domain tại: Tenten.vn, Matbao.net hoặc Namecheap.com
2. Trong Netlify: Site settings → Domain management → Add custom domain
3. Trỏ DNS theo hướng dẫn của Netlify

---

## ❗ LƯU Ý QUAN TRỌNG VỀ DỮ LIỆU

### localStorage hoạt động như thế nào?
- Dữ liệu lưu trong **trình duyệt** của từng máy tính
- Nếu dùng Chrome trên máy A → admin trên Chrome máy A mới thấy
- Nếu muốn nhiều máy xem cùng dữ liệu → cần nâng cấp lên database

### Giới hạn hiện tại
| Tính năng | Hiện tại (localStorage) | Nâng cấp cần |
|-----------|------------------------|--------------|
| Xem từ 1 máy | ✅ | — |
| Xem từ nhiều máy | ❌ | Backend API |
| Backup tự động | ❌ | Database |
| Thanh toán online | ❌ | Payment Gateway |

### Backup dữ liệu
- Vào trang Admin → Cài đặt → **"Xuất dữ liệu (JSON)"**
- Lưu file JSON ra ổ cứng định kỳ
- Để khôi phục: Cài đặt → **"Nhập dữ liệu (JSON)"**

---

## 📱 TRUY CẬP TỪ ĐIỆN THOẠI
Sau khi deploy Netlify:
- Khách hàng: Mở điện thoại → vào URL của site
- Admin: Mở `your-site.netlify.app/admin.html` trên điện thoại
- Lưu ý: Dữ liệu sẽ khác nhau giữa điện thoại và máy tính (khác trình duyệt)

---

## 🔧 CHỈNH SỬA NỘI DUNG

### Đổi tên khách sạn
Mở `index.html` → Ctrl+H → Tìm "Concept Maison" → Thay bằng tên của bạn

### Đổi địa chỉ, số điện thoại
Mở `index.html` → Tìm đến phần `footer` (cuối file) → Chỉnh sửa

### Đổi giá phòng mặc định
Mở `admin.html` → Đăng nhập → Trang "Sơ đồ phòng" → Quản lý từng phòng

---

## 📞 HỖ TRỢ
- Netlify Docs: https://docs.netlify.com/
- VS Code Tutorial: https://code.visualstudio.com/docs
