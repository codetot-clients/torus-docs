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

Khi truyền vào lấy dữ liệu đơn lẻ, sử dụng trường dữ liệu `slug`.

## Endpoints

### Dữ liệu chung (Global Data)

Các dữ liệu cơ bản như địa chỉ, link mạng xã hội, menu.

Danh sách các menu

```
/menus
```

Lấy danh sách các item trong một menu

```
/menu/<slug>
```

Lấy dữ liệu website chung

```
/globalData

Param ngôn ngữ:
- lang: (thay cho wpml_language), ví dụ en, vi, fr...
```

Lấy dữ liệu tất cả ngôn ngữ có trên CMS

```
/language
```

### Diseases

Lấy danh sách theo thứ tự mới nhất

```
/diseases

Params:
- posts_per_page: number
- paged: number
- categories: string (nếu nhiều hơn 1 thì nhập cách bởi dấu phẩy, vd: a,b,c) - là category slug
- slugs:  (nếu nhiều hơn 1 thì nhập cách bởi dấu phẩy, vd: a,b,c) - là disease slug
```

> Khi chọn lọc `slugs` thì điều kiện `post_per_page`, `paged` không cần thiết.

Lấy dữ liệu một loại disease theo post slug

```
/disease/<slug>
```

### Disease Categories

Lấy danh sách tất cả category

```
/categories?module=diseases
```

Lấy dữ liệu một category theo term slug

```
/diseaseCategory/<slug>
```

### Post/News Category

Lấy danh sách danh mục tin tức

```
/categories?module=news

Params: 
- slugs: string (nhiều: cách nhau bởi dấu phẩy, vd `beauty-2,beauty-3`)
```

Lấy danh sách bài viết

```
/posts

Params:
- posts_per_page: number
- paged: number
- categories: string (nhiều: cách nhau bởi dấu phẩy, vd `beauty-2,beauty-3`)
```

Lấy nội dung một bài viết lẻ:

```
/post/<slug>
```

Lấy bài viết được đánh dấu Sticky (nổi bật):

```
/highlightPosts

Params:
- posts_per_page: number (optional)
- paged: number (optional)
- categories: number (optional)
```

Lấy bài viết theo cấu trúc danh mục (category > posts)

```
/postsByAllCategories

Params:
- posts_per_page: number
```

### Page

Lấy nội dung bài viết

```
/page/<slug>
```
