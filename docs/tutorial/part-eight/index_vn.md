---
tiêu đề: Preparing a Site to Go Live
typora-copy-images-to: ./
disableTableOfContents: true
---

Wow! Bạn đã vượt qua cả một chặng đường dài ! Hãy cùng nhìn lại những gì bạn học được:

- tạo một website bằng Gatsby
- xây dựng trang và hợp phần
- trang trí các hợp phần
- thêm plugins cho trang web
- nguồn & biến đổi dữ liệu
- dùng GraphQL để lấy dữ liệu cho trang
- tạo trang từ dữ liệu của bạn bằng phương pháp lập trình

Trong phần cuối này, bạn sẽ được học qua một số bước thông dụng để chuẩn bị phát sóng một website. Hãy làm quen với [Lighthouse](https://developers.google.com/web/tools/lighthouse/) - một công cụ chẩn đoán website vô cùng hữu ích! Bên cạnh đó, chung tôi cũng sẽ cho bạn tiếp xúc với một vài plugins phổ biến mà bạn sẽ cần khi xây dựng các website Gatsby.

## Kiểm toán với Lighthouse

Trích từ [Lighthouse website](https://developers.google.com/web/tools/lighthouse/):

> Lighthouse là một mã nguồn mở, một công cụ tự động giúp nâng cao chất lượng các trang web. Bạn có thể dùng nó trên bất kì trang web nào, bất kể công khai hay cần xác thực. Nó có kiểm toán cho hiệu suất, hỗ trợ tiếp cận, ứng dụng web nâng cao (progressive web apps - PWAs), và hơn thế nữa.

Lighthouse đã được tích hợp trong công cụ cho nhà phát triển Chrome (Chrome DevTools). Chạy công cụ kiểm toán -- và rồi xem qua các lỗi nó tìm được và thay đổi theo các nâng cấp được gợi ý -- là phương pháp tối ưu để chuẩn bị cho website của bạn trước khi phát sóng. Nó giúp bạn tự tin có một website nhanh nhất và dễ tiếp cận nhất có thể.

Thử ngay đi nào!

Đầu tiên, bạn cần lập một phiên bản hoàn thiện cho trang Gatsby của bạn. Máy chủ thử nghiệm Gatsby được phát triển phù hợp cho việc triển khai nhanh. Tuy nhiên, website mà nó tạo ra, dù rất giống với các trang xây theo phiên bản thương mại, không tối ưu như bạn nghĩ.

### ✋ Tạo production build (phiên bản hoàn thiện)

1.  Dừng máy chủ thử nghiệm (trong trường hợp nó đang chạy) và chạy câu lệnh sau:

```shell
gatsby build
```

> 💡 Như bạn đã học trong [phần 1](/tutorial/part-one/), câu lệnh này xây một production build cho website của bạn và xuất các file tĩnh hoàn thiện vào trong thư mục `public`.

2.  Để xem production build của website trên máy tính cục bộ, chạy lệnh:

```shell
gatsby serve
```

Khi câu lệnh này chạy, bạn có thể xem website của bạn trực tiếp tại [`localhost:9000`](http://localhost:9000).

### Dùng công cụ kiểm toán Lighthouse

Tới đây bạn sẽ chạy thử Lighthouse lần đầu. 

1. Nếu chưa thực hiện, bạn hãy mở website bằng Chrome ẩn danh để không có bất kì tiện ích mở rộng nào làm gián đoạn quá trình kiểm toán. Sau đó, hãy mở công cụ cho nhà phát triển Chrome.

2.  Ấn vào tab "Audits"<!-- DevTools không có phiên bản Tiếng Việt -->, bạn sẽ thấy trên màn hình như sau:

![Bắt đầu kiểm toán với Lighthouse](./lighthouse-audit.png)

3.  Chọn "Perform an audit..." (Mặc định là tất cả các dạng kiểm toán sẽ được chọn). Sau đó chọn "Run audit". (Sẽ mất tầm một phút để hoàn thành bài kiểm toán). Một khi kiểm toán xong, bạn sẽ thấy kết quả hiện trên màn hình như sau:

![Kết quả kiểm toán từ Lighthouse](./lighthouse-audit-results.png)

Như bạn đã thấy, hiệu suất của Gatsby vô cùng đột phá, nhưng bạn vẫn chưa vận dụng được ứng dụng nâng cao (PWA), hỗ trợ tiếp cận, thông lệ phổ biến, và tối ưu hóa công cụ tìm kiếm (Search Engine Optimization - SEO) để cải thiện điểm số kiểm toán (đồng thời giúp website của bạn thân thiện hơn với người dùng và các công cụ tìm kiếm).

## Thêm tập tin kê khai (manifest file)

Có vẻ như điểm của bạn tụt hậu trong mục "Progressive Web App". Cùng giải quyết điều đó nào.

Nhưng trước hết, PWAs thật sự _là gì_?

Đó chỉ là những website thông thường nhưng tận dụng được chức năng tiên tiến của trình duyệt nhằm tăng cường trải nghiệm web thông qua những đặc tính và ưu điểm như của một ứng dụng. Tham khảo [Tổng quan của Google](https://developers.google.com/web/progressive-web-apps/) về định nghĩa của một trải nghiệm PWA.

Sự bao gồm của bản kê khai ứng dụng web (web app manifest) là một trong ba [yêu cầu cơ bản cho PWA](https://alistapart.com/article/yes-that-web-project-should-be-a-pwa#section1) được chấp nhận rộng rãi.

Trích [Google](https://developers.google.com/web/fundamentals/web-app-manifest/):

> Bản kê khai ứng dụng web chỉ đơn giản là một tập tin JSON dùng để thông báo cho trình duyệt về ứng dụng web và phương thức để 'cài đặt' ứng dụng đó trên điện thoại hay máy tính của người dùng.

[Bản kê khai plugin (manifest plugin) của Gatsby](/packages/gatsby-plugin-manifest/) tinh chỉnh Gatsby để tạo ra tập tin `manifest.webmanifest` trên mỗi trang web được tạo.

### ✋ Sử dụng `gatsby-plugin-manifest`

1.  Cài đặt plugin:

```shell
npm install --save gatsby-plugin-manifest
```

2. Thêm một icon tiêu đề (favicon) cho ứng dụng của bạn trong `src/images/icon.png`. Cho mục đích thực tập bạn có thể dùng [biểu tượng mẫu này](https://raw.githubusercontent.com/gatsbyjs/gatsby/master/docs/tutorial/part-eight/icon.png), nếu bạn không có sẵn. Biểu tượng này cần thiết để lập tất cả các hình ảnh cho kê khai. Để biết thêm thông tin, xem qua tài liệu cho [`gatsby-plugin-manifest`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-manifest/README.md).

3. Thêm plugin vào `plugins` tập hợp trong tập tin `gatsby-config.js`.

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
        // Bật thông báo "Thêm vào màn hình chính" và ngắt UI của trình duyệt (bao gồm cả núi lùi vè) 
        // Xem qua https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // This path is relative to the root of the site.
      },
    },
  ]
}
```

Đó là tất cả những gì bạn cần để bắt đầu thêm một bản kê khai web vào một website Gatsby. Ví dụ ở trên gợi nhắc một thiết lập cơ bản -- Truy cập [tài liệu tham khảo về plugin](/packages/gatsby-plugin-manifest/?=gatsby-plugin-manifest#automatic-mode) để tìm thêm lựa chọn.

## Thêm hỗ trợ ngoại tuyến

Một yêu cầu khác để website được công nhận là một PWA chính là vận dụng [máy chủ úy nhiệm (service worker)](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API). Máy chủ ủy nhiệm sẽ chạy nền, quyết định phương thức sử dụng mạng và nội dung cache (cached content) dựa trên hiện trạng kết nối, cho một trải nghiệm ngoại tuyết không gián đoạn và trong kiểm soát.

[Plugin Gatsby ngoại tuyến](/packages/gatsby-plugin-offline/) giúp website Gatsby có thể hoạt động ngoại tuyến và trở nên trơn tru hơn khi gặp kết nối kém bằng cách tạo một máy chủ ủy nhiệm cho trang web của bạn.

### ✋ Sử dụng `gatsby-plugin-offline`

1.  Cài đặt plugin:

```shell
npm install --save gatsby-plugin-offline
```

2.  Thêm plugin vào `plugins` tập hợp trong tập tin `gatsby-config.js`.

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
        // Bật thông báo "Thêm vào màn hình chính" và ngắt UI của trình duyệt (bao gồm cả núi lùi vè) 
        // Xem qua https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // This path is relative to the root of the site.
      },
    },
    // Tô màu dòng kế tiếp
    `gatsby-plugin-offline`,
  ]
}
```

Đó là tất cả những gì bạn cần biết để thiết lập một máy chủ úy nhiệm trên Gatsby.

> 💡 Tiện ích ngoại tuyến này nên được liệt kê _sau_ plugin kê khai (manifest plugin) để nó có thể cache `manifest.webmanifest` được tạo ra.

## Thêm siêu dữ liệu (metadata) của trang

Thêm siêu dữ liệu vào trang (ví dụ như tiêu đề hoặc miêu tả) là chìa khóa giúp cho các công cụ tìm kiếm như Google hiểu được nội dung của bạn và quyết định khi nào nó sẽ trồi lên trong kết quả tìm kiếm.

[Mũ bảo hiểm React (React Helmet)](https://github.com/nfl/react-helmet) là một gói cung cấp giao diện hợp phần React (React component interface) giúp bạn quản lý [tựa đề trang](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head).

[Plugin mũ bảo hiểm react (react helmet plugin)](/packages/gatsby-plugin-react-helmet/) của Gatsby cung cấp hỗ trợ nhanh cho dữ liệu kết xuất đồ họa máy chủ (server rendering data) cùng với Mũ bảo hiểm React. Thông qua plugin này, những thuộc tính bạn thêm vào Mũ bảo hiểm React cũng sẽ được thêm vào các trang HTML tĩnh được xây bằng Gatsby.

### ✋ Sử dụng `React Helmet` và `gatsby-plugin-react-helmet`

1.  Cài đặt cả hai gói:

```shell
npm install --save gatsby-plugin-react-helmet react-helmet
```

2.  Hãy chắc chắn rằng bạn đã có  `miêu tả` và một `tác giả` được thiết lập bên trong vật thể `siteMetadata` của bạn. Đồng thời, thêm plugin `gatsby-plugin-react-helmet` vào trong tập hợp `plugins` trong tệp tin của bạn `gatsby-config.js`.

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
    // Đánh dấu bắt đầu
    description: `A simple description about pandas eating lots...`,
    author: `gatsbyjs`,
    // Đánh dấu kết thúc
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
        // Bật thông báo "Thêm vào màn hình chính" và ngắt UI của trình duyệt (bao gồm cả núi lùi vè) 
        // Xem qua https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // This path is relative to the root of the site.
      },
    },
    `gatsby-plugin-offline`,
    // Tô mày dòng tiếp theo
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

Dòng code trên thiết lập mặc định cho các thẻ siêu dữ liệu (metadata tags) phổ biên nhất và cung cấp cho bạn một hợp phần `<SEO>` để làm việc cùng xuyên suốt dự án. Rất tiện dụng, phải không?

4.  Ngay bây giờ, bạn có thể dùng hợp phần `<SEO>` trong các bố cục mẫu và trang web và chuyền các đặc tính cho nó. Ví dụ, bạn thêm nó vào bố cục mẫu `blog-post.js` của bạn như sau:

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

The above example is based off the [Gatsby Starter Blog](/starters/gatsbyjs/gatsby-starter-blog/). By passing props to the `<SEO>` component, you can dynamically change the metadata for a post. In this case, the blog post `title` and `excerpt` (if it exists in the blog post markdown file) will be used instead of the default `siteMetadata` properties in your `gatsby-config.js` file.

Now, if you run the Lighthouse audit again as laid out above, you should get close to--if not a perfect-- 100 score!

> 💡 For further reading and examples, check out [Adding an SEO Component](/docs/add-seo-component/) and the [React Helmet docs](https://github.com/nfl/react-helmet#example)!

## Keep making it better

In this section, we've shown you a few Gatsby-specific tools to improve your site's performance and prepare to go live.

Lighthouse is a great tool for site improvements and learning -- Continue looking through the detailed feedback it provides and keep making your site better!

## Next Steps

### Official Documentation

- [Official Documentation](https://www.gatsbyjs.org/docs/): View our Official Documentation for _[Quick Start](https://www.gatsbyjs.org/docs/quick-start/)_, _[Detailed Guides](https://www.gatsbyjs.org/docs/preparing-your-environment/)_, _[API References](https://www.gatsbyjs.org/docs/gatsby-link/)_, and much more.

### Official Plugins

- [Official Plugins](https://github.com/gatsbyjs/gatsby/tree/master/packages): The complete list of all the Official Plugins maintained by Gatsby.

### Official Starters

1.  [Gatsby's Default Starter](https://github.com/gatsbyjs/gatsby-starter-default): Kick off your project with this default boilerplate. This barebones starter ships with the main Gatsby configuration files you might need. _[working example](http://gatsbyjs.github.io/gatsby-starter-default/)_
2.  [Gatsby's Blog Starter](https://github.com/gatsbyjs/gatsby-starter-blog): Gatsby starter for creating an awesome and blazing-fast blog. _[working example](http://gatsbyjs.github.io/gatsby-starter-blog/)_
3.  [Gatsby's Hello-World Starter](https://github.com/gatsbyjs/gatsby-starter-hello-world): Gatsby Starter with the bare essentials needed for a Gatsby site. _[working example](https://gatsby-starter-hello-world-demo.netlify.com/)_

## That's all, folks

Well, not quite; just for this tutorial. There are [Additional Tutorials](/tutorial/additional-tutorials/) to check out for more guided use cases.

This is just the beginning. Keep going!

- Did you build something cool? Share it on Twitter, tag [#buildwithgatsby](https://twitter.com/search?q=%23buildwithgatsby), and [@mention us](https://twitter.com/gatsbyjs)!
- Did you write a cool blog post about what you learned? Share that, too!
- Contribute! Take a stroll through [open issues](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22) on the gatsby repo and [become a contributor](/contributing/how-to-contribute/).

Check out the ["how to contribute"](/contributing/how-to-contribute/) docs for even more ideas.

We can't wait to see what you do 😄.
