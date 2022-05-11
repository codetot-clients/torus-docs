layout: page
title: "REST API"
permalink: /rest-api/

# REST API

Hệ thống được thiết kế theo tiêu chuẩn REST API, dựa trên viết các custom router phục vụ cho lấy dữ liệu khác nhau.

Các endpoint của hệ thống theo quy chuẩn:

```
wp-json/torus-data/v1/<endpoint_name>
```

Các đầu dữ liệu có sẵn bao gồm:

**Diseases**

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

**Disease Categories**

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
