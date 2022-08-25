# Dữ liệu chung (Global Data)

**Mục lục**

- [Cấp độ và yêu cầu](#cấp-độ-và-yêu-cầu)
- [Menu truy cập](#menu-truy-cập)
- [Giới thiệu](#giới-thiệu)
- [Thêm trường dữ liệu](#thêm-global-data)
- [Xoá/Đổi trường dữ liệu](#xoáđổi-key-global-data)
- [Dịch](#dịch)

## Cấp độ và yêu cầu

- Người quản lý có quyền cao nhất (Quản trị viên - Administrator - role `manage_options`)
- Plugin **Advanced Custom Fields (PRO)** đã được kích hoạt

## Menu truy cập

Sau khi đăng nhập, tìm menu chính **"Global Data"**, chọn các tab tương ứng để sửa nội dung.

![Menu sửa dữ liệu chung](global-data-menu.png)

Gồm các tab chính:

- **Info:** dữ liệu cơ bản nhất gồm Logo (logo đầu trang - màu nền tối và sáng, logo cuối trang), địa chỉ, thông tin bản quyền web
- **Contact:** dữ liệu email và số điện thoại
- **Social:** địa chỉ các mạng xã hội
- **REST API Data** (dành cho lập trình viên): thêm các key để hiển thị dữ liệu trong API endpoint. Xem mục "Thêm Global Data" để biết chi tiết

## Giới thiệu

![Giao diện sửa dữ liệu chung](global-data-edit.jpg)

Dữ liệu chung là các dữ liệu được quy ước sử dụng ở mọi nơi, cung cấp các thông tin cơ bản về Belle, bao gồm:

Các dữ liệu này được trích xuất qua endpoint [/get_global_data](rest-api.md#d%E1%BB%AF-li%E1%BB%87u-chung-global-data)

## Thêm Global Data

Cần thực hiện 2 bước: Edit Field Group (với quyền admin), và update tên field bổ sung dạng key tương ứng.

**Các bước sau chỉ nên dành cho developer hoặc người có kinh nghiệm làm việc với CMS.**

### Bước 1: Đồng bộ field group mới nhất

Trước khi edit bất kỳ field group này, bạn cần xem mục menu chính **Custom Fields** > tìm tab **"Sync available"** xem có code cập nhật không.

![Xem có tab Sync trong ACF không](global-data-acf-sync.png)

### Bước 2: Sửa Field Group "Global Data"

Vào bằng menu **Custom Fields** > chọn mục **Global Data**. Thêm field mới và lưu lại. Nên đặt tên theo dạng `a_b_c` cho keyword để đúng format hiện tại của code dự án.

Các định dạng field được hỗ trợ sẵn sàng để output.
- Text
- Url
- Image
- Textarea

### Bước 3: Thêm field key vào trong danh sách REST API trả ra

Trong menu chính Global Data, tìm tab **REST API Data**.

![Giao diện set key ACF global data](global-data-set-keys.png)

- Nếu key thêm là text thông thường, thêm vào `Text ACF Keys`.
- Nếu key là media (ảnh tải lên), thêm vào `Media ACF Keys`.

Kiểm tra bằng cách nhập liệu và mở API ra.

## Xoá/Đổi key Global Data

1. Truy cập menu **Field Groups**, chọn mục **Global Data** từ danh sách. Chọn key để xoá/sửa và ấn nút Save để có hiệu lực.

Để xoá 1 key:

![Xoá key trong Global Data](global-data-delete-key.png)

Để sửa 1 key:

![Sửa key và name hiển thị trong Global Data](global-data-edit-key.png)

2. Xoá tên key tương ứng trong menu chính **Global Data** > tab **REST API Data**.

![Giao diện set key ACF global data](global-data-set-keys.png)

## Dịch

Để dịch sang ngôn ngữ, truy cập menu Global Data, chọn lại ngôn ngữ từ thanh bar trên cùng màu đen.

![Giao diện chọn ngôn ngữ cho dịch Global Data](global-data-translate.png)
