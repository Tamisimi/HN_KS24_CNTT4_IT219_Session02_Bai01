# Bài 1 — Khởi tạo Droplet trên DigitalOcean

## Mục tiêu

Tạo máy chủ Ubuntu trên DigitalOcean, xác thực bằng SSH Key, kết nối thành công bằng tài khoản `root`.

## Các bước thực hiện

### 1. Tạo cặp khóa SSH trên máy cá nhân

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

- Nhấn Enter để dùng đường dẫn mặc định (`~/.ssh/id_ed25519`)
- Có thể để trống passphrase hoặc đặt mật khẩu khóa

Public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy toàn bộ nội dung file `.pub`.

### 2. Đăng ký / đăng nhập DigitalOcean

1. Truy cập https://www.digitalocean.com
2. Đăng ký hoặc đăng nhập tài khoản
3. Vào **Settings → Security → SSH Keys → Add SSH Key**
4. Dán public key, đặt tên (ví dụ: `laptop-personal`), lưu

### 3. Tạo Droplet

1. **Create → Droplets**
2. **Region:** Singapore (gần Việt Nam nhất)
3. **Image:** Ubuntu 22.04 LTS (hoặc bản mới hơn nếu có)
4. **Plan:** Basic → Regular SSD → Shared CPU → gói rẻ nhất ($4 hoặc $6/tháng)
5. **Authentication:** chọn **SSH Key** (không dùng password) → chọn key vừa thêm
6. Hostname (tuỳ chọn), sau đó **Create Droplet**
7. Đợi Droplet Active, ghi lại **Public IPv4**

### 4. Kết nối SSH từ máy cá nhân

```bash
ssh -i ~/.ssh/id_ed25519 root@<IP_ADDRESS_DROPLET>
```

Lần đầu có thể hỏi xác nhận fingerprint → gõ `yes`.

**Kết quả mong đợi:** vào được shell Ubuntu với user `root`, không cần nhập mật khẩu.

Ví dụ log thành công:

```text
Welcome to Ubuntu 22.04.x LTS (GNU/Linux ...)
...
root@ubuntu-s-1vcpu-1gb-sgp1-01:~#
```

### 5. Kiểm tra nhanh trên server

```bash
hostname
uname -a
ip a
```

## Ảnh minh họa / minh chứng nộp bài

Chèn vào đây (sau khi làm thật):

1. Ảnh DigitalOcean Console — Droplet đang **Active** (thấy IP, region Singapore, Ubuntu)
2. Ảnh hoặc copy log Terminal — lệnh `ssh ... root@IP` thành công

```text
# Dán log kết nối thành công bên dưới

```

## Ghi chú

| Hạng mục | Giá trị đã chọn |
|----------|-----------------|
| OS | Ubuntu 22.04 LTS |
| Region | Singapore |
| Plan | Basic / Shared CPU / Regular SSD (gói rẻ nhất) |
| Auth | SSH Key (ed25519) |
| User | root |
| IP Droplet | `<điền IP sau khi tạo>` |
