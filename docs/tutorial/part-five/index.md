---
tiêu đề: Source Plugins
typora-copy-images-to: ./
disableTableOfContents: true
---

> Mục hướng dẫn này nằm trong chuỗi hướng dẫn về lớp dữ liệu của Gatsby. Bạn cần bảo đảm thông qua [phần 4](/tutorial/part-four/) trước khi tiếp tục ở đây.

## Hướng dẫn này sẽ nói về điều gì?

Trong mục hướng dẫn này, bạn sẽ học về phương pháp kéo dữ liệu về trang web Gatsby của bạn sử dụng GraphQL và Source Plugins. Tuy nhiên, trước khi bạn học những plugins này, bạn sẽ muốn biết phương pháp sử dụng GraphiQL, một công cụ dùng để hỗ trợ tạo kết cấu đúng cho những lệnh truy vấn (query) của bạn.

## Giới thiệu GraphiQL

GraphiQL là môi trường phát triển tích hợp (IDE) của GraphQL. Nó là một công cụ mạnh mẽ (và toàn diện) mà bạn sẽ sử dụng thường xuyên khi xây dựng những trang web Gatsby.

Bạn có thể truy cập nó khi máy chủ phát triển của trang web của bạn đang vận hành như bình thường tại 
<http://localhost:8000/___graphql>.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="/graphiql-explore.mp4"></source>
  <p>Your browser does not support the video element.</p>
</video>

Khám phá tìm hiểu về "loại" `Site` được xây dựng sẵn và xem những trường nào có sẵn trong nó -- bao hàm object `siteMetadata` mà bạn đã truy vấn trước đó. Hãy thử mở GraphiQL và thử nghiệm với dữ liệu của bạn! Nhấn <kbd>Ctrl + Space</kbd> (hay sử dụng <kbd>Shift + Space</kbd> như là một tổ hợp phím tắt thay thế) để hiển thị cửa sổ tự động hoành thành và <kbd>Ctrl + Enter</kbd> để chạy lệnh truy vần GraphQL. Bạn sẽ sự dụng GraphiQL nhiều hơn trong phần còn lại của hướng dẫn.

## Sử dụng GraphiQL Explorer

GraphiQL Explorer cho phép bạn xây dựng một cách tương tác những truy vần hoàn thiện bằng việc click những trường có sẵn và dữ liệu đầu vào mà không phải thông qua quá trình gõ lại những lệnh truy vấn này.

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-build-a-graphql-query-using-gatsby-s-graphiql-explorer"
  lessonTitle="Build a GraphQL Query using Gatsby’s GraphiQL Explorer"
/>

## Source plugins

Dữ liệu trong những trang web Gatsby có thể đến từ bất kì nơi nào: APIs, cơ sở dữ liệu (databases), CMSs, những tập tin cục bộ, vâng vâng.

Source plugins tải dữ liệu từ mã nguồn của chúng. Ví dụ, source plugin về hệ thống tập tin biết làm cách nào để tải dữ liệu từ hệ thống tập tin. Plugin về WordPress biết làm cách nào tải dữ liệu từ API của WordPress.

Thêm vào [`gatsby-source-filesystem`](/packages/gatsby-source-filesystem/) và khám phá cách hoạt động của nó.

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

Lưu lại và tái khởi động máy chủ phát triển gatsby. Sau đó mở GraphQL again.

Trong khung Explorer, bạn sẽ thấy `allFile` và `file` sẵn có là những lựa chọn:

![hệ thống tập tin graphiql](graphiql-filesystem.png)

Click thanh thả xuống `allFile`. Định vị con trỏ của bạn phía sau của `allFile` trong khu vực của lệnh truy vấn, và sau đó gõ <kbd>Ctrl + Enter</kbd>. Việc làm này sẽ giúp điền trước một lệnh truy vấn cho `id` của từng tập tin. Nhấn "Play" để chạy lệnh truy vấn:

![hệ thống tập tin-lệnh truy vấn](filesystem-query.png)

Trong khung Explorer, trường `id` đã được tự động chọn. Lựa chọn thêm nhiều trường bằng việc chọn hộp kiểm tương ứng với trường đó. Nhấn "Play" để chạy lệnh truy vấn lần nữa, với những trường mới:

![filesystem-explorer-options](filesystem-explorer-options.png)

Hoặc là, bạn có thể thêm vào các trường bằng phím tắt tự động hoàn thành (<kbd>Ctrl + Space</kbd>). Việc làm này hiển thị những trường có thể truy vấn trên những node của `File`.

![filesystem-autocomplete](filesystem-autocomplete.png)

Thử thêm vào một số trường vào lệnh truy vấn của bạn, nhấn tổ hợp <kbd>Ctrl + Enter</kbd>
mỗi khi muốn chạy lại lệnh truy vấn. Bạn sẽ được thấy kết quả của lệnh truy vấn đã được cập nhật:

![allfile-lệnh truy vấn](allfile-query.png)

Kết quả là một danh sách của `File` "nodes" (node là một tên gọi hoa mỹ dành cho một object trong một
"graph"). Mỗi node object của `File` có những trường mà bạn đã truy vấn.

## Xây dưng một trang web với lệnh truy vấn GraphQL

Xây dựng những trang web mới với Gatsby thường bắt đầu với GraphiQL. Đầu tiên bạn dựng
lệnh truy vấn dữ liệu bằng thử nghiệm trong GraphiQL sau đó sao chép thông tin này vào vào một component trang của React
để bắt đầu xây dựng giao diện người dùng.

Hãy cùng thử việc này nào.

Tạo một tập tin mới tại `src/pages/my-files.js` với lệnh truy vần GraphQL `allFile` và bạn vừa
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
tạo một component mới để hiển thị dữ liêu bạn đang tải từ lệnh truy vấn GraphQL
để bạn có thể mày mò dữ liệu trong bàng điều khiển trình duyệt trong khi đang xây dựng giao diện người dùng.

Nếu bạn dẫn tới một trang web mới tại `/my-files/` và mở bảng điều khiển trình duyệt
bạn sẽ thấy như sau:

![dữ liệu-trong-bàng điều khiển](data-in-console.png)

Cấu trúc của dữ liệu giống như cấu trúc của lệnh truy vấn GraphQL.

Thêm một vài code vào component của bạn để in ra dữ liệu của File.

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

Và bây giờ dẫn tới [http://localhost:8000/my-files](http://localhost:8000/my-files)… 😲

![my-files-page](my-files-page.png)

## Tiếp theo là gì?

Hiện tại bạn đã được học cách thức source plugins mang dữ liệu _vào_ hệ thống dữ liệu của Gatsby. Trong hướng dẫn tiếp theo, bạn sẽ được học cách thức transformer plugins _biến đổi_ nội dung gốc được truyển tải bởi source plugins. Sự kết hợp giữa source plugins and transformer plugins có thể xử lý mọi cung ứng dữ liệu và chuyển đội dữ liệu mà bạn cần khi xây dựng trang web Gatsby. Tìm hiểu về transformer plugins tại [phần 6 của hướng dẫn](/tutorial/part-six/).
