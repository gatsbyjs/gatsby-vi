---
title: Giới thiệu về cách sử dụng CSS trong Gatsby
typora-copy-images-to: ./
disableTableOfContents: true
---

<!-- Idea: Create a glossary to refer to. A lot of these terms get jumbled -->

<!--
  - Global styles
  - Component css
  - CSS-in-JS
  - CSS Modules

-->

Chào mừng bạn đến với phần hai của trương mục hướng dẫn về Gatsby

## Hướng dẫn này sẽ nói về điều gì?

Trong phần này, các bạn sẽ được tìm hiểu về những lựa chọn nhằm tạo kiểu các trang web Gatsby và hiểu sâu hơn về sử dụng React components trong việc xây dựng các trang web.

## Sử dụng tạo kiểu toàn cục

Mỗi trang web đều có một tạo kiểu toàn cục. Chúng bao gồm những đặc trưng như kiểu chữ và tông màu nền. Các kiểu mẫu này đặt ra góc nhìn tổng thể về trang web - giống như là màu và kết cấu của một bức tường cho góc nhìn tổng thể về một căn phòng.

### Tạo ra những định dạng toàn cục với các tập tin CSS tiêu chuẩn

Một trong những cách trực tiếp nhất để thêm tạo kiểu toàn cục là sử dụng một bản định kiểu (stylesheet) `.css` toàn cục

#### ✋ Tạo một trang web Gatsby mới

Bắt đầu bằng việc tạo một trang web Gatsby. Cách tốt nhất (đặc biệt nếu bạn chưa quen với sử dụng dòng lệnh) là đóng cửa sổ terminal bạn đã sử dụng cho [phần một](/tutorial/part-one/) và mở một cửa sổ terminal mới cho phần hai.

Mở một cửa sổ terminal mới, tạo một trang web Gatsby "hello world" mới, và chạy máy chủ phát triển:

```shell
gatsby new tutorial-part-two https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-two
```

Bây giờ bạn đã có một trang web Gatsby (dựa trên mẫu khởi động Gatsby "hello world") với cấu trúc như sau:

```text
├── package.json
├── src
│   └── pages
│       └── index.js
```

#### ✋ Thêm định dạng vào tập tin css

1. Tạo một tập tin `.css` bên trong dự án của bạn:

```shell
cd src
mkdir styles
cd styles
touch global.css
```

> Chú ý: Bạn có thể thoải mái tạo các thư mục và tập tin này bằng trình soạn thảo code của bạn nếu muốn.

Bây giờ bạn sẽ có một cấu trúc như sau:

```text
├── package.json
├── src
│   └── pages
│       └── index.js
│   └── styles
│       └── global.css
```

2. Định nghĩa một vài định dạng trong tập tin `global.css`:

```css:title=src/styles/global.css
html {
  background-color: lavenderblush;
}
```

> Chú ý: Vị trí đặt tập tin css như ví dụ trên bên trong thư mục `/src/styles/` là tùy ý của bạn.

#### ✋ Tích hợp bản định kiểu vào trong `gatsby-browser.js`

1. Tạo tập tin `gatsby-browser.js`

```shell
cd ../..
touch gatsby-browser.js
```

Cấu trúc tập tin của dự án của bạn sẽ như sau:

```text
├── package.json
├── src
│   └── pages
│       └── index.js
│   └── styles
│       └── global.css
├── gatsby-browser.js
```

> 💡 Vậy `gatsby-browser.js` là gì? Bạn không cần phải quan tâm về nó quá nhiều bây giờ, bạn chỉ cần biết `gatsby-browser.js` là một trong số ít những tập tin đặc biệt mà Gatsby tìm và sử dụng (nếu có tồn tại). Ở đây, cách đặt tên cho tập tin **là** quan trọng. Nếu bạn muốn tìm hiểu thêm ngay bây giờ, bạn có thể xem ở [tài liệu này](/docs/browser-apis/).

2. Nhúng bản định kiểu được tạo gần đây của bạn vào tập tin `gatsby-browser.js`:

```javascript:title=gatsby-browser.js
import "./src/styles/global.css"

// hoặc là:
// require('./src/styles/global.css')
```

> Chú ý: Cú pháp CommonJS (`require`) và ES Module (`import`) đều có thể sử đụng được ở đây. Nếu bạn không biết phải chọn cú pháp nào, thì thường `import` là một mặc định tốt. Tuy nhiên, khi làm việc với các tập tin chỉ chạy trong môi trường Node.js (như là `gatsby-node.js`), bạn phải cần sử dụng cú pháp `require` .

3. Chạy máy chủ phát triển:

```shell
gatsby develop
```

Nếu bạn quan sát dự án của bạn trên trình duyệt, bạn có thể thấy màu tím Lavender được áp dụng cho mẫu khởi động "hello world":

![Lavender Hello World!](global-css.png)

> Thông tin thêm: Mục này của hướng dẫn tập trung vào cách nhanh nhất và trực tiếp nhất để bắt đầu tạo kiểu một trang web Gatsby — nhúng các tập tin CSS tiêu chuẩn một cách trực tiếp, thông qua `gatsby-browser.js`. Trong đa số các trường hợp, cách tốt nhất để thêm vào định dạng toàn cục là dùng những component bố cục dùng chung. [Tham khảo tài liệu](/docs/global-css/) để biết thêm thông tin về cách thức đó.

## Sử dụng CSS trong phạm vi của component

Cho đến nay, chúng ta đã bàn về phương pháp tiếp cận truyền thống về việc sử dụng những bản định mẫu css tiêu chuẩn. Bây giờ, chúng ta sẽ bàn về những phương pháp mô-đun hóa CSS về nhiều dạng để giải quyết vấn đề tạo kiểu nằng cách định hướng theo component.

### CSS Modules

Cùng tìm hiểu **CSS Modules**. trích dẫn từ
[the CSS Module homepage](https://github.com/css-modules/css-modules):

> Một **CSS Module** là một tập tin CSS mà ở đó tất cả các tên gọi class và hiệu ứng.
> được mặc định giới hạn trong phạm vi cục bộ.

Những CSS Modules rất phổ biến vì chúng cho phép bạn viết CSS như bình thường nhưng an toàn hơn. Công cụ sẽ tự động tạo ra tên gọi độc nhất dành cho class và hiệu ứng, cho nên bạn không cần phải lo lắng về vấn đề đụng chạm tên gọi của bộ chọn.

Với CSS Modules, Gatsby có thể được sử dụng ngay lập tức. Phương pháp này được khuyến nghị sử dụng cho những ai mới bắt đầu phát triển trên nền tảng Gatsby nói riêng (cũng như là React nói chung).

#### ✋ Xây dựng một trang web mới sử dụng CSS Modules

Trong mục này, bạn sẽ tạo một component của một trang mới và tạo kiểu component đó bằng việc sử dụng CSS Modules.

Đầu tiên, tạo một component mới tên là `Container`.

1. Tạo một thư mục mới tại `src/components` và sau đó, trong thư mục vừa tạo này, tạo một tập tin gọi là `container.js` và sao chép những dòng sau đây:

```jsx:title=src/components/container.js
import React from "react"
import containerStyles from "./container.module.css"

export default ({ children }) => (
  <div className={containerStyles.container}>{children}</div>
)
```

Bạn sẽ thấy rằng bạn đã nhúng một tập tin mô-đun css tên là `container.module.css`. Cùng tạo tập tin đó nào.

2. Trong cùng thư mục (`src/components`), tạo tập tin `container.module.css` và sao chép những dòng sau đây:

```css:title=src/components/container.module.css
.container {
  margin: 3rem auto;
  max-width: 600px;
}
```

Bạn sẽ thấy rằng tên của tập tin kết thúc với `.module.css` thay vì thường là `.css`. Đây là cách để bạn cho Gatsby biết rằng tập tin CSS này nên được xử lý như là một mô-đun CSS thay vì là một tập tin CSS thông thường.

3. Tạo một component trang mới tại
   `src/pages/about-css-modules.js`:

```jsx:title=src/pages/about-css-modules.js
import React from "react"

import Container from "../components/container"

export default () => (
  <Container>
    <h1>About CSS Modules</h1>
    <p>CSS Modules are cool</p>
  </Container>
)
```

Bây giờ, nếu bạn mở `http://localhost:8000/about-css-modules/`, trang của bạn sẽ nhìn giống như sau:

![Trang web với định dạng mô-đun CSS](css-modules-basic.png)

#### ✋ Tạo kiểu cho một component sử dụng CSS Modules

Trong mục này, bạn sẽ tạo một danh sách về người với tên, ảnh đại diện, và tiểu sử cá nhân. Bạn sẽ tạo một component tên là `<User />` và tạo kiểu component này sử dụng CSS Modules.

1. Tạo tập tin CSS tại `src/pages/about-css-modules.module.css`.

2. Sao chép những dòng sau vào một tập tin mới:

```css:title=src/pages/about-css-modules.module.css
.user {
  display: flex;
  align-items: center;
  margin: 0 auto 12px auto;
}

.user:last-child {
  margin-bottom: 0;
}

.avatar {
  flex: 0 0 96px;
  width: 96px;
  height: 96px;
  margin: 0;
}

.description {
  flex: 1;
  margin-left: 18px;
  padding: 12px;
}

.username {
  margin: 0 0 12px 0;
  padding: 0;
}

.excerpt {
  margin: 0;
}
```

3. Nhúng tập tin `src/pages/about-css-modules.module.css` vào trang `about-css-modules.js` mà bạn tạo trước đó bằng việc thay đổi những dòng đầu tiên của tập tin như sau:

```javascript:title=src/pages/about-css-modules.js
import React from "react"
// highlight-next-line
import styles from "./about-css-modules.module.css"
import Container from "../components/container"

// highlight-next-line
console.log(styles)
```

Mã lệnh `console.log(styles)` sẽ in kết quả của việc nhúng tập tin để bạn có thể thấy kết quả của tập tin `./about-css-modules.module.css` đã qua xử lý. Nếu bạn mở bảng điều khiển (console) của nhà lập trình (ví dụ như developer tools của Firefox hay là Chrome) trên trình duyệt của bạn, bạn sẽ thấy:

![Kết quả của việc nhúng mô-đun CSS trong console](css-modules-console.png)

Nếu bạn so sánh với tập tin CSS của mình, bạn sẽ thấy mỗi class bây giờ là một trường (key) bên trong đối tượng được nh1ung và mỗi trường chỉ đến một chuỗi kí tự dài. Ví dụ `avatar` chỉ đến `src-pages----about-css-modules-module---avatar---2lRF7`. Những trường này là những tên class mà CSS Modules tạo ra. Chúng được bảo đảm về sự duy nhất xuyên suốt trang web của bạn. Và vì bạn nhúng các tập tin này để sử dụng các class, cho nên sẽ không có thắc mắc về vị trí sử dụng của một số CSS.

4. Tạo một inline component mới gọi là `<User />` bên trong trang `about-css-modules.js`.
   Điều chỉnh `about-css-modules.js` sao cho giống như sau:

```jsx:title=src/pages/about-css-modules.js
import React from "react"
import styles from "./about-css-modules.module.css"
import Container from "../components/container"

console.log(styles)

// highlight-start
const User = props => (
  <div className={styles.user}>
    <img src={props.avatar} className={styles.avatar} alt="" />
    <div className={styles.description}>
      <h2 className={styles.username}>{props.username}</h2>
      <p className={styles.excerpt}>{props.excerpt}</p>
    </div>
  </div>
)
// highlight-end

export default () => (
  <Container>
    <h1>About CSS Modules</h1>
    <p>CSS Modules are cool</p>
    {/* highlight-start */}
    <User
      username="Jane Doe"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
      excerpt="I'm Jane Doe. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
    <User
      username="Bob Smith"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
      excerpt="I'm Bob Smith, a vertically aligned type of guy. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
    {/* highlight-end */}
  </Container>
)
```

> Thông tin thêm: Nhìn chung, nếu bạn sử dụng một component ở nhiều vị trí khác nhau trên cùng một trang web, nó nên được đặt thành 1 mô-đun riêng trong thư mục "components". Nhưng nếu nó chỉ được sử dụng trong 1 tập tin duy nhất, hãy tạo nó "inline" (trong cùng file mà nó được sử dụng).

Trang kết quả cuối cùng nên trông giống như sau:

![Trang danh sách người dùng tạo với CSS Modules](css-modules-userlist.png)

### CSS-in-JS

CSS-in-JS là một phương pháp tạo kiểu định hướng theo component. Một cách chung nhất, nó là một kiểu mẫu mà ở đó [CSS được viết inline bằng cách sử dụng JavaScript](https://reactjs.org/docs/faq-styling.html#what-is-css-in-js).

#### Sử dụng CSS-in-JS với Gatsby

Có rất nhiều thư viện CSS-in-JS và nhiều trong số chúng đã có plugins của Gatsby. Chúng ta sẽ không bàn về một ví dụ của CSS-in-JS trong phần hướng dẫn này, tuy nhiên chúng tôi khuyến khích bạn [tìm hiểu](/docs/styling/) về những gì hệ sinh thái này có thể cung cấp. Chúng tôi có các hướng dẫn ngắn về 2 thư viện tiêu biểu là [Emotion](/docs/emotion/) và [Styled Components](/docs/styled-components/).

#### Tài liệu tham khảo về CSS-in-JS

Nếu bạn muốn tìm hiểu thêm, hãy xem [Bài huyết trình năm 2014 đã khởi động trào lưu này của Christopher "vjeux" Chedeau](https://speakerdeck.com/vjeux/react-css-in-js) và [Phát biểu gần đây hơn của Mark Dalgleish về "Một ngôn ngữ tạo kiểu thống nhất"](https://medium.com/seek-blog/a-unified-styling-language-d0c208de2660).

### Những lựa chọn CSS khác

Gatsby hỗ trợ gần như tất cả các lựa chọn tạo kiểu (Nếu như lựa chọn CSS yêu thích của bạn chưa có Gatsby plugin, [vui lòng đóng góp nếu có thể!](/contributing/how-to-contribute/))

- [Typography.js](/packages/gatsby-plugin-typography/)
- [Sass](/packages/gatsby-plugin-sass/)
- [JSS](/packages/gatsby-plugin-jss/)
- [Stylus](/packages/gatsby-plugin-stylus/)
- [PostCSS](/packages/gatsby-plugin-postcss/)

và nhiều hơn nữa!

## Tiếp theo là gì?

Bây giờ ta sẽ tiếp tục đến với [phần ba của hướng dẫn](/tutorial/part-three/), nơi mà bạn sẽ được học về Gatsby plugins và cách bố trí các component.
