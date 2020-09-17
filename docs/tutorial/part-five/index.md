---
title: Source Plugins
typora-copy-images-to: ./
disableTableOfContents: true
---

> Bài hướng dẫn này là một phần trong chuỗi bài về lớp dữ liệu của Gatsby. Hãy bảo đảm rằng bạn đã thông qua [phần 4](/tutorial/part-four/) trước khi tiếp tục ở đây.

## Bài hướng dẫn này có những gì?

Trong mục hướng dẫn này, bạn sẽ học về cách kéo dữ liệu vào trong trang web Gatsby của bạn sử dụng GraphQL và các source plugin. Tuy nhiên, trước khi bạn học về những plugin này, bạn sẽ muốn biết về cách sử dụng một thứ gọi là GraphiQL, một công cụ hỗ trợ bạn cấu trúc nên những câu truy vấn của bạn một cách đúng đắn.

## Giới thiệu GraphiQL

GraphiQL là môi trường phát triển tích hợp (IDE) cho GraphQL. Nó là một công cụ mạnh mẽ (và hoàn toàn tuyệt vời) mà bạn sẽ sử dụng thường xuyên khi xây dựng những trang web Gatsby.

<<<<<<< HEAD
Bạn có thể truy cập nó khi máy chủ phát triển của trang web của bạn đang vận hành—mặc định tại
<http://localhost:8000/___graphql>.
=======
You can access it when your site's development server is running—normally at
`http://localhost:8000/___graphql`.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="/graphiql-explore.mp4"></source>
  <p>Trình duyệt của bạn không hỗ trợ phần tử video này.</p>
</video>

Hãy khám phá xung quanh về "kiểu" `Site` được tích hợp sẵn và xem những trường nào có sẵn trong nó -- bao gồm đối tượng `siteMetadata` mà bạn đã truy vấn trước đây. Hãy thử mở GraphiQL và thử nghiệm với dữ liệu của bạn! Nhấn <kbd>Ctrl + Space</kbd> (hay sử dụng <kbd>Shift + Space</kbd> như là một tổ hợp phím tắt thay thế) để hiển thị cửa sổ tự động hoành thành và <kbd>Ctrl + Enter</kbd> để chạy câu truy vấn GraphQL. Bạn sẽ sử dụng GraphiQL nhiều hơn trong phần còn lại của loạt bài hướng dẫn.

## Sử dụng GraphiQL Explorer

GraphiQL Explorer cho phép bạn xây dựng những truy vần hoàn thiện một cách tương tác bằng việc click qua những trường có sẵn và dữ liệu đầu vào mà không phải thông qua việc lặp đi lặp lại quá trình gõ những lệnh truy vấn này.

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-build-a-graphql-query-using-gatsby-s-graphiql-explorer"
  lessonTitle="Build a GraphQL Query using Gatsby’s GraphiQL Explorer"
/>

## Các source plugin

Dữ liệu trong những trang web Gatsby có thể đến từ bất kì nơi nào: APIs, cơ sở dữ liệu (databases), CMSs, những tập tin tại chỗ, vâng vâng.

Những source plugin lấy dữ liệu từ nguồn của chúng. Ví dụ, source plugin filesystem biết làm cách nào để lấy dữ liệu từ hệ thống tập tin. Plugin WordPress biết làm cách nào để lấy dữ liệu từ WordPress API.

Hãy thêm [`gatsby-source-filesystem`](/packages/gatsby-source-filesystem/) vào và khám phá cách hoạt động của nó.

Đầu tiên, cài đặt plugin tại thư mục gốc của dự án:

```shell
npm install --save gatsby-source-filesystem
```

Sau đó thêm vào tập tin `gatsby-config.js` của bạn:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
  },
  plugins: [
    // highlight-start
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
    // highlight-end
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

Lưu và khởi động lại máy chủ phát triển gatsby. Sau đó mở GraphQL một lần nữa.

Trong khung Explorer, bạn sẽ thấy `allFile` và `file` là những lựa chọn sẵn có:

![graphiql-filesystem](graphiql-filesystem.png)

Click thanh thả xuống `allFile`. Đặt con trỏ của bạn phía sau `allFile` trong khu vực của lệnh truy vấn, và sau đó nhấn <kbd>Ctrl + Enter</kbd>. Việc làm này sẽ giúp điền trước một lệnh truy vấn cho `id` của từng tập tin. Bấm "Play" để chạy lệnh truy vấn:

![filesystem-query](filesystem-query.png)

Trong khung Explorer, trường `id` đã được tự động chọn. Lựa chọn thêm nhiều trường bằng việc đánh dấu hộp kiểm tương ứng với trường đó. Bấm "Play" để chạy lệnh truy vấn lần nữa, với những trường mới:

![filesystem-explorer-options](filesystem-explorer-options.png)

Bằng một cách khác, bạn có thể thêm các trường vào bằng phím tắt tự động hoàn thành (<kbd>Ctrl + Space</kbd>). Việc này hiển thị những trường có thể truy vấn được trên những node `File`.

![filesystem-autocomplete](filesystem-autocomplete.png)

<<<<<<< HEAD
Thử thêm một số trường vào lệnh truy vấn của bạn, nhấn tổ hợp <kbd>Ctrl + Enter</kbd>
mỗi khi muốn chạy lại lệnh truy vấn. Bạn sẽ được thấy kết quả của lệnh truy vấn đã được cập nhật:
=======
Try adding a number of fields to your query, press <kbd>Ctrl + Enter</kbd>
each time to re-run the query. You'll see the updated query results:
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

![allfile-qeury](allfile-query.png)

Kết quả là một mảng những `File` "node" (node là một tên gọi hoa mỹ dành cho một đối tượng trong một
"graph"). Mỗi đối tượng `File` node có những trường mà bạn đã truy vấn.

## Xây dưng một trang với một lệnh truy vấn GraphQL

Xây dựng những trang mới với Gatsby thường bắt đầu với GraphiQL. Đầu tiên bạn phác họa ra
lệnh truy vấn dữ liệu bằng việc thử nghiệm trong GraphiQL sau đó sao chép thông tin này vào vào một component trang React
để bắt đầu xây dựng UI.

Hãy cùng thử làm việc này nào.

Tạo một tập tin mới tại `src/pages/my-files.js` với lệnh truy vấn GraphQL `allFile` mà bạn vừa
tạo:

```jsx:title=src/pages/my-files.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default ({ data }) => {
  console.log(data) // highlight-line
  return (
    <Layout>
      <div>Hello world</div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```

Dòng lệnh `console.log(data)` được làm nổi bật ở trên. Nó thường có ích khi
tạo một component mới để in ra dữ liệu bạn đang nhận được từ câu truy vấn GraphQL
để bạn có thể mày mò dữ liệu trong bàng điều khiển trình duyệt trong khi đang xây dựng UI.

Nếu bạn dẫn đến trang mới tại `/my-files/` và mở bảng điều khiển trình duyệt
bạn sẽ thấy đại loại như sau:

![data-in-console](data-in-console.png)

Cấu trúc của dữ liệu giống với cấu trúc của lệnh truy vấn GraphQL.

Thêm một vài dòng code vào component của bạn để in ra dữ liệu của File.

```jsx:title=src/pages/my-files.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default ({ data }) => {
  console.log(data)
  return (
    <Layout>
      {/* highlight-start */}
      <div>
        <h1>My Site's Files</h1>
        <table>
          <thead>
            <tr>
              <th>relativePath</th>
              <th>prettySize</th>
              <th>extension</th>
              <th>birthTime</th>
            </tr>
          </thead>
          <tbody>
            {data.allFile.edges.map(({ node }, index) => (
              <tr key={index}>
                <td>{node.relativePath}</td>
                <td>{node.prettySize}</td>
                <td>{node.extension}</td>
                <td>{node.birthTime}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
      {/* highlight-end */}
    </Layout>
  )
}

export const query = graphql`
  query {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```

<<<<<<< HEAD
Và bây giờ dẫn tới [http://localhost:8000/my-files](http://localhost:8000/my-files)… 😲
=======
And now visit `http://localhost:8000/my-files`… 😲
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

![my-files-page](my-files-page.png)

## Tiếp theo là gì?

Hiện tại bạn đã được học cách thức những source plugin mang dữ liệu _vào_ hệ thống dữ liệu của Gatsby. Trong hướng dẫn tiếp theo, bạn sẽ được học cách thức những transformer plugin _biến đổi_ nội dung thô được truyển tải bởi các source plugin. Sự kết hợp giữa các source plugin và các transformer plugin có thể xử lý mọi sự cung ứng dữ liệu và chuyển đội dữ liệu mà bạn cần khi xây dựng một trang web Gatsby. Tìm hiểu về những transformer plugin tại [phần 6 của hướng dẫn](/tutorial/part-six/).
