# Dữ liệu chung (Global Data)

![Giao diện sửa dữ liệu chung](global-data-edit.jpg)

Dữ liệu chung là các dữ liệu được quy ước sử dụng ở mọi nơi, cung cấp các thông tin cơ bản về Belle, bao gồm:

- Các logo SVG (Header, Footer)
- Bản quyền cuối trang 
- Địa chỉ và chi nhánh
- Thông tin liên hệ
- Liên kết mạng xã hội

Các dữ liệu này được trích xuất qua endpoint [/get_global_data](rest-api.md#d%E1%BB%AF-li%E1%BB%87u-chung-global-data)

## Thêm Global Data

Cần thực hiện 2 bước: Edit Field Group (với quyền admin), và update code bổ sung key tương ứng.

### Bước 1: Edit Field Group "Global Data"

_Trước khi edit bất kỳ field group này, bạn cần xem mục Custom Fields > tìm tab "Sync available" xem có code cập nhật không._

Vào bằng menu **Custom Fields** > chọn mục **Global Data**. Thêm field mới và lưu lại. Nên đặt tên theo dạng `a_b_c` cho keyword để đúng format hiện tại của code dự án.

Các định dạng field được hỗ trợ sẵn sàng để output.
- Text
- Url
- Image
- Textarea

### Bước 2: Thêm field key vào trong danh sách REST API trả ra

Vào sửa code trong plugin `wp-content/plugins/torus-data/inc/`, tìm function `torus_data_get_global_data`.

- Nếu key thêm là text thông thường, thêm vào `$acf_keys`:

```php
$acf_keys = [
  'address_1',
  'address_2',
  'address_3',
  'footer_copyright',
  'email',
  'phone',
  'facebook',
  'twitter',
  'linkedin',
  'youtube'
];
```

Nếu key là media (ảnh tải lên), thêm vào `$media_acf_keys`:

```php
$media_acf_keys = [
  'header_logo',
  'header_alternative_logo',
  'footer_logo'
];
```

Kiểm tra bằng cách nhập liệu và mở API ra.

## Xoá/Đổi key Global Data

Tương tự như khi thêmn ở bước trên, với quyền admin, bạn làm lần lượt:
- Sửa field group "Global Data" trong menu Custom Fields
- Xoá field key tương ứng trong function `torus_data_get_global_data()`
