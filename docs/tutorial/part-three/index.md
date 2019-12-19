---
title: Tạo Nested Layout Components
typora-copy-images-to: ./
disableTableOfContents: true
---

Chào mừng đến với phần 3!

## Có gì trong bài hướng dẫn này?

Ở phần này, bạn sẽ học về các thành phần mở rộng của Gatsby và tạo các thành phần "bố cục".

Các thành phần mở rộng của Gatsby là những gói JavaScript nhằm bổ sung chức năng cho một trang web trên nền tảng Gatsby. Gatsby được thiết kế với khả năng nâng cấp, tức là các thành phần này có thể mở rộng và thay đổi hầu như mọi thứ mà Gatsby thực hiện.

Các thành phần bố cục được dùng cho từng khu vực của website mà bạn muốn chia sẻ giữa nhiều trang với nhau. Ví dụ, các websites thường sẽ có cùng có một thành phần bố cục ở đầu trang và cuối trang. Một số thành phần khác cũng thường được thêm vào trong bố cục như các thanh bên và/hoặc menu điều hướng. Ở trang ví dụ này, phần đầu trang là một trong các thành phần bố cục của gatsbyjs.org.

Cùng tìm hiểu sâu hơn về phần 3.

## Sử dụng các thành phần mở rộng

Có lẽ bạn đã quen thuộc với ý tưởng của các thành phần mở rộng. Nhiều hệ thống phần mềm hỗ trợ việc thêm vào các thành phần mở rộng được tùy chỉnh để bổ sung các chức năng mới hoặc thay đổi các hoạt động chính của phần mềm. Các thành phần mở rộng của Gatsby hoạt động tương tự như vậy.

Những thành viên cộng đồng (tương tự như bạn!) có thể đóng góp các thành phần mở rộng (các đoạn code nhỏ được viết bằng JavaScript) để những người khác có thể sử dụng khi xây dựng các trang web trên nền tảng Gatsby.

> Đã có hàng trăm plugins rồi! Tìm hiểu thêm về Gatsby [Thư viện Plugin](/plugins/).

Mục đích của chúng tôi là làm cho các thành phần mở rộng dễ dàng cài đặt và sử dụng. Bạn sẽ có thể sử dụng các thành phần mở rộng này trong hầu hết các trang web trên nền tảng Gatsby mà bạn xây dựng. Ở phần còn lại của bài hướng dẫn, bạn sẽ có cơ hội thực hành việc cài đặt và sử dụng chúng.

Trong phần giới thiệu về sử dụng các thành phần mở rộng, chúng ta sẽ cài đặt và sử dụng chúng cho Typography.js.

[Typography.js](https://kyleamathews.github.io/typography.js/) là một thư viện JavaScript nhằm tạo ra các kiểu mẵu toàn cục về thiết kế chữ cho trang web của bạn. Thư viện này có một [Gatsby plugin](/packages/gatsby-plugin-typography/) để đơn giản hóa việc sử dụng cho một trang web trên nền tảng Gatsby.

### ✋ Tạo một trang web trên nền tảng Gatsby

Như chúng ta đã đề cập ở [phần 2](/tutorial/part-two/), ngay lúc này bạn nên đóng tất cả các cửa sổ terminal và các tập tin projects ở những phần trước của bài hướng dẫn. Sau đó mở một của sổ terminal mới và chạy các lệnh sau để tạo một trang web mới trên nền tảng Gatsby trong thư mục `tutorial-part-three` và truy cập vào thư mục mới này:

```shell
gatsby new tutorial-part-three https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-three
```

### ✋ Cài đặt và tùy chỉnh `gatsby-plugin-typography`

Có 2 bước chính để sử dụng một thành phần mở rộng: Cài đặt và tùy chỉnh.

1. Cài đặt `gatsby-plugin-typography` NPM package.

```shell
npm install --save gatsby-plugin-typography react-typography typography typography-theme-fairy-gates
```

> Chú ý: Typography.js yêu cầu thêm một số tệp khác đã được bao gồm trong phần hướng dẫn. Các yêu cầu thêm tương tự như vậy sẽ được nêu rõ trong phần hướng dẫn "cài đặt" của mỗi thành phần mở rộng.

2. Chỉnh sửa file `gatsby-config.js` tại thư mục gốc của project thành:

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

`gatsby-config.js` là một file đặc biệt khác mà Gatsby sẽ tự động nhận diện. Đây là nơi bạn sẽ thêm các thành phần mở rộng và những tùy chỉnh khác của trang web.

> Truy cập [doc on gatsby-config.js](/docs/gatsby-config/) để tìm hiểu thêm, nếu bạn muốn.

3. Typography.js cần một file tùy chỉnh. Tạo một thư mục mới đặt tên `utils` trong thư mục `src`. Sau đó thêm vào `utils` một file mới đặt tên `typography.js` và sao chép đoạn sau vào trong file:

```javascript:title=src/utils/typography.js
import Typography from "typography"
import fairyGateTheme from "typography-theme-fairy-gates"

const typography = new Typography(fairyGateTheme)

export const { scale, rhythm, options } = typography
export default typography
```

4. Khởi động development server.

```shell
gatsby develop
```

Sau khi bạn tải trang web, nếu bạn dùng công cụ Chrome developer để kiểm tra HTML được tạo ra, bạn sẽ thấy rằng thành phần mở rộng trong việc thiết kế chữ đã thêm một `<style>` element vào `<head>` element cùng với CSS của nó.

![typography-styles](typography-styles.png)

### ✋ Thay đổi nội dung và kiểu mẫu

Sao chép đoạn sau vào `src/pages/index.js` để bạn có thể quan sát 
sự thay đổi trên CSS được tạo ra bởi Typography.js dễ dàng hơn.

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

Cùng hoàn thiện nhanh nào. Nhiều trang web có một cột đơn văn bản được canh lề ở giữa trang. Để làm được điều này, thêm đoạn sau vào
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

Tốt lắm. Bạn đã cài đặt và tùy chỉnh xong thành phần mở rộng Gatsby đầu tiên!

## Tạo các thành phần bố cục

Bây giờ chúng ta học tiếp về các các thành phần bố cục. Để chuẩn bị cho phần này, hãy thêm một vài trang mới vào trong project của bạn bao gồm: một trang about và một trang contact.

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

Trang about mới sẽ trông như thế này:

![about-uncentered](about-uncentered.png)

Hmm. Sẽ tốt hơn nếu nội dung của hai trang mới được canh lề ở giữa tương tự như trang index. Và sẽ tốt hơn nếu có sự điều hướng toàn cục để khách dễ dàng hơn trong việc tìm kiếm và truy cập các trang phụ.

Bạn sẽ thực hiện các sự thay đổi này thông qua thành phần bố cục đầu tiên.

### ✋ Tạo thành phần bố cục đầu tiên

1. Tạo một thư mục mới tại `src/components`.

2. Tạo một thành phần bố cục cơ bản tại `src/components/layout.js`:

```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    {children}
  </div>
)
```

3. Nạp thành phần bố cục mới này vào trong `src/pages/index.js` ở trang web của bạn:

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

Tốt lắm, bố cục đã xong! Nội dung trang index của bạn vẫn được canh lề ở giữa. 

Nhưng hãy thực hiện điều hướng vào `/about/`, hoặc `/contact/`. Nội dung của những trang này vẫn chưa được canh lề ở giữa.

4. Nạp thành phần bố cục vào trong `about.js` và `contact.js` (tương tự như bạn đã làm cho `index.js` ở bước trước đó).

Nội dung tất cả ba trang của bạn đã được canh lề ở giữa bằng cách sử dụng chung một thành phần bố cục!

### ✋ Thêm tiêu đề cho một trang web

1. Thêm đoạn sau vào thành phần bố cục mới của bạn:

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

### ✋ Thêm vào đường dẫn điều hướng giữa các trang

1. Thêm đoạn sau vào trong thành phần bố cục:

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

![with-navigation2](with-navigation2.png)

Và bạn đã hoàn thành xong! Một site gồm 3 trang với điều hướng toàn cục cơ bản.

_Thử thách:_ Với sức mạnh của "thành phần bố cục" mới, hãy thử thêm vào đầu trang, cuối trang, điều hướng toàn cục, thanh bên,... vào trang web của bạn trên nền tảng Gatsby!

## Có gì ở phần kế tiếp?

Tiếp tục [phần 4 của bài hướng dẫn](/tutorial/part-four/) để học thêm về lớp dữ liệu của Gatsby và tạo trang một cách hệ thống.
