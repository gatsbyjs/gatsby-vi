---
title: Làm quen với các thành phần trong Gatsby
typora-copy-images-to: ./
disableTableOfContents: true
---

Trong [**phần trước**](/tutorial/part-zero/), bạn đã chuẩn bị môi trường phát triển cục bộ bằng cách cài đặt những phầm mềm cần thiết và tạo trang Gatsby đầu tiên sử dụng [**mẫu khởi động “hello world”**](https://github.com/gatsbyjs/gatsby-starter-hello-world). Bây giờ, hãy đi sâu hơn nữa vào phần code được tạo bởi mẫu khởi động đó.

## Sử dụng bộ khởi động Gatsby

Trong [**bài hướng dẫn phần 0**](/tutorial/part-zero/), bạn đã tạo một trang mới dựa trên mẫu khởi động "hello world" sử dụng những lệnh sau:

```shell
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

Khi tạo một trang Gatsby mới, bạn cần sử dụng những cấu trục lệnh sau để tạo một trang mới dựa trên bất kì mẫu khởi động Gatsby hiện có:

```shell
gatsby new [SITE_DIRECTORY_NAME] [URL_OF_STARTER_GITHUB_REPO]
```

Nếu bạn bỏ qua phần URL ở cuối, Gatsby sẽ tự động tạo một trang cho bạn dựa vào [**bản mẫu mặc định**](https://github.com/gatsbyjs/gatsby-starter-default). Đối với phần này của bài hướng dẫn, hãy gắn bó với mẫu "Hello World" mà bạn đã tạo trong bài hướng dẫn phần 0. Bạn có thể học thêm về [modifying starters](/docs/modifying-a-starter) trong tài liệu.

### ✋ Mở code

Trong trình soạn thảo code của bạn, mở phần code được tạo bới trang "Hello World" và xem các thư mục và tệp khác nhau trong thư mục "hello-world". Nó sẽ trông như thế này:

![dự án Hello World trong VS Code](01-hello-world-vscode.png)

_Lưu ý: Một lần nữa, Again, trình soạn thảo hiển thị ở đây là Visual Studio Code. Nếu bạn sử dụng một trình soạn thảo khác, nó sẽ trông hơi khác._

Hãy cùng xem phần code tạo nên trang chủ.

> 💡 Nếu như bạn đã dừng máy chủ phát triển sau khi chạy lệnh `gatsby develop` in the previous section, hãy khởi động nó lại bây giờ, đã đến lúc để thực hiện một số thay đổi cho trang hello-world!

## Làm quen với các trang Gatsby

Mở thư mục `/src` trong trình soạn thảo code của bạn. Bên trong là một thư mục duy nhất: `/pages`.

Mở tệp tại `src/pages/index.js`.Phần code trong tệp này tạo ra một thành phần chứa một div và vài văn bản - thích hợp, “Hello world!”

### ✋ Thay đổi trang chủ của "Hello World"

1.  Thay đổi văn bản "Hello World!" thành "Hello Gatsby!" và lưu tệp. Nếu các cửa sổ của bạn nằm cạnh nhau, bạn có thể thấy các thay đổi về code và nội dung được phản ánh gần như ngay lập tức trong trình duyệt sau khi bạn lưu tệp.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="./02-demo-hot-reloading.mp4"></source>
  <p>Xin lỗi! Trình duyệt của bạn không hỗ trợ video này.</p>
</video>

> 💡 Gatsby sử dụng **hot reloading** để tăng tốc quá trình phát triển của bạn. Về cơ bản, khi bạn đang chạy máy chủ (server) phát triển Gatsbyto, các tệp của trang Gatsby được xem ở background - bất cứ khi nào bạn lưu tệp, các thay đổi của bạn sẽ lập tức được phản ánh trong trình duyệt. Bạn không cần phải làm mới trang hoặc khởi động lại máy chủ phát triển - các thay đổi của bạn mới xuất hiện.

2.  Bây giờ bạn có thể làm những thay đổi của bạn rõ hơn một chút. Hãy thử thay thế code trong tệp `src/pages/index.js` với code bên dưới và lưu lần nữa. Bạn sẽ thấy những thay đổi trong văn bản - màu văn bản sẽ có màu tím và kích thước phông chữ sẽ lớn hơn.

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <div style={{ color: `purple`, fontSize: `72px` }}>Hello Gatsby!</div>
)
```

> 💡 Chúng tôi sẽ giới thiệu nhiều hơn về kiểu (styling) trong Gatsby trong [**phần 2**](/tutorial/part-two/) của bài hướng dẫn.

3.  Xóa kiểu dáng kích thước phông chữ, thay văn bản "Hello Gatsby!" thành tiêu đề cấp một (h1), và thêm một đoạn văn (p) bên dưới tiêu đề.

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  {/* highlight-start */}
  <div style={{ color: `purple` }}>
    <h1>Hello Gatsby!</h1>
    <p>What a world.</p>
  {/* highlight-end */}
  </div>
)
```

![Nhiều thay đổi hơn với hot reloading](03-more-hot-reloading.png)

4.  Thêm một hình ảnh. (Trong trường hợp này, một tấm hình ngẫu nhiên từ Unsplash).

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <div style={{ color: `purple` }}>
    <h1>Hello Gatsby!</h1>
    <p>What a world.</p>
    {/* highlight-next-line */}
    <img src="https://source.unsplash.com/random/400x200" alt="" />
  </div>
)
```

![Thêm hình ảnh](04-add-image.png)

### Đợi đã... HTML trong JavaScript?

_Nếu như bạn quen thuộc với React và JSX, bạn có thể thoải mái bỏ qua phần này._ Nếu như bạn chưa từng làm việc với bộ khung (framework) React trước đây, bạn có thể tự hỏi HTML làm gì trong một hàm JavaScript. Hoặc là tại sao chúng ta nhập khẩu `react` ở dòng đầu nhưng dường như không sử dụng nó ở bất cứ đâu. Phiên bản lai "HTML trong JS" này trên thực tế là một cú pháp mở rộng của JavaScript, đối với React, gọi là JSX. Bạn có thể làm theo bài hướng dẫn này mà không cần kinh nghiệm với React, nhưng nếu bạn tò mò, đây là một đoạn trích ngắn gọn…

Xem xét nội dung ban đầu của tệp `src/pages/index.js`:

```jsx:title=src/pages/index.js
import React from "react"

export default () => <div>Hello world!</div>
```

Trong JavaScript thuần, nó trông như thế này:

```javascript:title=src/pages/index.js
import React from "react"

export default () => React.createElement("div", null, "Hello world!")
```

Bây giờ bạn có thể phát hiện ra việc sử dụng nhập khẩu `'react'`! Nhưng chờ đã, Bạn đang viết JSX, không phải thuần HTML và JavaScript. Làm cách nào mà trình duyệt đọc được? Câu trả lời ngắn ngọn là: Nó không có. các trang Gatsby đi kèm với công cụ đã được thiết lập sẵn để chuyển đổi mã nguồn của bạn thành một cái gì đó mà trình duyệt có thể diễn giải.

## Xây dựng với các thành phần

Trang chủ bạn vừa mới thực hiên chỉnh sửa được tạo ra bằng cách định nghĩa một thành phần trang. Chính xác thì “thành phần” là gì?

Được định nghĩa rộng rãi, một thành phần là một khối hợp nhất (building block) cho trang của bạn;Nó là một đoạn mã khép kín mô tả một phần của UI (giao diện người dùng).

Gatsby được xây dựng trên React. Khi chúng ta nói về việc sử dụng và định nghĩa **thành phần**, chúng ta thực sự đang nói về **Các thành phần React** — đoạn mã khép kín (thường được viết bằng JSX) có thể chấp nhận đầu vào và trả về các phần tử React mô tả một phần của UI.

Một trong những thay đổi lớn nhất về mặt tinh thần mà bạn thực hiện khi bắt đầu xây dựng với các thành phần (nếu bạn đã là một nhà phát triển) là bây giờ CSS, HTML, và JavaScript của bạn được kết hợp chặt chẽ và thường sống chung trong một tệp.

Mặc dù một thay đổi có vẻ đơn giản, điều này có ý nghĩa sâu sắc đối với với cách bạn nghĩ về xây dựng trang web.

Lấy ví dụ về tạo một nút tùy chỉnh. Trong quá khứ, bạn sẽ tạo một lớp CSS (có lẽ là: `.primary-button`) với các kiểu tùy chỉnh của bạn và sau đó sử dụng bất cứ khi nào bạn muốn áp dụng các kiểu đó. Ví dụ:

```html
<button class="primary-button">Click me</button>
```

Trong thế giới của các thành phần, thay vào đó bạn tạo một thành phần `PrimaryButton` với các kiểu nút của bạn và sử dụng xuyên suốt trang của bạn như:

<!-- prettier-ignore -->
```jsx
<PrimaryButton>Click me</PrimaryButton>
```

Các thành phần trở thành khối xây dựng cơ sở của trang của bạn. Thay vì bị giới hạn trong các khối xây dựng mà trình duyệt cung cấp, ví dụ `<button />`, bạn có thể dễ dàng tạo các khối xây dựng thanh lịch đáp ứng các nhu cầu của các dự án của bạn.

### ✋ Sử dụng các thành phần trang

Bất cứ thành phần React nào được định nghĩa trong `src/pages/*.js` sẽ tự động trở thành một trang. Hãy xem điều này trong hành động.

Bạn đã có một tệp `src/pages/index.js` đi kèm với mẫu khởi động "Hello World". Hãy tạo một trang about.

1.  Tạo một tệp mới tại `src/pages/about.js`, sao chép code sau vào tệp mới, và lưu lạie.

```jsx:title=src/pages/about.js
import React from "react"

export default () => (
  <div style={{ color: `teal` }}>
    <h1> Giới thiệu về Gatsby</h1>
    <p>Such wow. Very React.</p>
  </div>
)
```

2.  Hướng đến http://localhost:8000/about/.

![Trang about mới](05-about-page.png)

Chỉ với đặt một thành phần React vào tệp `src/pages/about.js`, bạn bây giờ có thể truy cập tại `/about`.

### ✋ Sử dụng các thành phần phụ

Hãy nói rằng trang chủ và trang about cả hai đều khá lớn và bạn đã viết lại rất nhiều thứ. Bạn có thể sử dụng các thành phần phụ để chia UI thành các phần có thể tái sử dụng. Cả hai trang của bạn có các tiêu đề `<h1>` - tạo một thành phần mô tả một `Header`.

1.  Tạo một thư mục mới tại `src/components` và một tệp trong thư mục đó gọi là `header.js`.
2.  Thêm code sau vào tệp mới `src/components/header.js`.

```jsx:title=src/components/header.js
import React from "react"

export default () => <h1>Đây là tiêu đề.</h1>
```

3.  Sửa đổi tệp `about.js` để nhập khẩu thành phần `Header`. Thay thế đánh dấu `h1` với `<Header />`:

```jsx:title=src/pages/about.js
import React from "react"
import Header from "../components/header" // highlight-line

export default () => (
  <div style={{ color: `teal` }}>
    <Header /> {/* highlight-line */}
    <p>Such wow. Very React.</p>
  </div>
)
```

![Thêm thành phần Header](06-header-component.png)

Trong trình duyệt, văn bản tiêu đề "Giới thiệu về Gatsby" bây giờ nên được thay bằng "Đây là tiêu đề." Nhưng bạn không muốn trang "About" hiển thị là "Đây là tiêu đề.". Bạn muốn nó hiển thị, "Giới thiệu về Gatsby".

4.  Trờ về tệp `src/components/header.js` và thực hiện những thay đổi sau:

```jsx:title=src/components/header.js
import React from "react"

export default props => <h1>{props.headerText}</h1> {/* highlight-line */}
```

5.  Trở về tệp `src/pages/about.js` và thực hiện những thay đổi sau:

```jsx:title=src/pages/about.js
import React from "react"
import Header from "../components/header"

export default () => (
  <div style={{ color: `teal` }}>
    <Header headerText="Giới thiệu về Gatsby" /> {/* highlight-line */}
    <p>Such wow. Very React.</p>
  </div>
)
```

![Truyền dữ liệu đến tiêu đề](07-pass-data-header.png)

Bây giờ bạn nên thấy văn bản tiêu đề "Giới thiệu về Gatsby" của bạn một lần nữa!

### “props” là gì?

Trước đó bạn định nghĩa các thành phần React là những đoạn code có thể tái sử dụng mô tả UI. Để làm cho các đoạn code có thể tái sử dụng này động bạn cần có khả năng cung cấp cho chúng với dữ liệu khác nhau. Bạn làm điều đó bằng đầu vào được gọi “props". Props là (đủ thích hợp) các thuộc tính được cung cấp cho các thành phần React.

Trong `about.js` bạn truyền một `headerText` prop với giá trị của `"Giới thiệu về Gatsby"` cho thành phần phụ `Header` được nhập:

```jsx:title=src/pages/about.js
<Header headerText="Giới thiệu về Gatsby" />
```

Trong `header.js`, thành phần tiêu đề hy vọng nhận được `headerText` prop (bởi vì bạn đã viết nó để mong đợi điều đó). Vì vậy bạn có thể truy cập nó như thế này:

```jsx:title=src/components/header.js
<h1>{props.headerText}</h1>
```

> 💡 Trong JSX, bạn có thể nhúng bất kì biểu thức JavaScript nào bằng cách gói nó với `{}`. Đây là cách bạn có thể truy cập vào thuộc tính `headerText` (hoặc là “prop!”) từ đối tượng “props”.

Nếu bạn đã truyền một prop khác tới thành phần `<Header />` của bạn, như vậy...

```jsx:title=src/pages/about.js
<Header headerText="Giới thiệu về Gatsby" arbitraryPhrase="is arbitrary" />
```

...bạn có thể truy cập vào `arbitraryPhrase` prop: `{props.arbitraryPhrase}`.

6.  Để nhấn mạnh cách làm cho thành phần của bạn có thể tái sử dụng, thêm một thành phần `<Header />` vào trang about, thêm code sau đây vào tệp `src/pages/about.js`, và lưu lại.

```jsx:title=src/pages/about.js
import React from "react"
import Header from "../components/header"

export default () => (
  <div style={{ color: `teal` }}>
    <Header headerText="Giới thiệu về Gatsby" />
    <Header headerText="It's pretty cool" /> {/* highlight-line */}
    <p>Such wow. Very React.</p>
  </div>
)
```

![Trùng lặp tiêu đề để thể hiện khả năng tái sử dụng](08-duplicate-header.png)

Và bạn có nó rồi đấy; Một tiêu đề thứ hai - không cần viết lại bất kì code gì - bằng cách truyền dữ liệu khác nhau sử dụng props.

### Sử dụng các thành phần bố cục

Các thành phần bố cục dành cho các phần của trang mà bạn muốn chia sẻ cho nhiều trang khác nhau. Ví dụ, các trang Gatsby thường sẽ có một thành phần bố cục với một tiêu đề và cuối trang được chia sẻ. Những điều phổ biến khác để thêm vào bố cục bao gồm thanh bên (sidebar) và/hoặc một menu điều hướng.

Bạn sẽ tìm hiểu thêm về các thành phần bố cục trong [**phần 3**](/tutorial/part-three/).

## Linking between pages

Bạn sẽ thường muốn kết nối giữa các trang — Hãy xem định tuyến trong một trang Gatsby.

### ✋ Sử dụng thành phần `<Link />`

1.  Mở thành phần trang mục lục (`src/pages/index.js`), xuất khẩu thành phần `<Link />` từ Gatsby, thêm một thành phần `<Link />` ở trên tiêu đề, và cung cấp cho nó một thuộc tính `to` với giá trị của `"/contact/"` cho tên đường dẫn:

```jsx:title=src/pages/index.js
import React from "react"
import { Link } from "gatsby" // highlight-line
import Header from "../components/header"

export default () => (
  <div style={{ color: `purple` }}>
    <Link to="/contact/">Contact</Link> {/* highlight-line */}
    <Header headerText="Hello Gatsby!" />
    <p>What a world.</p>
    <img src="https://source.unsplash.com/random/400x200" alt="" />
  </div>
)
```

Khi bạn bấm vào liên kết mới "Contact" trong trang chủ, bạn sẽ thấy...

![Trang Gatsby dev 404](09-dev-404.png)

...Trang Gatsby phát triển 404. Tại sao? Bởi vì bạn đang cố liên kết tới một trang chưa tồn tại.

2.  Bây giờ bạn sẽ phải tạo một thành phần trang cho trang "Contact" mới tại `src/pages/contact.js` và để nó liên kết với trang chủ:

```jsx:title=src/pages/contact.js
import React from "react"
import { Link } from "gatsby"
import Header from "../components/header"

export default () => (
  <div style={{ color: `teal` }}>
    <Link to="/">Home</Link>
    <Header headerText="Contact" />
    <p>Send us a message!</p>
  </div>
)
```

Sau khi bạn lưu tệp, bạn sẽ thấy trang contact và có thể theo liên kết để trở về trang chủ.

<video controls="controls" loop="true">
  <source type="video/mp4" src="./10-linking-between-pages.mp4"></source>
  <p>Xin lỗi! Trình duyệt của bạn không hỗ trợ video này.</p>
</video>

Thành phần `<Link />` của Gatsby là để liên kết giữa các trang trong trang web của bạn. Đối với các liên kết bên ngoài không được xử lí bởi trang Gatsby của bạn, sử dụng thẻ `<a>` HTML thông thường.

## Triển khai một trang Gatsby

Gatsby.js là một trình tạo web hiện đại, có nghĩa là không có máy chủ để thiết lập hoặc cơ sở dữ liệu phức tạp để triển khai. Thay vào đó, lệnh `build` của Gatsby tạo ra một thư mục chứa các tệp HTML và JavaScript tĩnh mà bạn có thể triển khai đến một dịch vụ lưu trữ trang web tĩnh.

Thử sử dụng [Surge](http://surge.sh/) để triển khai trang web Gatsby đầu tiên của bạn. Surge là một trong nhiều "máy chủ trang web tĩnh" cho phép triển khai các trang web Gatsbyis.

Nếu trước đó bạn vẫn chưa cài đặt &amp; thiết lập Surge, mở một cửa sở terminal và cài đặt công cụ dòng lệnh của họ:

```shell
npm install --global surge

# Then create a (free) account with them
surge login
```

Kế tiếp, xây dựng trang web của bạn bằng cách chạy lệnh sau trong terminal ở gốc của trang web của bạn (mẹo: đảm bảo bạn đang chạy lệnh này ở gốc của trang web của bạn, trong trường hợp này là thư mục hello-world, bạn có thể làm bằng cách mở một tab mới trong cùng một cửa sổ bạn đã sử dụng để chạy `gatsby develop`):

```shell
gatsby build
```

Việc xây dựng sẽ mất khoảng 15-30 giây. Một khi việc xây dựng hoàn tất, thật thú vị khi xem các tệp mà lệnh `gatsby build` vừa chuẩn bị để triển khai.

Hãy xem danh sách các tệp được tạo bằng cách nhập lệnh sau vào thư mục gốc của trang web của bạn, điều này cho phép bạn xem thư mục `public`:

```shell
ls public
```

Sau đó, cuối cùng triển khai trang web của bạn bằng cách xuất bản các tệp được tạo ra tới surge.sh.

```shell
surge public/
```

Khi điều này kết thúc, bạn sẽ thấy trong terminal của bạn một cái gì đó như:

![Ảnh chụp màn hình của việc xuất bản trang web Gatsby với Surge](surge-deployment.png)

Mở địa chỉ trang web được liệt kê ở dòng cuốiOpen the web address listed on the bottom line (`lowly-pain.surge.sh` trong trường hợp này) và bạn sẽ thấy trang web mới được xuất bản của bạn! Tuyệt vời!

## ➡️ Điều gì tiếp theo?

Trong phần này bạn:

- Học về mẫu khởi động Gatsby, và làm thế nào để sử dụng chúng để tạo dự án mới
- Học về cú pháp JSX
- Học về các thành phần
- Học về các thành phần trang Gatsby và các thành phần phụ
- Học về React “props” và tái sử dụng các thành phần React

Bây giờ, chuyển sang [**thêm kiểu vào trang web của bạn**](/tutorial/part-two/)!
