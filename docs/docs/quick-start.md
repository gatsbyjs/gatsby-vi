---
title: Bắt đầu nhanh
---

Hướng dẫn này phù hợp cho những lập trình viên từ trung cấp đến nâng cao. Với những hướng dẫn căn bản hơn về Gatsby, [vui lòng xem tại đây](/tutorial/)

## Sử dụng Gatsby CLI:

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-quick-start-with-gatsby-create-develop-and-build-gatsby-sites-from-the-command-line"
  lessonTitle="Bắt đầu nhanh với Gatsby. Tạo dựng trang web với Gatsby thông qua câu lệnh"
/>

**Lưu Ý**: Video này sử dụng `npx`, là 1 công cụ dùng để chạy npm package mà không cần phải qua cài đặt. Chạy lệnh `npx gatsby new` cũng giống như chạy lệnh `gatsby new` sau khi đã cài đặt `gatsby-cli` trên máy của bạn.

### Cài đặt Gatsby CLI:

```shell
npm install -g gatsby-cli
```

### Tạo trang Gatsby mới:

```shell
gatsby new gatsby-site
```

### Vào thư mục chứa site bạn vừa tạo:

```shell
cd gatsby-site
```

### Khởi động development server:

```shell
gatsby develop
```

Gatsby sẽ khởi động môi trường dev reload liên tục ở đường dẫn mặc định `localhost:8000`.

Hãy thử chỉnh sửa 1 trang Javascript trong `src/pages`. Những thay đổi của bạn sẽ được cập nhật ngay trên trình duyệt.

### Tạo bản build cho production

```shell
gatsby build
```

Gatsby sẽ tạo ra một bản build tối ưu cho trang của bạn, tạo ra các file HTML tĩnh và đóng gói các mảng Javascript code của bạn.

### Chạy bản build production trên máy local

```shell
gatsby serve
```

Gatsby sẽ tạo 1 server HTML local cho bạn test trang web. Hãy nhớ dùng câu lệnh `gatsby build` trước khi chạy lệnh `gatsby serve` nhé.

### Tìm hiểu thêm về dòng lệnh Gatsby CLI

Để hiểu rõ hơn về các câu lênh mà Gatsby CLI có, chạy lệnh `gatsby --help` trong terminal.

Nếu muốn tìm hiểu câu lệnh cụ thể, chạy lệnh `gatsby TÊN_LỆNH --help`, ví dụ `gatsby new --help`.

Để có thêm thông tin về Gatsby CLI, bạn có thể xem [Ghi chú về CLI](/docs/gatsby-cli/).

