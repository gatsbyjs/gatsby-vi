---
title: Tạo những Component Bố cục Lồng nhau
typora-copy-images-to: ./
disableTableOfContents: true
---

Chào mừng đến với phần 3!

## Bài hướng dẫn này có những gì?

Ở phần này, bạn sẽ tìm hiểu về các plugin trong Gatsby và tạo các component "bố cục".

Các Gatsby plugin là những gói JavaScript nhằm bổ sung chức năng cho một trang web Gatsby. Gatsby được thiết kế để có thể mở rộng, tức là các plugin có thể mở rộng và chỉnh sửa hầu như mọi thứ mà Gatsby thực hiện.

Các component bố cục được dùng cho các bộ phận của website mà bạn muốn chia sẻ giữa nhiều trang với nhau. Ví dụ, các website thường sẽ có một component bố cục ở đầu trang (header) và cuối trang (footer) được dùng chung (trong nhiều trang khác nhau). Những thứ thông thường khác cũng được thêm vào bố cục là sidebar và/hoặc menu định hướng. Ví dụ như trang này, phần đầu trang (header) là một phần thuộc về component bố cục của gatsbyjs.org.

Hãy tìm hiểu sâu hơn về phần 3.

## Sử dụng các plugin

Có lẽ bạn đã quen thuộc với ý tưởng của các plugin. Nhiều hệ thống phần mềm hỗ trợ việc thêm vào các plugin tùy chỉnh để bổ sung các chức năng mới hoặc thậm chí thay đổi các hoạt động cốt lõi của phần mềm. Các Gatsby plugin hoạt động tương tự như vậy.

Những thành viên cộng đồng (tương tự như bạn!) có thể đóng góp các plugin (các đoạn code JavaScript nhỏ) để những người khác có thể sử dụng khi xây dựng các trang web Gatsby.

> Đã có hàng trăm plugins rồi! Tìm hiểu thêm về [thư viện Plugin](/plugins/) của Gatsby.

Mục đích của chúng tôi là làm cho các plugin dễ dàng cài đặt và sử dụng. Bạn rất có khả năng là sẽ sử dụng plugin trong hầu hết mọi trang web Gatsby mà bạn xây dựng. Ở phần còn lại của bài hướng dẫn, bạn sẽ có cơ hội thực hành việc cài đặt và sử dụng chúng.

Trong phần giới thiệu khởi đầu về sử dụng các plugin, chúng ta sẽ cài đặt và triển khai Gatsby plugin cho Typography.js.

[Typography.js](https://kyleamathews.github.io/typography.js/) là một thư viện JavaScript mà sẽ tạo ra các định dạng toàn cục về thiết kế chữ cho trang web của bạn. Thư viện này có một [plugin Gatsby tương ứng](/packages/gatsby-plugin-typography/) để đơn giản hóa việc sử dụng cho một trang web Gatsby.

### ✋ Tạo một trang web Gatsby

Như chúng ta đã đề cập ở [phần 2](/tutorial/part-two/), ngay lúc này bạn nên đóng tất cả các cửa sổ terminal và các tập tin dự án ở những phần trước của bài hướng dẫn để giữ mọi thứ gọn gàng trên Desktop. Sau đó mở một của sổ terminal mới và chạy các lệnh sau để tạo một trang web Gatsby mới trong thư mục `tutorial-part-three` và di chuyển vào thư mục mới này:

```shell
gatsby new tutorial-part-three https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-three
```

### ✋ Cài đặt và cấu hình `gatsby-plugin-typography`

Có 2 bước chính để sử dụng một plugin: Cài đặt và cấu hình.

1. Cài đặt gói NPM cho `gatsby-plugin-typography`.

```shell
npm install --save gatsby-plugin-typography react-typography typography typography-theme-fairy-gates
```

> Chú ý: Typography.js yêu cầu một số gói bổ sung đã được bao gồm trong phần hướng dẫn. Các yêu cầu bổ sung tương tự như vậy sẽ được nêu rõ trong phần hướng dẫn "cài đặt" của mỗi plugin.

2. Chỉnh sửa tập tin `gatsby-config.js` tại thư mục gốc của dự án như sau:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

`gatsby-config.js` là một tập tin đặc biệt khác mà Gatsby sẽ tự động nhận diện. Đây là nơi bạn sẽ thêm các plugin và những cấu hình khác của trang web.

> Xem qua [tài liệu về gatsby-config.js](/docs/gatsby-config/) để tìm hiểu thêm, nếu bạn muốn.

3. Typography.js cần một tập tin cấu hình. Tạo một thư mục mới đặt tên `utils` trong thư mục `src`. Sau đó thêm vào `utils` một tập tin mới đặt tên là `typography.js` và sao chép đoạn sau vào trong tập tin này:

```javascript:title=src/utils/typography.js
import Typography from "typography"
import fairyGateTheme from "typography-theme-fairy-gates"

const typography = new Typography(fairyGateTheme)

export const { scale, rhythm, options } = typography
export default typography
```

4. Khởi động máy chủ phát triển.

```shell
gatsby develop
```

Một khi bạn tải trang web, nếu bạn kiểm tra qua HTML được tạo ra, bằng cách sử dụng Chrome Developer Tools, bạn sẽ thấy rằng plugin định dạng đã thêm một phần tử `<style>` vào phần tử `<head>` cùng với CSS của nó.

![typography-styles](typography-styles.png)

### ✋ Thực hiện một số thay đổi nội dung và định dạng

Sao chép đoạn sau vào `src/pages/index.js` để bạn có thể quan sát
hiệu ứng CSS được tạo ra bởi Typography.js dễ dàng hơn.

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <div>
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
      What do I like to do? Lots of course but definitely enjoy building
      websites.
    </p>
  </div>
)
```

Bây giờ trang web của bạn sẽ trông như thế này:

![no-layout](no-layout.png)

Hãy cùng thực hiện một sự cải thiện nhanh nào! Nhiều trang web có một cột đơn văn bản được canh lề ở giữa trang. Để làm được điều này, thêm đoạn sau vào
`<div>` trong `src/pages/index.js`.

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  // highlight-next-line
  <div style={{ margin: `3rem auto`, maxWidth: 600 }}>
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
      What do I like to do? Lots of course but definitely enjoy building
      websites.
    </p>
  </div>
)
```

![with-layout2](with-layout2.png)

Tốt lắm. Bạn đã cài đặt và cấu hình xong Gatsby plugin đầu tiên!

## Tạo các component bố cục

Bây giờ chúng ta học tiếp về các các component bố cục. Để chuẩn bị cho phần này, hãy thêm một vài trang mới vào trong dự án của bạn bao gồm: một trang about và một trang contact.

```jsx:title=src/pages/about.js
import React from "react"

export default () => (
  <div>
    <h1>About me</h1>
    <p>I’m good enough, I’m smart enough, and gosh darn it, people like me!</p>
  </div>
)
```

```jsx:title=src/pages/contact.js
import React from "react"

export default () => (
  <div>
    <h1>I'd love to talk! Email me at the address below</h1>
    <p>
      <a href="mailto:me@example.com">me@example.com</a>
    </p>
  </div>
)
```

Hãy cùng xem trang about mới trông như thế nào:

![about-uncentered](about-uncentered.png)

Hmm. Sẽ tốt hơn nếu nội dung của hai trang mới được canh lề ở giữa tương tự như trang index. Và sẽ hay hơn nếu nó có một cách để điều hướng trong toàn bộ trang web, để nó trở nên dễ dàng cho những người ghé thăm trang web có thể tìm kiếm và truy cập các trang phụ.

Bạn sẽ thực hiện các sự thay đổi này bằng cách tạo ra component bố cục đầu tiên.

### ✋ Tạo component bố cục đầu tiên

1. Tạo một thư mục mới tại `src/components`.

2. Tạo một component bố cục cơ bản tại `src/components/layout.js`:

```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    {children}
  </div>
)
```

3. Nhúng component bố cục mới này vào trong component trang `src/pages/index.js` của bạn:

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout" // highlight-line

export default () => (
  <Layout> {/* highlight-line */}
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
      What do I like to do? Lots of course but definitely enjoy building
      websites.
    </p>
  </Layout> {/* highlight-line */}
)
```

![with-layout2](with-layout2.png)

Tốt lắm, bố cục đã hoạt động! Nội dung trang index của bạn vẫn được canh lề ở giữa.

Nhưng hãy thực hiện điều hướng vào `/about/`, hoặc `/contact/`. Nội dung của những trang này vẫn chưa được canh lề ở giữa.

4. Nhúng component bố cục vào trong `about.js` và `contact.js` (tương tự như bạn đã làm cho `index.js` ở bước trước đó).

Nội dung cả ba trang của bạn đã được canh lề ở giữa nhờ component bố cục dùng chung duy nhất này!

### ✋ Thêm tiêu đề cho một trang web

1. Thêm đoạn sau vào component bố cục mới của bạn:

```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    <h3>MySweetSite</h3> {/* highlight-line */}
    {children}
  </div>
)
```

Nếu như bạn truy cập vào bất kì trang nào trong số ba trang, bạn sẽ thấy cùng một tiêu đề đã được thêm vào, ví dụ trang `/about/`:

![with-title](with-title.png)

### ✋ Thêm liên kết điều hướng giữa các trang

1. Thêm đoạn sau vào trong component bố cục:

```jsx:title=src/components/layout.js
import React from "react"
// highlight-start
import { Link } from "gatsby"

const ListLink = props => (
  <li style={{ display: `inline-block`, marginRight: `1rem` }}>
    <Link to={props.to}>{props.children}</Link>
  </li>
)
// highlight-end

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    {/* highlight-start */}
    <header style={{ marginBottom: `1.5rem` }}>
      <Link to="/" style={{ textShadow: `none`, backgroundImage: `none` }}>
        <h3 style={{ display: `inline` }}>MySweetSite</h3>
      </Link>
      <ul style={{ listStyle: `none`, float: `right` }}>
        <ListLink to="/">Home</ListLink>
        <ListLink to="/about/">About</ListLink>
        <ListLink to="/contact/">Contact</ListLink>
      </ul>
    </header>
    {/* highlight-end */}
    {children}
  </div>
)
```

![with-navigation2](with-navigation.png)

Và bạn đã hoàn thành xong! Một trang web gồm 3 trang với điều hướng toàn cục cơ bản.

_Thử thách:_ Với sức mạnh của "component bố cục" mới, hãy thử thêm vào đầu trang, cuối trang, điều hướng toàn cục, các sidebar,... vào trang web Gatsby của bạn!

## Tiếp theo là gì?

Tiếp tục [phần 4 của bài hướng dẫn](/tutorial/part-four/) để học thêm về lớp dữ liệu của Gatsby và tạo trang bằng cách lập trình.
