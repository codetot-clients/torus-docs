# Development

Hệ thống CMS được chia làm hai thành phần dựa trên nền tảng open source WordPress.

- Plugin Torus Data
- Theme CT Torus (chỉ sử dụng cho phase 1)

## Plugin Torus Data

### API

Quản trị toàn bộ các đầu ra endpoint API

```
wp-content/plugins/torus-data/inc/classes/api/*.php
```

Quy tắc thiết kế:

- Mỗi class đều `implements Torus_Data_Api_Interface`.
- Sử dụng duy nhất 1 namespace và version `"$this->namespace/$this->version"`
- Verify đầu vào dữ liệu endpoint nếu là parameters, bao gồm `required`, `validate_callback` và `sanitize_callback`

Xem santize tham khảo ở đây: https://developer.wordpress.org/plugins/security/securing-output/

```php
register_rest_route("$this->namespace/$this->version", '/get_disease', [
  'method' => ['GET'],
  'permission_callback' => '__return_true',
  'callback' => [$this, 'get_disease_callback'],
  // Xác định đầu vào là ?post_slug=xxx
  'args' => [
      'post_slug' => [
          'required' => true,
          'sanitize_callback' => 'sanitize_text_field'
      ]
  ]
]);
```

- Đặt tên trùng khớp cho endpoint và callback

Ví dụ `/get_disease` thì callback là `get_disease_callback`

```php
<?php
register_rest_route("$this->namespace/$this->version", '/get_disease', [
    'method' => ['GET'],
    'permission_callback' => '__return_true',
    'callback' => [$this, 'get_disease_callback'],
    'args' => [
        'post_slug' => [
            'required' => true,
            'sanitize_callback' => 'sanitize_text_field'
        ]
    ]
]);
```

- Callback luôn luôn gọi vào 1 helper function để dữ liệu xử lý và output.

```php
<?php

function get_disease_category_callback($request) {
  ...
  $term_data = torus_data_get_disease_category($term_id);
  
  if (empty($term_data) || is_wp_error($term_data)) {
    return new WP_REST_Response([
      'errorCode' => 404,
      'errorMessage' => _x('Data is not available.', 'rest api response', 'torus-data')
    ], 404);
  }
  
  return new WP_REST_Response([
    'data' => $term_data
  ], 200);
}
```

### Helper functions

Các helper functions có triết lý thiết kế theo các định dạng:

**Query tinh giản**

- Sử dụng best practice với `WP_Query` để giản lược số lượng query database thấp nhất.

```php
$post_args = [
  'no_found_rows' => true,
  'update_post_term_cache' => false,
  'update_post_meta_cache' => false,
  'fields' => 'ids'
];
```

- Luôn cho phép khả năng mở rộng thông qua kết hợp parameter mở rộng khi cần.

```php
if (!empty($extra_args)) {
    $post_args = array_merge($default_args, $extra_args);
} else {
    $post_args = $default_args;
}
```

- Định nghĩa dữ liệu cứng theo dạng key => label cho mục đích dịch thuật

```php
function torus_data_get_disease_meta_keys()
{
    return [
        'no_prescription_treatment' => __('No Prescription Treatment', 'torus-data'),
        'main_cause'                => __('Main Cause', 'torus-data'),
        'differential_diagnosis'    => __('Differential Diagnosis', 'torus-data'),
        'synonymes'                 => __('Synonymes', 'torus-data'),
        'cell_type'                 => __('Cell Type', 'torus-data'),
        'treatment'                 => __('Treatment', 'torus-data'),
        'good_to_know'              => __('Good To Know', 'torus-data')
    ];
}
```

- Dữ liệu đầu ra được tổ chức theo các định dạng PHP Array.

```php
$disease_data = torus_get_disease_data($post_id);

// Kết quả trả ra:

// Dữ liệu cơ bản bắt đầu với prefix post_
post_id
post_title
post_content
post_permalink

// Dữ liệu meta nằm trong array riêng
meta = []

// Dữ liệu term nằm trong array riêng
categories = []
```
