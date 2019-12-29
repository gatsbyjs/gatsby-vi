---
title: Các transformer plugin
typora-copy-images-to: ./
disableTableOfContents: true
---

> Bài hướng dẫn này là một phần trong chuỗi bài về lớp dữ liệu của Gatsby. Hãy đảm bảo rằng bạn đã xem qua [phần 4](/tutorial/part-four/) và [phần 5](/tutorial/part-five/) trước khi tiếp tục tại đây.

## Bài hướng dẫn này có những gì?

Bài hướng dẫn lần trước đã chỉ ra cách các source plugin mang dữ liệu _vào trong_ hệ thống dữ liệu của Gatsby. Trong bài hướng dẫn này, bạn sẽ học cách các transformer plugin _chuyển đổi_ các nội dung thô được mang bởi các source plugin. Sự kết hợp giữa các source plugin và các transformer plugin có thể xử lý tất cả các nguồn dữ liệu và chuyển đổi dữ liệu mà bạn có thể cần khi xây dựng một trang web Gatsby.

## Các transformer plugin

Thông thường, định dạng của dữ liệu mà bạn lấy từ các source plugin không phải là cái bạn muốn 
sử dụng để xây dựng website. Source plugin hệ thống tập tin cho phép bạn truy vấn dữ liệu 
_về_ các tập tin nhưng nếu bạn muốn truy vấn dữ liệu _bên trong_ các tập tin thì sao?

Để thực hiện điều này, Gatsby hỗ trợ các transformer plugin lấy
nội dung thô từ các source plugin và _chuyển đổi_ nó thành một cái gì đó có thể sử dụng nhiều hơn.

Ví dụ, các tập tin markdown. Markdown dễ viết nhưng khi bạn xây dựng một 
trang với nó, bạn cần markdown trở thành HTML.

Hãy thêm một tập tin markdown vào site của bạn tại
`src/pages/sweet-pandas-eating-sweets.md` (Đây sẽ là markdown đầu tiên của bạn ở dạng
bài viết trên blog) và tìm hiểu cách _chuyển đổi_ nó sang HTML bằng cách sử dụng các transformer plugin và
GraphQL.

```markdown:title=src/pages/sweet-pandas-eating-sweets.md
---
title: "Sweet Pandas Eating Sweets"
date: "2017-08-10"
---

Pandas are really sweet.

Here's a video of a panda eating sweets.

<iframe width="560" height="315" src="https://www.youtube.com/embed/4n0xNbfJLR8" frameborder="0" allowfullscreen></iframe>
```

Sau khi bạn lưu tập tin, nhìn `/my-files/` một lần nữa—tập tin markdown mới đầu tiên ở trong
bảng. Đây là một tính năng rất mạnh mẽ của Gatsby. Tương tự như ví dụ
`siteMetadata` trước đó, các source plugin có thể tải lại dữ liệu trực tiếp.
`gatsby-source-filesystem` luôn quét tìm các tập tin mới được thêm vào và 
nếu có, chạy lại các truy vấn của bạn. 

Hãy thêm vào một transformer plugin có thể chuyển đổi các tập tin markdown:

```shell
npm install --save gatsby-transformer-remark
```

Sau đó thêm nó vào `gatsby-config.js` như thông thường:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
  },
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
    `gatsby-transformer-remark`, // highlight-line
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

Khởi động lại máy chủ phát triển sau đó làm mới (hoặc mở lại) GraphiQL và quan sát 
chế độ tự động hoàn thành:

![markdown-autocomplete](markdown-autocomplete.png)

Chọn `allMarkdownRemark` một lần nữa và chạy tương tự như đã làm cho `allFile`. Bạn sẽ
thấy tại đó tập tin markdown mà bạn vừa mới thêm vào. Tìm hiểu các field 
có sẵn trên `MarkdownRemark` node.

![markdown-query](markdown-query.png)

Ok! Hy vọng một số điểm cơ bản đang bắt đầu vào đúng vị trí. Các source plugin mang
dữ liệu _vào trong_ hệ thống dữ liệu của Gatsby và các transformer plugin _chuyển đổi_ các nội dung thô 
được mang bởi các source plugin. Quá trình này có thể xử lý tất cả các nguồn dữ liệu và 
chuyển đổi dữ liệu mà bạn có thể cần khi xây dựng một trang web Gatsby.

## Tạo một danh sách các tập tin markdown của site trong `src/pages/index.js`

Bây giờ bạn sẽ phải tạo một danh sách các tập tin markdown của bạn trên trang đầu. Giống như nhiều 
blog khác, bạn muốn kết thúc với một danh sách các liên kết trên trang đầu chỉ đến từng
bài viết trên blog. Với GraphQL, bạn có thể _truy vấn_ cho danh sách hiện tại các bài viết dưới dạng markdown trên blog 
vì vậy bạn sẽ không cần phải duy trì danh sách theo cách thủ công.

Như là với trang `src/pages/my-files.js`, thay thế `src/pages/index.js` với 
đoạn sau để thêm một truy vấn GraphQL với một số HTML và định dạng ban đầu.

```jsx:title=src/pages/index.js
import React from "react"
import { graphql } from "gatsby"
import { css } from "@emotion/core"
import { rhythm } from "../utils/typography"
import Layout from "../components/layout"

export default ({ data }) => {
  console.log(data)
  return (
    <Layout>
      <div>
        <h1
          css={css`
            display: inline-block;
            border-bottom: 1px solid;
          `}
        >
          Amazing Pandas Eating Things
        </h1>
        <h4>{data.allMarkdownRemark.totalCount} Posts</h4>
        {data.allMarkdownRemark.edges.map(({ node }) => (
          <div key={node.id}>
            <h3
              css={css`
                margin-bottom: ${rhythm(1 / 4)};
              `}
            >
              {node.frontmatter.title}{" "}
              <span
                css={css`
                  color: #bbb;
                `}
              >
                — {node.frontmatter.date}
              </span>
            </h3>
            <p>{node.excerpt}</p>
          </div>
        ))}
      </div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allMarkdownRemark {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          excerpt
        }
      }
    }
  }
`
```

Bây giờ frontpage sẽ trông như thế này:

![frontpage](frontpage.png)

Nhưng một bài viết trên blog của bạn trông có vẻ hơi đơn điệu. Vì vậy, hãy thêm một cái khác tại
`src/pages/pandas-and-bananas.md`

```markdown:title=src/pages/pandas-and-bananas.md
---
title: "Pandas and Bananas"
date: "2017-08-21"
---

Do Pandas eat bananas? Check out this short video that shows that yes! pandas do
seem to really enjoy bananas!

<iframe width="560" height="315" src="https://www.youtube.com/embed/4SZl1r2O_bY" frameborder="0" allowfullscreen></iframe>
```

![two-posts](two-posts.png)

Trông ổn đấy! Ngoại trừ... thứ tự của bài viết là sai.

Nhưng điều này có thể sửa dễ dàng. Khi truy vấn một kết nối của một vài dạng, bạn có thể truyền 
nhiều đối số (argument) tới truy vấn GraphQL. Bạn có thể `sắp xếp` và `lọc` các node, thiết lập 
có bao nhiêu node để `bỏ qua`, và chọn `giới hạn` có bao nhiêu node để gọi. Với 
bộ toán tử (operator) mạnh mẽ này, bạn có thể chọn bất kỳ dữ liệu nào bạn muốn-trong định dạng bạn 
cần.

Trong trang index của truy vấn GraphQL, thay đổi `allMarkdownRemark` thành
`allMarkdownRemark(sort: { fields: [frontmatter___date], order: DESC })`. _Chú ý: Có 3 dấu gạch dưới giữa `frontmatter` và `date`._ Lưu lại
và thứ tự sắp xếp đã được sửa.

Hãy mở GraphiQL và thử qua các tùy chọn sắp xếp khác nhau . Bạn có thể sắp xếp 
kết nối `allFile` cùng với các kết nối khác.

Để biết thêm tài liệu về các toán tử truy vấn (query operator) của chúng tôi, hãy khám phá  [Hướng dẫn tham khảo GraphQL.](/docs/graphql-reference/)

## Thử thách

Hãy thử tạo một trang mới có chứa một bài viết trên blog và xem điều gì xảy ra với danh sách các bài viết trên blog ở trang chủ!

## Tiếp theo là gì?

Thật là tuyệt! Bạn vừa tạo một trang index nơi bạn sẽ truy vấn các
tập tin markdown và tạo một danh sách các tiêu đề bài viết trên blog và các đoạn trích. Nhưng bạn không muốn chỉ thấy các đoạn trích, bạn muốn các trang thực sự cho các tập tin markdown của mình.

Bạn có thể tiếp tục tạo các trang bằng cách đặt các React component trong `src/pages`. Tuy nhiên, bạn sẽ
tìm hiểu tiếp sau đây cách tạo các trang _bằng cách lập trình_ từ _dữ liệu_. Gatsby _không_ 
bị giới hạn để tạo các trang từ các tập tin như nhiều trình tạo trang tĩnh. Gatsby cho phép
bạn sử dụng GraphQL để truy vấn _dữ liệu_ của bạn và ánh xạ (map) các kết quả truy vấn tới các _trang_ ngay tại 
thời điểm xây dựng. Đây là một ý tưởng thực sự mạnh mẽ. Bạn sẽ khám phá ý nghĩa của nó và
cách sử dụng nó trong hướng dẫn tiếp theo, trong đó bạn sẽ học cách [tạo các trang từ dữ liệu bằng cách lập trình](/tutorial/part-seven/).
