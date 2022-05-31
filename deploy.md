# Deploy dự án

Dự án được lưu trữ trên GitHub (private repository). Hình thức cài đặt có thể tải source code về (dạng file nén .zip) hoặc sử dụng terminal trên server hỗ trợ SSH.

## Cài đặt source code

**Tải source code và tự upload**

Hình thức tải về và tự upload lên yêu cầu hỗ trợ FTP/sFTP. Tải code lên đúng folder.

**Upload qua Git**

*Yêu cầu*:

- Server hỗ trợ Git, ví dụ trên Ubuntu chạy lệnh cài đặt `sudo apt install git`.
- Server nên hỗ trợ [wp-cli](https://wp-cli.org/#installing)
- Generate SSH Key (.pub) để access vào private repository. Liên hệ khoi@codetot.com để add key vào repository.

```
ssh-keygen -t ed25519 -C "cms@belle.ai"
```

Tại folder dự kiến, ví dụ `/home/belle-cms/`

Branch checkout: `production`

```
git init
git remote add origin git@github.com:codetot-clients/torus-cms.git
git fetch origin
git reset --hard origin/production
git checkout -b production
```

## Cài đặt database

- Lấy database bản mới nhất từ demo site
- Import database vào MySQL sử dụng công cụ hoặc phpMyadmin nếu có.
- [Thay đổi đường dẫn lại cho CMS](https://wordpress.org/support/article/changing-the-site-url/), tốt nhất là [sửa trong database](https://wordpress.org/support/article/changing-the-site-url/#changing-the-url-directly-in-the-database).
- Truy cập đường dẫn và thiết lập database mới
- Truy cập vào đường dẫn /wp-admin/, tìm mục **Settings / Permalinks** và ấn nút Lưu lại một lần.

## Deploy thông qua Docker

Trong GitHub, hệ thống tạo phiên bản docker bằng cách phát hành lại từ nhánh `origin/production` sang `docker`. Lấy source bản Docker để deploy.
