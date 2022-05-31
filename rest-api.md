# REST API

Hệ thống được thiết kế theo tiêu chuẩn REST API, dựa trên viết các custom router phục vụ cho lấy dữ liệu khác nhau.

Các endpoint của hệ thống theo quy chuẩn:

```
wp-json/torus-data/v1/<endpoint_name>
```

Param để lấy nội dung theo ngôn ngữ khác, có sẵn trong mọi endpoint. 

```
- wpml_language: string (vd en, vi)
```

Prefer khi truyền vào lấy dữ liệu đơn lẻ, sử dụng trường dữ liệu `slug`.

```
post_slug
term_slug
```

## Endpoints

### Dữ liệu chung (Global Data)

Các dữ liệu cơ bản như địa chỉ, link mạng xã hội, menu.

Danh sách các menu

```
get_menus
```

Lấy danh sách các item trong một menu

```
get_menu

Params:
- menu: string
```

Lấy dữ liệu website chung

```
get_global_data
```

Lấy dữ liệu tất cả ngôn ngữ có trên CMS

```
get_wpml_languages
```

### Diseases

Lấy danh sách theo thứ tự mới nhất

```
get_diseases

Params:
- posts_per_page: number
- paged: number
```

Lấy dữ liệu một loại disease theo post slug

```
get_disease

Params:
- post_slug: string
```

### Disease Categories

Lấy danh sách tất cả category

```
get_disease_categories

Params:
- is_top_level: bool
- parent_term_slug: string
```

Lấy dữ liệu một category theo term slug

```
get_disease_category

Params:
- term_slug: string
```

### Post/News Category

Lấy danh sách page News landing (Blog/News)

```
get_page_for_posts
```

Lấy danh sách danh mục tin tức

```
get_categories
```

Lấy danh sách bài viết

```
get_posts

Params:
- posts_per_page: number
- paged: number
```

Lấy nội dung một bài viết lẻ:


```
get_post

Params:
- post_slug
```

### Page

Lấy nội dung bài viết

```
get_page

Params:
- post_slug
```
