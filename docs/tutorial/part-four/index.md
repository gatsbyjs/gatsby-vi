---
title: Dữ liệu trong Gatsby
typora-copy-images-to: ./
disableTableOfContents: true
---

Chào mừng đến Phần Bốn của bản hướng dẫn! Nửa đoạn đường rồi! Hi vọng mọi thứ đang trở
nên thoải mái hơn 😀

## Nhắc lại vắn tắt nửa đầu của phần hướng dẫn

Cho đến giờ, bạn đã học qua cách sử dụng React.js—và công cụ này mạnh mẽ như thế này khi bạn có thể dùng nó để
tạo nên những component của _chính bạn_ hoạt động như những khối cấu tạo tùy chỉnh cho những trang web.

Bạn cũng đã khám phá việc tạo kiểu cho các component bằng CSS Modules.

## Bài hướng dẫn này có những gì?

Trong bốn phần tiếp theo của hướng dẫn (bao gồm cả phần này), bạn sẽ đi sâu vào lớp dữ liệu của Gatsby, một tính năng mạnh mẽ của Gatsby cho phép bạn dễ dàng xây dựng trang web từ Markdown, WordPress, headless CMSs, và tất cả những nguồn dữ liệu khác từ tất cả các loại.

**LƯU Ý:** Lớp dữ liệu của Gatsby được hỗ trợ bởi GraphQL. Để được hướng dẫn sâu hơn về
GraphQL, chúng tôi khuyến cáo bạn xem qua [Cách dùng GraphQL](https://www.howtographql.com/).

## Dữ liệu trong Gatsby

Một trang web bao gồm bốn phần: HTML, CSS, JS, và dữ liệu. Nửa phần đầu của
phần hướng dẫn đã tập trung vào ba phần đầu tiên. Bây giờ chúng ta sẽ học làm thế nào để vận dụng dữ liệu trong
những trang web Gatsby.

**Dữ liệu là gì?**

Một câu trả lời rất chuyên môn trong khoa học máy tính sẽ là: dữ liệu là những thứ như `"strings"`,
số nguyên (`42`), đối tượng (objects) (`{ pizza: true }`), vân vân.

Tuy nhiên, nhằm mục địch làm việc với Gatsby, một câu trả lời hữu ích hơn là
"tất cả những gì tồn tại bên ngoài một React component".

Đến bây giờ, bạn đã viết văn bản và thêm hình ảnh _trực tiếp_ vào những component.
Đó là một cách _tuyệt vời_ để tạo dựng nhiều trang web. Thế nhưng, thường bạn sẽ muốn lưu trữ
dữ liệu _bên ngoài_ các component và sau đó mới mang dữ liệu _vào trong_ compoennt khi
cần.

Nếu bạn đang xây dựng một trang web với WordPress (để những người đóng góp khác
có một giao diện đẹp mắt để thêm và bảo trì nội dung) và Gatsby, _dữ liệu_
cho trang web (các trang và các bài đăng) đều trong WordPress và bạn _kéo_ dữ liệu đó, khi
cần, vào trong component của bạn.

Dữ liệu cũng có thể tồn tại trong định dạng tập tin như Markdown, CSV, v.v.
cũng như các cơ sở dữ liệu và mọi loại API.

**Lớp dữ liệu của Gatsby cho phép bạn kéo dữ liệu từ các nguồn này (và bất cứ một nguồn nào khác)
trực tiếp vào các component của bạn**—trong hình và dạng mà bạn mong muốn.

## Sử dụng Dữ Liệu Phi Cấu Trúc so với GraphQL

### Tôi có cần phải dùng GraphQL và các source plugin đế kéo dữ liệu vào các trang web Gatsby không?

Hoàn toàn không! Bạn có thể dùng node API `createPages` để kéo dữ liệu phi cấu trúc trực tiếp vào những trang Gatsby, thay vì thông qua lớp dữ liệu GraphQL. Đây là lựa chọn tuyệt vời cho những trang web nhỏ, trong khi GraphQL và những source plugin có thể giúp tiết kiệm thời gian với những trang web phức tạp hơn.

Hãy xem qua hướng dẫn [Sử dụng Gatsby mà không cần GraphQL](/docs/using-gatsby-without-graphql/) để học cách kéo dữ liệu vào trang web Gatsby của bạn bằng cách sử dụng node API `createPages` và được thấy một trang web ví dụ!

### Khi nào tôi cần dùng dữ liệu phi cấu trúc hay là GraphQL?

Nếu bạn đang xây dựng một trang web nhỏ, một cách hiệu quả để tạo là kéo dữ liệu phi cấu trúc vào như được bày ra trong chỉ dẫn này, bằng API `createPages`, và nếu trang web trở nên phức tạp hơn sau này, bạn tiến đến xây dựng những trang web phức tạp hơn, hoặc bạn muốn biến đổi dữ liệu của bạn, hãy làm theo các bước sau:

1. Xem qua [Thư viện Plugin](/plugins/) để xem nếu các source plugin và/hoặc transformer plugin mà bạn muốn sử dụng đã tồn tại hay chưa
2. Nếu chúng không tồn tại, hãy đọc hướng dẫn [Biên soạn Plugin](/docs/creating-plugins/) và cân nhắc việc tự tạo riêng cho bạn!

### Cách lớp dữ liệu của Gatsby dùng GraphQL để kéo dữ liệu vào các component

Có rất nhiều lựa chọn để tải dữ liệu vào các React component. Một trong những cách
phổ biến và mạnh mẽ nhất là một công nghệ gọi là
[GraphQL](http://graphql.org/).

GraphQL được phát minh bởi Facebook để giúp các kỹ sư sản phẩm _kéo_ dữ liệu cần thiết vào
những component.

GraphQL là một ngôn ngữ truy vấn (**q**uery **l**anguage, _QL_ là một phần của tên nó). Nếu bạn
quen thuộc với SQL, ngôn ngữ này hoạt động một cách tương tự vậy. Bằng cách sử dụng một cú pháp đặc biệt, bạn mô tả
dữ liệu mà bạn muốn trong component của bạn và dữ liệu đó sẽ được đưa
đến bạn.

Gatsby vận dụng GraphQL để cho phép các component khai báo dữ liệu mà nó cần.

## Tạo một trang web ví dụ mới

Hãy tạo một trang web mới cho phần hướng dẫn này. Bạn sẽ tạo một trang blog Markdown gọi là "Pandas Eating Lots". Trang blog này sẽ tập trung vào trình bày những bức ảnh và video tuyệt nhất của những chú gấu trúc đang ăn rất nhiều thức ăn. Trong quá trình tạo, bạn sẽ được va chạm với GraphQL và khả năng hỗ trợ Markdown của Gatsby.

Hãy mở một cửa sổ terminal mới và chạy những dòng lệnh sau để tạo một trang web Gatsby mới trong một thư mục gọi là `tutorial-part-four`. Sau đó điều hướng tới thư mục mới đó:

```shell
gatsby new tutorial-part-four https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-four
```

Tiếp theo hãy cài đặt vài thành phần phụ thuộc (dependencies) cần thiết khác tại thư mục gốc của dự án. Bạn sẽ dùng Kiểu chữ với chủ đề
"Kirkham", và bạn sẽ thử qua một thư viện CSS-trong-JS, ["Emotion"](https://emotion.sh/):

```shell
npm install --save gatsby-plugin-typography typography react-typography typography-theme-kirkham gatsby-plugin-emotion @emotion/core
```

Thiết lập một trang web tương tự với những gì bạn có khi dừng lại ở [Phần Ba](/tutorial/part-three). Trang web này sẽ có một component bố cục và hai component trang:

```jsx:title=src/components/layout.js
import React from "react"
import { css } from "@emotion/core"
import { Link } from "gatsby"

import { rhythm } from "../utils/typography"

export default ({ children }) => (
  <div
    css={css`
      margin: 0 auto;
      max-width: 700px;
      padding: ${rhythm(2)};
      padding-top: ${rhythm(1.5)};
    `}
  >
    <Link to={`/`}>
      <h3
        css={css`
          margin-bottom: ${rhythm(2)};
          display: inline-block;
          font-style: normal;
        `}
      >
        Pandas Eating Lots
      </h3>
    </Link>
    <Link
      to={`/about/`}
      css={css`
        float: right;
      `}
    >
      About
    </Link>
    {children}
  </div>
)
```

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => (
  <Layout>
    <h1>Amazing Pandas Eating Things</h1>
    <div>
      <img
        src="https://2.bp.blogspot.com/-BMP2l6Hwvp4/TiAxeGx4CTI/AAAAAAAAD_M/XlC_mY3SoEw/s1600/panda-group-eating-bamboo.jpg"
        alt="Group of pandas eating bamboo"
      />
    </div>
  </Layout>
)
```

```jsx:title=src/pages/about.js
import React from "react"
import Layout from "../components/layout"

export default () => (
  <Layout>
    <h1>About Pandas Eating Lots</h1>
    <p>
      We're the only site running on your computer dedicated to showing the best
      photos and videos of pandas eating lots of food.
    </p>
  </Layout>
)
```

```javascript:title=src/utils/typography.js
import Typography from "typography"
import kirkhamTheme from "typography-theme-kirkham"

const typography = new Typography(kirkhamTheme)

export default typography
export const rhythm = typography.rhythm
```

`gatsby-config.js` (cần phải nằm trong thư mục gốc của dự án của bạn, không được dưới src)

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

Hãy thêm những tập tin trên rồi chạy lệnh `gatsby develop`, như thường lệ, và bạn sẽ nhìn thấy như sau:

![bắt đầu](start.png)

Bạn đã có thêm một trang web nhỏ với 1 bố cục và 2 trang.

Bây giờ bạn có thể bắt đầu truy vấn 😋

## Truy vấn GraphQL đầu tiên của Bạn

Khi tạo trang web, có thể bạn sẽ muốn tái sử dụng những mẩu dư liệu dùng chung -- như _tiêu đề của trang web_ chẳng hạn. Hãy nhìn vào trang `/about/`. Bạn sẽ để ý rằng bạn có tiêu đề của trang web (`Pandas Eating Lots`) trong cả component bố cục (header của cả trang web) cũng như trong `<h1 />` của trang `about.js` (header riêng của trang).

Nếu nhưng bạn muốn thay đổi tiêu đề của trang web trong tương lai thì sao? Bạn sẽ phải tìm dòng tiêu đề trong khắp mọi component và chỉnh sửa từng trường hợp một. Việc này cực bất tiện và dễ dính lỗi, đặc biệt đối với những trang web lớn hơn, phức tạp hơn. Thay vì thế, bạn có thể lưu trữ tiêu đề tại một vị trí và trỏ đến vị trí đó từ các file khác; thay đổi tiêu đề tại một nơi duy nhất, và Gatsby sẽ _kéo_ tiêu đề đã được thay đổi của bạn vào trong những file được liên kết với tiêu đề đó.

Nơi để lưu trữ những mẩu dữ liệu chung này là đối tượng `siteMetadata` trong file `gatsby-config.js`. Hãy thêm tiêu đề trang web của bạn vào file `gatsby-config.js`:

```javascript:title=gatsby-config.js
module.exports = {
  // highlight-start
  siteMetadata: {
    title: `Title from siteMetadata`,
  },
  // highlight-end
  plugins: [
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

Hãy khởi động lại máy chủ phát triển.

### Sử dụng truy vấn trang

Bây giờ tiêu đề trang web đã sẵn sàng để được truy vấn; Hãy thêm nó vào file `about.js` bằng [truy vấn trang](/docs/page-query):

```jsx:title=src/pages/about.js
import React from "react"
import { graphql } from "gatsby" // highlight-line
import Layout from "../components/layout"

// highlight-next-line
export default ({ data }) => (
  <Layout>
    <h1>About {data.site.siteMetadata.title}</h1> {/* highlight-line */}
    <p>
      We're the only site running on your computer dedicated to showing the best
      photos and videos of pandas eating lots of food.
    </p>
  </Layout>
)

// highlight-start
export const query = graphql`
  query {
    site {
      siteMetadata {
        title
      }
    }
  }
`
// highlight-end
```

Thành công rồi! 🎉

![Tiêu đề của trang được kéo từ siteMetadata](site-metadata-title.png)

Câu truy vấn GraphQL cơ bản thu hồi `tiêu đề` trong `about.js` đã thay đổi là:

```graphql:title=src/pages/about.js
{
  site {
    siteMetadata {
      title
    }
  }
}
```

> 💡 Trong [phần năm](/tutorial/part-five/#introducing-graphiql), bạn sẽ gặp một công cụ cho phép chúng ta khám phá và tương tác với dữ liệu sẵn có thông qua GraphQL, và giúp hình thành nên những câu truy vấn giống như ở trên.

Các câu truy vấn trang tồn tại bên ngoài định nghĩa của component -- theo quy ước là ở cuối tập tin chứa component trang -- và chỉ có trong các component trang.

### Sử dụng StaticQuery

[StaticQuery](/docs/static-query/) là một API mới được giới thiệu trong Gatsby v2 cho phép các component không-phải-trang (như component `layout.js` của bạn), thu dữ liệu thông qua các câu truy vấn GraphQL.
Hãy dùng phiên bản hook mới được được giới thiệu — [`useStaticQuery`](/docs/use-static-query/).

Hãy thực hiện một vài thay đổi trong file `src/components/layout.js` của bạn để có thể dùng hook `useStaticQuery` và đề cập đến `{data.site.siteMetadata.title}` sử dụng dữ liệu này. Khi bạn đã hoàn thành thay đổi, file của bạn sẽ trông giống như thế này:

```jsx:title=src/components/layout.js
import React from "react"
import { css } from "@emotion/core"
// highlight-next-line
import { useStaticQuery, Link, graphql } from "gatsby"

import { rhythm } from "../utils/typography"
// highlight-start
export default ({ children }) => {
  const data = useStaticQuery(
    graphql`
      query {
        site {
          siteMetadata {
            title
          }
        }
      }
    `
  )
  return (
    // highlight-end
    <div
      css={css`
        margin: 0 auto;
        max-width: 700px;
        padding: ${rhythm(2)};
        padding-top: ${rhythm(1.5)};
      `}
    >
      <Link to={`/`}>
        <h3
          css={css`
            margin-bottom: ${rhythm(2)};
            display: inline-block;
            font-style: normal;
          `}
        >
          {data.site.siteMetadata.title} {/* highlight-line */}
        </h3>
      </Link>
      <Link
        to={`/about/`}
        css={css`
          float: right;
        `}
      >
        About
      </Link>
      {children}
    </div>
    // highlight-start
  )
}
// highlight-end
```

Thêm một thành công nữa! 🎉

![Tiêu đề trang và tiêu đề bố cục đều được kéo từ siteMetadata](site-metadata-two-titles.png)

Vì sao lại dùng hai câu truy vấn khác nhau ở đây? Những ví dụ này là giới thiệu nhanh cho
các dạng truy vấn, cách chúng được định dạng, và nơi chúng được vận dụng. Hiện tại,
hãy ghi nhớ rằng chỉ trang mới có thể tạo câu truy vấn trang. Các component không-phải-trang, như
Layout, có thể sử dụng StaticQuery. [Phần 7](/tutorial/part-seven/) của hướng dẫn này sẽ giải thích về các dạng truy vấn
ở mức độ sâu hơn.

Nhưng hãy khôi phục lại tiêu đề thật sự.

Một trong những nghuyên tắc cốt lõi của Gatsby đó là _những nhà sáng tạo cần một kết nối trực tiếp với những gì họ đang tạo nên_ ([ngã mũ thán phục với Bret Victor](http://blog.ezyang.com/2012/02/transcript-of-inventing-on-principle/)). Nói cách khác, khi bạn thực hiện thay đổi trong code, bạn nên ngay lập tức thấy được hiệu ứng của thay đổi đó. Bạn điều khiển đầu vào của Gatsby và bạn thấy được đầu ra mới hiện lên trên màn hình.

Nên hầu hết mọi nơi, những thay đổi bạn tạo ra sẽ lập tức có hiệu lực. Hãy sửa file `gatsby-config.js` lần nữa, lần này đổi `title` trở lại thành "Pandas Eating Lots". Sự thay đổi sẽ hiện lên rất nhanh trong các trang web của bạn.

![Cả hai tiêu đề đều hiện Pandas Eating Lots](pandas-eating-lots-titles.png)

## Tiếp theo là gì?

Tiếp đến, bạn sẽ học về cách kéo dữ liệu vào trang web Gatsby của bạn bằng cách sử dụng
GraphQL với những source plugin trong [phần năm](/tutorial/part-five/) của
hướng dẫn.
