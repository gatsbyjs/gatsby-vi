---
title: Chuẩn bị cho một trang web Lên Sóng
typora-copy-images-to: ./
disableTableOfContents: true
---

Wow! Bạn đã đi cả một chặng đường dài! Bạn đã được học cách:

- tạo các trang web Gatsby mới
- tạo các trang và component
- tạo kiểu cho các component
- thêm các plugin vào một trang web
- cung ứng & biến đổi dữ liệu
- sử dụng GraphQL để truy vấn dữ liệu cho các trang
- tạo trang từ dữ liệu của bạn bằng phương pháp lập trình

Trong phần cuối này, bạn sẽ được xem qua một số bước thông dụng để chuẩn bị cho một website lên sóng bằng cách làm quen với một công cụ chuẩn đoán trang web mạnh mẽ gọi là [Lighthouse](https://developers.google.com/web/tools/lighthouse/). Trong quá trình đó, chúng tôi sẽ giới thiệu một vài plugin nữa mà bạn sẽ thường muốn dùng trong trang web Gatsby của bạn.

## Đánh giá với Lighthouse

Trích từ [website của Lighthouse](https://developers.google.com/web/tools/lighthouse/):

> Lighthouse là một công cụ mã nguồn mở, tự động hóa cho việc nâng cao chất lượng các trang web. Bạn có thể chạy nó trên bất kì trang web nào, dù là công cộng hay yêu cầu xác thực. Nó có các đánh giá cho hiệu suất, khả năng tiếp cận (accessibility), ứng dụng web nâng cao (progressive web apps - PWAs), và hơn thế nữa.

Lighthouse được tích hợp trong Chrome DevTools (công cụ cho nhà phát triển của Chrome). Chạy công cụ đánh giá -- sau đó giải quyết các lỗi nó tìm được và thực hiện những cải tiến mà nó đề xuất -- là một cách tuyệt vời để chuẩn bị cho trang web của bạn lên sóng. Nó giúp bạn tự tin rằng trang web của bạn nhanh và dễ tiếp cận nhất có thể.

Hãy thử ngay đi nào!

Đầu tiên, bạn cần tạo một production build (phiên bản phát hành) của trang web Gatsby của bạn. Máy chủ phát triển Gatsby được tối ưu hóa cho việc phát triển nhanh; Tuy nhiên, trang web mà nó tạo ra, dù rất giống với phiên bản phát hành của trang web, không được tối ưu bằng.

### ✋ Tạo một production build

1.  Dừng máy chủ phát triển (nếu nó vẫn đang chạy) và chạy câu lệnh sau:

```shell
gatsby build
```

> 💡 Như bạn đã học trong [phần 1](/tutorial/part-one/), câu lệnh này dựng một production build của trang web của bạn và xuất các file tĩnh đã được dựng vào trong thư mục `public`.

2.  Xem trang web phát hành một cách cục bộ. Hãy hạy lệnh:

```shell
gatsby serve
```

Một khi câu lệnh này bắt đầu, bạn có thể xem trang web của bạn tại [`localhost:9000`](http://localhost:9000).

### Chạy một đánh giá Lighthouse

Bây giờ bạn sẽ chạy bài kiểm tra Lighthouse đầu tiên của bạn.

1. Nếu chưa thực hiện, bạn hãy mở trang web trong Chế độ Ẩn danh của Chrome để không có tiện ích mở rộng nào can thiệp vào bài kiểm tra. Sau đó, hãy mở Chrome DevTools.

2. Ấn vào tab "Audits" nơi bạn sẽ thấy một màn hình như sau:

![Bắt đầu đánh giá với Lighthouse](./lighthouse-audit.png)

3.  Click vào "Perform an audit..." (Tất cả các dạng kiểm toán sẽ được chọn theo mặc định). Sau đó click "Run audit". (Nó sẽ mất tầm một phút để chạy bài đánh giá). Một khi đánh giá xong, bạn sẽ thấy kết quả trông giống như thế này:

![Kết quả đánh giá từ Lighthouse](./lighthouse-audit-results.png)

Như bạn có thể thấy, hiệu suất của Gatsby là vô cùng đột phá, nhưng bạn vẫn thiếu những thứ cho PWA, Accessibility, Best Practices, và SEO để cải thiện điểm số của bạn (đồng thời làm cho trang web của bạn thân thiện hơn với người dùng và các công cụ tìm kiếm).

## Thêm một tập tin kê khai

Có vẻ như bạn có một điểm hơi tụt hậu trong mục "Progressive Web App". Cùng giải quyết điều đó nào.

Nhưng trước hết, chính xác thì PWAs _là gì_?

Chúng là những trang web thông thường nhưng tận dụng được những chức năng của trình duyệt hiện đại nhằm tăng cường trải nghiệm web thông qua những chức năng và lợi ích như là của một ứng dụng. Hãy xem qua [tổng quan của Google](https://developers.google.com/web/progressive-web-apps/) về những thứ định nghĩa một trải nghiệm PWA.

Sự bao gồm của một bản kê khai ứng dụng web (web app manifest) là một trong ba [yêu cầu cơ bản cho một PWA](https://alistapart.com/article/yes-that-web-project-should-be-a-pwa#section1) được chấp nhận rộng rãi.

Trích [Google](https://developers.google.com/web/fundamentals/web-app-manifest/):

> Bản kê khai ứng dụng web là một tập tin JSON đơn giản báo cho trình duyệt về ứng dụng web của bạn và cách nó hành xử khi được 'cài đặt' trên điện thoại hay máy tính của người dùng.

[Plugin kê khai của Gatsby](/packages/gatsby-plugin-manifest/) cấu hình Gatsby để tạo ra một tập tin `manifest.webmanifest` trên mỗi trang web được dựng.

### ✋ Sử dụng `gatsby-plugin-manifest`

1.  Cài đặt plugin:

```shell
npm install --save gatsby-plugin-manifest
```

2. Thêm một favicon (icon tiêu đề) cho ứng dụng của bạn trong `src/images/icon.png`. Cho mục đích của bài hướng dẫn này bạn có thể dùng [biểu tượng mẫu này](https://raw.githubusercontent.com/gatsbyjs/gatsby/master/docs/tutorial/part-eight/icon.png), nếu bạn không có sẵn. Biểu tượng này là cần thiết để dựng tất cả các hình ảnh cho bản kê khai. Để biết thêm thông tin, xem qua tài liệu cho [`gatsby-plugin-manifest`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-manifest/README.md).

3. Thêm plugin vào mảng `plugins` trong tập tin `gatsby-config.js`.

```javascript:title=gatsby-config.js
{
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: `GatsbyJS`,
        short_name: `GatsbyJS`,
        start_url: `/`,
        background_color: `#6b37bf`,
        theme_color: `#6b37bf`,
        // Để kính hoạt bản thông báo "Add to Homescreen" vô hiệu hóa UI của trình duyệt (bao gồm nút back)
        // hãy xem qua https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // Đường dẫn này là tương đối so với thư mục gốc của trang web
      },
    },
  ]
}
```

Đó là tất cả những gì bạn cần để bắt đầu với việc thêm một bản kê khai web vào một trang web Gatsby. Ví dụ ở trên phản ảnh cấu hình cơ bản -- Hãy xem qua [tài liệu tham khảo về plugin](/packages/gatsby-plugin-manifest/?=gatsby-plugin-manifest#automatic-mode) để có nhiều tùy chọn hơn.

## Thêm hỗ trợ ngoại tuyến

Một yêu cầu khác để một trang web đủ điều kiện là một PWA là vận dụng một [service worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API). Một service worker sẽ chạy nền, quyết định việc phục vụ mạng hay là những nội dung được cached (lưu trữ sẵn để dùng sau) dựa trên trạng thái kết nối, cho phép một trải nghiệm ngoại tuyết trơn tru và trong kiểm soát.

[Plugin ngoại tuyến của Gatsby](/packages/gatsby-plugin-offline/) làm cho một trang web Gatsby hoạt động ngoại tuyến và trở nên chống chịu hơn đối với kết nối mạng kém bằng cách tạo một service worker cho trang web của bạn.

### ✋ Sử dụng `gatsby-plugin-offline`

1.  Cài đặt plugin:

```shell
npm install --save gatsby-plugin-offline
```

2.  Thêm plugin vào mảng `plugins` trong tập tin `gatsby-config.js`.

```javascript:title=gatsby-config.js
{
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: `GatsbyJS`,
        short_name: `GatsbyJS`,
        start_url: `/`,
        background_color: `#6b37bf`,
        theme_color: `#6b37bf`,
        // Để kính hoạt bản thông báo "Add to Homescreen" vô hiệu hóa UI của trình duyệt (bao gồm nút back)
        // hãy xem qua https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // Đường dẫn này là tương đối so với thư mục gốc của trang web
      },
    },
    // highlight-next-line
    `gatsby-plugin-offline`,
  ]
}
```

Đó là tất cả những gì bạn cần để bắt đầu với service worker trên Gatsby.

> 💡 Plugin ngoại tuyến này nên được liệt kê _sau_ plugin kê khai để plugin ngoại tuyến có thể cache được tập tin `manifest.webmanifest` được tạo ra.

## Thêm siêu dữ liệu vào trang

Thêm siêu dữ liệu (metadata) vào các trang (ví dụ như tiêu đề hoặc miêu tả) là chìa khóa giúp cho các công cụ tìm kiếm như Google hiểu được nội dung của bạn và quyết định khi nào nó sẽ nổi lên trong kết quả tìm kiếm.

[React Helmet](https://github.com/nfl/react-helmet) là một gói cung cấp một giao diện dưới dạng React component để bạn quản lý [phần đầu của tài liệu](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head) của bạn.

[Plugin react helmet](/packages/gatsby-plugin-react-helmet/) của Gatsby cung cấp hỗ trợ drop-in cho dữ liệu kết xuất đồ họa máy chủ (server rendering data) cùng với Mũ bảo hiểm React. Thông qua plugin này, những thuộc tính bạn thêm vào Mũ bảo hiểm React cũng sẽ được thêm vào các trang HTML tĩnh được xây bằng Gatsby.

### ✋ Sử dụng `React Helmet` và `gatsby-plugin-react-helmet`

1.  Cài đặt cả hai gói:

```shell
npm install --save gatsby-plugin-react-helmet react-helmet
```

2.  Hãy chắc chắn rằng bạn đã có `miêu tả` và một `tác giả` được thiết lập bên trong vật thể `siteMetadata` của bạn. Đồng thời, thêm plugin `gatsby-plugin-react-helmet` vào trong tập hợp `plugins` trong tệp tin của bạn `gatsby-config.js`.

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
    // highlight-start
    description: `A simple description about pandas eating lots...`,
    author: `gatsbyjs`,
    // highlight-end
  },
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: `GatsbyJS`,
        short_name: `GatsbyJS`,
        start_url: `/`,
        background_color: `#6b37bf`,
        theme_color: `#6b37bf`,
        // Enables "Add to Homescreen" prompt and disables browser UI (including back button)
        // see https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // This path is relative to the root of the site.
      },
    },
    `gatsby-plugin-offline`,
    // highlight-next-line
    `gatsby-plugin-react-helmet`,
  ],
}
```

3. Bên trong thư mục `src/components`, tạo một tệp tin mới tên `seo.js` và thêm những dòng sau:

```jsx:title=src/components/seo.js
import React from "react"
import PropTypes from "prop-types"
import Helmet from "react-helmet"
import { useStaticQuery, graphql } from "gatsby"

function SEO({ description, lang, meta, title }) {
  const { site } = useStaticQuery(
    graphql`
      query {
        site {
          siteMetadata {
            title
            description
            author
          }
        }
      }
    `
  )

  const metaDescription = description || site.siteMetadata.description

  return (
    <Helmet
      htmlAttributes={{
        lang,
      }}
      title={title}
      titleTemplate={`%s | ${site.siteMetadata.title}`}
      meta={[
        {
          name: `description`,
          content: metaDescription,
        },
        {
          property: `og:title`,
          content: title,
        },
        {
          property: `og:description`,
          content: metaDescription,
        },
        {
          property: `og:type`,
          content: `website`,
        },
        {
          name: `twitter:card`,
          content: `summary`,
        },
        {
          name: `twitter:creator`,
          content: site.siteMetadata.author,
        },
        {
          name: `twitter:title`,
          content: title,
        },
        {
          name: `twitter:description`,
          content: metaDescription,
        },
      ].concat(meta)}
    />
  )
}

SEO.defaultProps = {
  lang: `en`,
  meta: [],
  description: ``,
}

SEO.propTypes = {
  description: PropTypes.string,
  lang: PropTypes.string,
  meta: PropTypes.arrayOf(PropTypes.object),
  title: PropTypes.string.isRequired,
}

export default SEO
```

Dòng code trên thiết lập mặc định cho các thẻ siêu dữ liệu (metadata tags) phổ biên nhất và cung cấp cho bạn một component `<SEO>` để làm việc cùng xuyên suốt dự án. Rất tiện dụng, phải không?

4.  Ngay bây giờ, bạn có thể dùng component `<SEO>` trong các bố cục mẫu và trang web và chuyển các đặc tính qua cho nó. Ví dụ, bạn thêm nó vào bố cục mẫu `blog-post.js` của bạn như sau:

```jsx:title=src/templates/blog-post.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"
// highlight-next-line
import SEO from "../components/seo"

export default ({ data }) => {
  const post = data.markdownRemark
  return (
    <Layout>
      // highlight-start
      <SEO title={post.frontmatter.title} description={post.excerpt} />
      // highlight-end
      <div>
        <h1>{post.frontmatter.title}</h1>
        <div dangerouslySetInnerHTML={{ __html: post.html }} />
      </div>
    </Layout>
  )
}

export const query = graphql`
  query($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
      }
      // highlight-next-line
      excerpt
    }
  }
`
```

Ví dụ trên dựa vào [Blog về Gatsby cho lính mới](/starters/gatsbyjs/gatsby-starter-blog/). Bằng cách chuyển các đặc tính sang cho component `<SEO>`, bạn có thể thay đổi siêu dữ liệu của một bài đăng một cách linh động. Trong trường hợp này, `title` và `excerpt` của bài đăng (nếu nó có tồn tại trong tập tin markdown của bài) sẽ được dung thay cho đặc tính mặc định là `siteMetadata` trong tập tin `gatsby-config.js`.

Ngay bây giờ, nếu bạn chạy kiểm toán Lighthouse một lần nữa như đã được hướng dẫn trước đó, bạn sẽ gần như đạt được--thậm chí có thể đạt được cả-- 100 điểm!

> 💡 Để tìm thêm thông tin và các ví dụ, tham khảo [Thêm một component SEO](/docs/add-seo-component/) và [Tài liệu về Mũ bảo hiểm React](https://github.com/nfl/react-helmet#example)!

## Không ngừng tiến bộ

Trong chương này, chúng tôi đã cho bạn biết qua một vài công cụ chuyên dụng cho Gatsby để giúp cải thiện điểm số hiệu suất của website của bạn và săn sàng để phát trực tiếp.

Lighthouse là một công cụ tuyệt vời cho các cải tiến website và để học hỏi -- Tiếp tục xem qua các đóng góp tỉ mỉ nó cung cấp và không ngừng cải thiện website!

## Những bước tiếp theo

### Tài liệu chính thức

- [Bộ tài liệu chính thức](https://www.gatsbyjs.org/docs/): Xem tài liệu chính thức cho _[Làm quen](https://www.gatsbyjs.org/docs/quick-start/)_, _[Hướng dẫn chi tiết](https://www.gatsbyjs.org/docs/preparing-your-environment/)_, _[API tham khảo](https://www.gatsbyjs.org/docs/gatsby-link/)_, và nhiều hơn thế nữa.

### Những Plugin chính thức

- [Những Plugin chính thức](https://github.com/gatsbyjs/gatsby/tree/master/packages): Danh sách đầy đủ mọi Plugin chính thức được bảo trì bởi Gatsby.

### Tài liệu chính thức cho người mới học

1.  [Tài liệu Gatsby mặc định cho người mới học](https://github.com/gatsbyjs/gatsby-starter-default): Bắt tay ngay vào dự án của bạn với bố cục mẫu này. Bộ sườn này đã bao gồm các tập tin tinh chỉnh Gatsby cần thiết cho bạn. _[ví dụ thực tế](http://gatsbyjs.github.io/gatsby-starter-default/)_
2.  [Blog Gatsby cho người mới](https://github.com/gatsbyjs/gatsby-starter-blog): Bộ hướng dẫn tạo một blog tuyệt vời ông mặt trời và nhanh chớp nhoáng bằng Gatsby. _[ví dụ thực tế](http://gatsbyjs.github.io/gatsby-starter-blog/)_
3.  [Gatsby Hello-World cho người mới](https://github.com/gatsbyjs/gatsby-starter-hello-world): Bộ Gatsby cho người mới nhưng đã được tối giản vừa đủ để xây một trang web Gatsby. _[ví dụ thực tế](https://gatsby-starter-hello-world-demo.netlify.com/)_

## Chỉ vậy thôi, các bằng hữu

Thật ra, cũng không hẳn là vậy; chỉ vậy cho chương hướng dẫn thôi. Vẫn còn [Phụ lục](/tutorial/additional-tutorials/) để đọc thêm hướng dẫn cho các trường hợp cụ thể.

Đây chỉ là khởi đầu. Tiến lên!

- Bạn vừa tạo được một cái gì đó thú vị? Chia sẻ ngay trên Twitter, gắn thẻ [#buildwithgatsby](https://twitter.com/search?q=%23buildwithgatsby), và [@cho chúng tôi biết](https://twitter.com/gatsbyjs)!
- Bạn có một bài đăng về những gì đã học được? Chia sẻ cả điều đó!
- Đóng góp! Dạo quanh [bàn luận các sự cố](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22) trên repo của gatsby và [trở thành cộng tác](/contributing/how-to-contribute/).

Tham khảo tài liệu["đóng góp như thế nào"](/contributing/how-to-contribute/) để có thêm nhiều ý tưởng.

Chúng tôi không thể đợi xem những thành quả của bạn 😄.
